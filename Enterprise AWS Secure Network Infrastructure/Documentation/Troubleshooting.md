# Troubleshooting Guide

This document describes the issues encountered during the deployment of the **Enterprise AWS Secure Network Infrastructure** project and the steps taken to resolve them.

---

# Issue 1 – Apache Web Server Not Accessible

## Problem

The Apache Web Server was running successfully, but the website could not be accessed from the browser.

---

## Symptoms

- EC2 instance was in the **Running** state.
- Apache service (`httpd`) was active.
- Security Group allowed HTTP (80).
- Public IP address was assigned.
- Browser displayed a connection timeout.

---

## Root Cause

The **Public Network ACL** did not allow **Ephemeral Ports (1024–65535)** required for return traffic.

Although inbound HTTP traffic reached the instance, the response packets were blocked by the Network ACL.

---

## Solution

Added an inbound rule to the Public Network ACL:

| Protocol | Port Range | Source |
|----------|------------|--------|
| TCP | 1024–65535 | 0.0.0.0/0 |

After updating the Network ACL, the Apache website became accessible.

---

# Issue 2 – Unable to SSH into Private EC2

## Problem

Direct SSH access to the Private EC2 instance was not possible.

---

## Cause

The Private EC2 instance was deployed inside a **Private Subnet** without a Public IP address.

---

## Solution

Connected using the Bastion Host.

Connection Flow

```
Laptop
    │
    ▼
Bastion Host
    │
    ▼
Private EC2
```

This allowed secure administrative access without exposing the private instance to the internet.

---

# Issue 3 – Amazon EBS Volume Not Visible

## Problem

The newly attached Amazon EBS volume was not immediately available for use.

---

## Cause

The volume had been attached but was not formatted or mounted.

---

## Solution

Verify the attached disk.

```bash
lsblk
```

Create a filesystem.

```bash
sudo mkfs.xfs /dev/nvme1n1
```

Create a mount point.

```bash
sudo mkdir /data
```

Mount the volume.

```bash
sudo mount /dev/nvme1n1 /data
```

Verify the mount.

```bash
df -h
```

---

# Issue 4 – EBS Volume Not Mounted After Reboot

## Problem

After restarting the EC2 instance, the Amazon EBS volume was no longer mounted.

---

## Cause

The volume was mounted manually and no persistent mount configuration existed.

---

## Solution

Retrieve the volume UUID.

```bash
sudo blkid
```

Add an entry to `/etc/fstab`.

```bash
sudo nano /etc/fstab
```

Verify the configuration.

```bash
sudo mount -a
```

The volume now mounts automatically after every reboot.

---

# Issue 5 – Private EC2 Required Internet Access

## Problem

The Private Application Server needed internet access to install software and download updates.

---

## Cause

Private Subnets do not have direct internet connectivity.

---

## Solution

- Created a NAT Gateway in the Public Subnet.
- Allocated an Elastic IP.
- Updated the Private Route Table.

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | NAT Gateway |

The Private EC2 could now access the internet while remaining inaccessible from the public internet.

---

# Issue 6 – Secure Access to Amazon S3

## Problem

The Private EC2 required access to Amazon S3 without exposing traffic to the internet.

---

## Solution

Configured:

- Gateway VPC Endpoint
- IAM Role with `AmazonS3FullAccess`

This enabled secure, private communication with Amazon S3 over the AWS network.

---

# Issue 7 – VPC Peering Connectivity Failed

## Problem

Instances in the Enterprise VPC and Development VPC could not communicate.

---

## Possible Causes

- VPC Peering request not accepted
- Missing routes in Route Tables
- Security Group restrictions
- Network ACL restrictions

---

## Solution

Verified:

- VPC Peering connection status was **Active**
- Route Tables contained the correct peering routes
- Security Groups allowed required traffic
- Network ACLs allowed communication

Connectivity was successfully verified using:

```bash
ping <Private-IP>
```

---

# Best Practices Learned

- Verify Security Groups and Network ACLs together during network troubleshooting.
- Use a Bastion Host instead of assigning Public IPs to private servers.
- Configure `/etc/fstab` to ensure EBS volumes persist after reboot.
- Use IAM Roles instead of storing AWS credentials on EC2 instances.
- Access Amazon S3 privately using a Gateway VPC Endpoint.
- Test connectivity after each networking change to isolate issues quickly.

---

# Troubleshooting Checklist

| Check | Status |
|--------|--------|
| EC2 Instance Running | ✅ |
| Security Groups Verified | ✅ |
| Network ACL Rules Verified | ✅ |
| Route Tables Configured | ✅ |
| Internet Gateway Attached | ✅ |
| NAT Gateway Working | ✅ |
| Apache Service Running | ✅ |
| EBS Mounted Successfully | ✅ |
| IAM Role Attached | ✅ |
| S3 Gateway Endpoint Configured | ✅ |
| VPC Peering Active | ✅ |
| Connectivity Verified | ✅ |
