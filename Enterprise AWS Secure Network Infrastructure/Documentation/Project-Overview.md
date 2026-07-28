# Enterprise AWS Secure Network Infrastructure

## Project Overview

This project demonstrates the design, deployment, and configuration of a secure AWS cloud infrastructure using Amazon Virtual Private Cloud (Amazon VPC). The infrastructure follows AWS networking best practices by separating resources into public and private subnets while implementing secure administrative access through a Bastion Host.

The project was built completely through hands-on implementation using the AWS Management Console and Linux command-line tools. It covers core AWS networking, compute, storage, identity, and connectivity services that are commonly used in enterprise cloud environments.

---

## Objectives

- Design a secure Virtual Private Cloud (VPC)
- Deploy public and private subnets
- Configure Internet and private network connectivity
- Secure EC2 instances using Security Groups and Network ACLs
- Implement secure SSH access using a Bastion Host
- Deploy and configure an Apache Web Server
- Configure outbound internet access using a NAT Gateway
- Attach and mount Amazon EBS storage
- Configure private Amazon S3 access using a Gateway VPC Endpoint
- Implement IAM Roles for secure service access
- Establish private communication between two VPCs using VPC Peering

---

# AWS Services Used

| Service | Purpose |
|----------|---------|
| Amazon VPC | Isolated virtual network |
| Public & Private Subnets | Network segmentation |
| Internet Gateway | Internet connectivity |
| Route Tables | Network routing |
| Security Groups | Instance-level firewall |
| Network ACLs | Subnet-level firewall |
| Amazon EC2 | Compute instances |
| Bastion Host | Secure SSH access |
| NAT Gateway | Outbound internet for private subnet |
| Elastic IP | Static public IP for NAT Gateway |
| Amazon EBS | Persistent block storage |
| Amazon S3 | Object storage |
| Gateway VPC Endpoint | Private S3 connectivity |
| IAM Roles | Secure access to AWS services |
| VPC Peering | Private communication between VPCs |

---

# Project Architecture

The infrastructure consists of two AWS Virtual Private Clouds.

## Enterprise VPC

CIDR

```
10.0.0.0/16
```

Resources

- Public Subnet
- Private Subnet
- Bastion Host
- Apache Web Server
- NAT Gateway
- Private Application Server
- Amazon EBS
- S3 Gateway Endpoint

---

## Development VPC

CIDR

```
192.168.0.0/16
```

Resources

- Public Subnet
- Development EC2 Instance

Both VPCs communicate securely using VPC Peering.

---

# Security Implementation

The project follows multiple security layers.

- Security Groups
- Network ACLs
- Private Subnet Isolation
- Bastion Host Administration
- IAM Roles
- Gateway VPC Endpoint

These controls ensure that private resources remain inaccessible from the public internet while still allowing secure administrative access.

---

# Key Features

- Enterprise-grade VPC architecture
- Public and private subnet deployment
- Secure SSH administration through Bastion Host
- Apache web server deployment
- NAT Gateway for private outbound access
- Persistent Amazon EBS storage
- Private Amazon S3 connectivity using Gateway Endpoint
- IAM Role-based authentication
- Cross-VPC communication using VPC Peering
- Troubleshooting of Network ACL ephemeral port issue

---

# Skills Demonstrated

- Amazon VPC
- Amazon EC2
- Amazon EBS
- Amazon S3
- IAM
- Security Groups
- Network ACLs
- Route Tables
- Internet Gateway
- NAT Gateway
- Elastic IP
- Gateway VPC Endpoint
- VPC Peering
- Linux Administration
- SSH
- Apache HTTP Server
- AWS Networking

---



