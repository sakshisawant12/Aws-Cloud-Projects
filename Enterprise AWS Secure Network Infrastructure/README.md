# Enterprise AWS Secure Network Infrastructure

## 📌 Project Overview

This project demonstrates the design and deployment of a secure enterprise AWS network infrastructure on Amazon Web Services (AWS). It focuses on implementing secure networking, private resource access, Linux administration, storage management, and inter-VPC communication using AWS best practices.

The architecture consists of an Enterprise VPC with public and private subnets, a Bastion Host for secure SSH access, a private application server, Amazon EBS for persistent storage, Amazon S3 with a Gateway Endpoint for private S3 access, and VPC Peering to securely connect multiple VPCs.

This project provides hands-on experience with core AWS networking services and security concepts required for Cloud Engineer and Cloud Support Engineer roles.

---

# 🏗️ Architecture

```text
                                    Internet
                                        │
                                Internet Gateway
                                        │
                          ┌─────────────┴─────────────┐
                          │                           │
                    Public Subnet               Private Subnet
                          │                           │
                    Bastion Host              Private App Server
                          │                           │
                          │                     Amazon EBS Volume
                          │                           │
                          │                    S3 Gateway Endpoint
                          │                           │
                          └──────────────► Amazon S3 ◄──────────────┘

                             Enterprise VPC
                                    │
                               VPC Peering
                                    │
                             Development VPC
                                    │
                             Development EC2
```

---

# ☁️ AWS Services Used

- AWS Identity and Access Management (IAM)
- Amazon Virtual Private Cloud (VPC)
- Public & Private Subnets
- Internet Gateway
- NAT Gateway
- Elastic IP
- Route Tables
- Security Groups
- Network ACLs (NACL)
- Amazon EC2
- Amazon EBS
- Amazon S3
- Amazon S3 Gateway Endpoint
- VPC Peering
- AWS CLI
- Linux (Amazon Linux)
- Apache HTTP Server

---

# 🚀 Project Features

- Designed a secure enterprise AWS network infrastructure.
- Implemented public and private subnet architecture.
- Configured Internet Gateway for internet connectivity.
- Configured NAT Gateway for secure outbound internet access from private subnet.
- Configured Route Tables for network routing.
- Implemented Security Groups and Network ACLs for traffic control.
- Deployed Bastion Host for secure SSH access.
- Launched private EC2 application server.
- Attached and mounted Amazon EBS storage.
- Configured Amazon S3 Gateway Endpoint for private S3 access.
- Established secure communication between Enterprise and Development VPCs using VPC Peering.
- Installed and configured Apache HTTP Server.
- Performed Linux server administration.
- Managed AWS resources using AWS CLI.

---

# 📂 Project Components

## IAM

- IAM Users
- IAM Groups
- IAM Policies
- Least Privilege Access

---

## Networking

- Enterprise VPC
- Development VPC
- CIDR Planning
- Public Subnet
- Private Subnet
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups
- Network ACLs
- Elastic IP
- VPC Peering

---

## Compute

- Amazon EC2
- Bastion Host
- Private Application Server
- Apache Web Server

---

## Storage

- Amazon EBS
- Volume Attachment
- File System Creation
- Persistent Mount using `/etc/fstab`

---

## Object Storage

- Amazon S3
- Bucket Versioning
- Bucket Encryption
- Lifecycle Management
- S3 Gateway Endpoint

---

# ⚙️ Deployment Steps

## Step 1

Created IAM users, groups, and policies following the principle of least privilege.

---

## Step 2

Created Enterprise VPC with custom CIDR block.

---

## Step 3

Created:

- Public Subnet
- Private Subnet

---

## Step 4

Configured:

- Internet Gateway
- Route Tables

---

## Step 5

Created NAT Gateway and associated Elastic IP.

---

## Step 6

Configured:

- Security Groups
- Network ACLs

---

## Step 7

Launched Bastion Host in the Public Subnet.

---

## Step 8

Launched Private EC2 Instance inside the Private Subnet.

---

## Step 9

Connected securely using SSH through Bastion Host.

```bash
ssh -i key.pem ec2-user@<Bastion-Public-IP>

ssh -i key.pem ec2-user@<Private-IP>
```

---

## Step 10

Configured Apache Web Server.

```bash
sudo yum update -y
sudo yum install httpd -y

sudo systemctl enable httpd
sudo systemctl start httpd
```

---

## Step 11

Created Amazon EBS Volume.

Attached the volume.

Verified:

```bash
lsblk
```

Formatted:

```bash
sudo mkfs -t xfs /dev/xvdf
```

Mounted:

```bash
sudo mount /dev/xvdf /data
```

Persistent Mount:

```bash
sudo blkid

sudo nano /etc/fstab
```

Verified:

```bash
df -h
```

---

## Step 12

Created Amazon S3 Bucket.

Configured:

- Versioning
- Encryption
- Lifecycle Rule

---

## Step 13

Configured Amazon S3 Gateway Endpoint.

Verified private access to S3.

---

## Step 14

Created Development VPC.

Configured VPC Peering.

Updated Route Tables.

Verified successful connectivity.

---

# 💻 Linux Commands Used

```bash
hostname

hostname -I

pwd

ls

lsblk

df -h

mount

blkid

mkdir

cd

chmod

chown

yum update

yum install httpd

systemctl status httpd

systemctl enable httpd

systemctl start httpd

ssh

ping

curl
```

---

# 🔒 Security Implementation

- IAM Least Privilege
- Private Subnet Isolation
- Bastion Host Architecture
- Security Groups
- Network ACLs
- Private S3 Access using Gateway Endpoint
- Controlled SSH Access
- Persistent Storage Encryption Support

---

# 🌐 Networking Concepts Demonstrated

- CIDR Blocks
- Public vs Private Subnets
- Internet Gateway
- NAT Gateway
- Elastic IP
- Route Tables
- Security Groups
- Network ACLs
- Bastion Host
- SSH
- VPC Peering
- Amazon S3 Gateway Endpoint

---



# 🧠 Key Learning Outcomes

- Designed a secure enterprise AWS network architecture.
- Implemented secure networking using AWS VPC.
- Managed compute resources using Amazon EC2.
- Configured persistent storage with Amazon EBS.
- Implemented secure S3 access using Gateway Endpoints.
- Configured secure SSH access using a Bastion Host.
- Established secure communication between VPCs using VPC Peering.
- Strengthened Linux administration and AWS CLI skills.
- Gained hands-on experience with AWS networking and security best practices.

---

# 🚀 Future Enhancements

- Application Load Balancer (ALB)
- Auto Scaling Group
- Amazon Route 53
- Amazon RDS
- Amazon CloudWatch Monitoring
- Infrastructure as Code (Terraform)
- CI/CD Integration
- Multi-AZ High Availability Architecture

---

# 📚 Skills Demonstrated

- AWS Cloud
- IAM
- Amazon VPC
- EC2
- EBS
- Amazon S3
- VPC Peering
- Security Groups
- Network ACLs
- Internet Gateway
- NAT Gateway
- AWS CLI
- Linux Administration
- Apache HTTP Server
- Networking
- Cloud Security
- Troubleshooting

---

## 👩‍💻 Author

**Sakshi Santosh Sawant**

Cloud Computing Enthusiast | AWS | Linux | Networking

GitHub: https://github.com/sakshisawant12
LinkedIn: *(Add your LinkedIn profile here)*
