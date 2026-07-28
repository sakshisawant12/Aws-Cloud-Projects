# Enterprise AWS Secure Network Infrastructure

# Deployment Steps

This document explains the complete deployment process followed to build the Enterprise AWS Secure Network Infrastructure project using the AWS Management Console and Linux commands.

---

# Phase 1 – Enterprise Network Foundation

## Step 1 – Create Enterprise VPC

Create a Virtual Private Cloud.

| Property | Value |
|----------|-------|
| Name | Enterprise VPC |
| CIDR Block | 10.0.0.0/16 |
| Tenancy | Default |

---

## Step 2 – Create Subnets

Create two subnets inside the Enterprise VPC.

### Public Subnet

| Property | Value |
|----------|-------|
| CIDR | 10.0.1.0/24 |
| Purpose | Public Resources |

### Private Subnet

| Property | Value |
|----------|-------|
| CIDR | 10.0.2.0/24 |
| Purpose | Private Resources |

---

## Step 3 – Create Internet Gateway

- Create Internet Gateway
- Attach it to Enterprise VPC

---

## Step 4 – Configure Public Route Table

Create Public Route Table.

Routes

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |
| 0.0.0.0/0 | Internet Gateway |

Associate the Public Route Table with the Public Subnet.

---

## Step 5 – Configure Private Route Table

Create Private Route Table.

Initially configure only:

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |

Associate the Private Route Table with the Private Subnet.

No Internet Gateway is attached at this stage.

---

# Phase 2 – Security Configuration

## Step 6 – Create Security Groups

### Bastion-SG

Inbound Rules

| Type | Source |
|------|--------|
| SSH (22) | My Public IP |

---

### Web-SG

Inbound Rules

| Type | Source |
|------|--------|
| HTTP | Anywhere |
| HTTPS | Anywhere |
| SSH | Bastion-SG |

---

### App-SG

Inbound Rules

| Type | Source |
|------|--------|
| SSH | Bastion-SG |

---

## Step 7 – Configure Network ACLs

### Public NACL

Associate with Public Subnet.

Inbound Rules

- SSH
- HTTP
- HTTPS

Outbound Rules

- Allow All Traffic

---

### Private NACL

Associate with Private Subnet.

Inbound Rules

- SSH
- Source : 10.0.1.0/24

Outbound Rules

- Allow All Traffic

---

# Phase 3 – Public Infrastructure

## Step 8 – Launch Bastion Host

Configuration

- Enterprise VPC
- Public Subnet
- Bastion-SG
- Auto Assign Public IP Enabled

---

## Step 9 – Launch Apache Web Server

Configuration

- Enterprise VPC
- Public Subnet
- Web-SG
- Auto Assign Public IP Enabled

---

## Step 10 – Connect to Bastion Host

SSH into Bastion Host using PowerShell.

```bash
ssh -i key.pem ec2-user@<Public-IP>
```

---

Copy the PEM key to Bastion Host.

```bash
scp -i key.pem key.pem ec2-user@<Bastion-IP>:~
```

---

Set proper permissions.

```bash
chmod 400 key.pem
```

---

SSH from Bastion Host to Apache Web Server.

```bash
ssh -i key.pem ec2-user@<Web-Private-IP>
```

---

Install Apache.

```bash
sudo yum update -y

sudo yum install httpd -y

sudo systemctl enable httpd

sudo systemctl start httpd
```

---

Edit the web page.

```bash
sudo nano /var/www/html/index.html
```

---

## Step 11 – Troubleshooting

Issue

Apache Web Server was not reachable.

Root Cause

Ephemeral ports were missing in the Public Network ACL.

Solution

Allow the required Ephemeral Port range.

After updating the Network ACL, the Apache website became accessible.

---

# Phase 4 – Private Network

## Step 12 – Create NAT Gateway

Allocate an Elastic IP.

Create NAT Gateway inside the Public Subnet.

Update Private Route Table.

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | NAT Gateway |

This allows private resources to access the internet without exposing them publicly.

---

# Phase 5 – Private Application Server

## Step 13 – Launch Private EC2

Configuration

- Enterprise VPC
- Private Subnet
- App-SG

---

## Step 14 – Connect Through Bastion Host

SSH into the Private EC2 through Bastion Host.

```bash
ssh -i key.pem ec2-user@<Private-IP>
```

---

# Phase 6 – Amazon EBS

## Step 15 – Attach Amazon EBS

Attach a new EBS Volume to the Private EC2.

Verify the disk.

```bash
lsblk
```

Create filesystem.

```bash
sudo mkfs.xfs /dev/nvme1n1
```

Create mount directory.

```bash
sudo mkdir /data
```

Mount the volume.

```bash
sudo mount /dev/nvme1n1 /data
```

Verify.

```bash
df -h
```

Retrieve UUID.

```bash
sudo blkid
```

Configure persistent mounting.

```bash
sudo nano /etc/fstab
```

Test.

```bash
sudo mount -a
```

---

# Phase 7 – Amazon S3

## Step 16 – Create Amazon S3 Bucket

Create a new S3 Bucket.

---

## Step 17 – Configure Gateway Endpoint

Configuration

| Property | Value |
|----------|-------|
| Type | Gateway |
| Service | Amazon S3 |
| VPC | Enterprise VPC |
| Route Table | Private Route Table |
| Policy | Full Access |

---

## Step 18 – Create IAM Role

Configuration

| Property | Value |
|----------|-------|
| Trusted Entity | AWS Service |
| Use Case | EC2 |
| Permission | AmazonS3FullAccess |

---

## Step 19 – Attach IAM Role

Attach the IAM Role to the Private EC2.

Actions

Security

↓

Modify IAM Role

↓

Select EC2-S3-Access-Role

↓

Update IAM Role

The Private EC2 can now access Amazon S3 through the Gateway Endpoint without using the public internet.

---

# Phase 8 – Development Environment

## Step 20 – Create Development VPC

Create

- Development VPC
- Public Subnet
- Internet Gateway
- Route Table
- Security Group
- Development EC2

---

# Phase 9 – VPC Peering

## Step 21 – Create VPC Peering

Requester

Enterprise VPC

Accepter

Development VPC

Accept the request.

---

## Step 22 – Update Route Tables

Enterprise Private Route Table

| Destination | Target |
|-------------|--------|
| 192.168.0.0/16 | VPC Peering |

Development Route Table

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | VPC Peering |

---

# Phase 10 – Connectivity Verification

## Step 23 – Verify Connectivity

Test private communication between the Enterprise and Development VPCs.

```bash
ping <Private-IP>
```

Successful ping confirms that VPC Peering has been configured correctly.

---

# Deployment Summary

✔ Enterprise VPC Created

✔ Public & Private Subnets Configured

✔ Internet Gateway Attached

✔ Route Tables Configured

✔ Security Groups Configured

✔ Network ACLs Configured

✔ Bastion Host Deployed

✔ Apache Web Server Deployed

✔ Public NACL Troubleshooting Completed

✔ NAT Gateway Configured

✔ Private EC2 Deployed

✔ Amazon EBS Attached

✔ Amazon S3 Gateway Endpoint Configured

✔ IAM Role Attached

✔ Development VPC Created

✔ VPC Peering Configured

✔ End-to-End Connectivity Verified
