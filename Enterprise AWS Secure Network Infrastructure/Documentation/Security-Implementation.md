# Security Implementation

This document explains the security controls implemented in the **Enterprise AWS Secure Network Infrastructure** project to protect cloud resources, restrict unauthorized access, and follow AWS security best practices.

---

# Security Overview

The infrastructure was designed using a **defense-in-depth** approach by implementing multiple security layers.

Security was achieved using:

- Security Groups
- Network ACLs
- Public and Private Subnet Isolation
- Bastion Host
- IAM Roles
- Gateway VPC Endpoint
- Route Table Configuration

---

# Security Architecture

```
                Internet
                    │
        HTTP/HTTPS  │  SSH (My IP)
                    │
                    ▼
          Public Subnet
      ┌────────────────────┐
      │ Bastion Host       │
      │ Apache Web Server  │
      │ NAT Gateway        │
      └────────────────────┘
               │
          SSH Only
               │
               ▼
        Private Subnet
      ┌────────────────────┐
      │ Private App Server │
      │ Amazon EBS         │
      └────────────────────┘
               │
               ▼
      S3 Gateway Endpoint
               │
               ▼
         Amazon S3 Bucket
```

---

# Security Groups

Security Groups provide instance-level firewall protection.

---

## Bastion Security Group

### Purpose

Allow secure administrative SSH access.

### Inbound Rules

| Protocol | Port | Source |
|----------|------|--------|
| SSH | 22 | My Public IP |

### Outbound Rules

Allow All Traffic

---

## Web Security Group

### Purpose

Allow public users to access the web application while restricting administrative access.

### Inbound Rules

| Protocol | Port | Source |
|----------|------|--------|
| HTTP | 80 | Anywhere |
| HTTPS | 443 | Anywhere |
| SSH | 22 | Bastion Security Group |

### Outbound Rules

Allow All Traffic

---

## Application Security Group

### Purpose

Protect the Private Application Server.

### Inbound Rules

| Protocol | Port | Source |
|----------|------|--------|
| SSH | 22 | Bastion Security Group |

### Outbound Rules

Allow All Traffic

---

# Network ACLs

Network ACLs provide subnet-level security.

---

## Public Network ACL

Associated with

- Public Subnet

### Inbound Rules

- SSH
- HTTP
- HTTPS
- Ephemeral Ports (1024–65535)

### Outbound Rules

Allow All Traffic

---

## Private Network ACL

Associated with

- Private Subnet

### Inbound Rules

SSH

Source

```
10.0.1.0/24
```

### Outbound Rules

Allow All Traffic

---

# Bastion Host

The Bastion Host acts as the only administrative entry point into the infrastructure.

SSH Flow

```
Laptop

↓

PowerShell

↓

Bastion Host

↓

Apache Web Server

or

↓

Private App Server
```

Advantages

- No direct SSH access to private resources
- Centralized administration
- Reduced attack surface

---

# Private Subnet Isolation

The Private Application Server is deployed inside a Private Subnet.

Characteristics

- No Public IP
- No Internet Gateway
- Not directly accessible from the Internet
- Accessible only through the Bastion Host

This reduces the risk of unauthorized access.

---

# NAT Gateway Security

The NAT Gateway provides outbound internet connectivity to private resources.

Purpose

- Install packages
- Download updates
- Access external repositories

without allowing inbound internet connections.

---

# IAM Role

Instead of storing AWS credentials on the EC2 instance, an IAM Role was attached.

Permission

```
AmazonS3FullAccess
```

Benefits

- Temporary AWS credentials
- No hardcoded Access Keys
- Secure service-to-service communication

---

# Gateway VPC Endpoint

A Gateway Endpoint was configured for Amazon S3.

Benefits

- Private communication with Amazon S3
- Traffic remains inside the AWS network
- No Internet Gateway required
- No NAT Gateway required for S3 access

---

# VPC Peering Security

A VPC Peering connection was established between:

- Enterprise VPC
- Development VPC

Route tables were updated to allow only private communication between the two networks.

No public internet was used for VPC-to-VPC communication.

---

# Security Issue Encountered

## Problem

The Apache Web Server was not reachable after deployment.

## Root Cause

The Public Network ACL did not allow Ephemeral Ports required for return traffic.

## Solution

Added the Ephemeral Port range:

```
1024–65535
```

After updating the Network ACL, SSH and HTTP communication worked successfully.

---

# Security Best Practices Implemented

- Principle of Least Privilege
- Public and Private Network Segmentation
- Bastion Host Administration
- Security Group Restrictions
- Network ACL Filtering
- IAM Role Authentication
- Private S3 Access using Gateway Endpoint
- Private EC2 Deployment
- Route Table Isolation
- VPC Peering for Internal Communication

---

# Security Services Used

- Amazon VPC
- Security Groups
- Network ACLs
- Bastion Host
- IAM Roles
- Internet Gateway
- NAT Gateway
- Gateway VPC Endpoint
- VPC Peering

---

# Key Learning Outcomes

- Implemented layered network security in AWS.
- Restricted administrative access using a Bastion Host.
- Secured private workloads with Security Groups and Network ACLs.
- Enabled secure service access using IAM Roles.
- Configured private Amazon S3 connectivity using a Gateway Endpoint.
- Established secure communication between two VPCs using VPC Peering.
- Troubleshot and resolved a Network ACL configuration issue involving ephemeral ports.
