# Networking Concepts

This document explains the networking concepts implemented in the **Enterprise AWS Secure Network Infrastructure** project and their role in building a secure and scalable AWS environment.

---

# 1. Amazon VPC

Amazon Virtual Private Cloud (VPC) is a logically isolated virtual network in AWS where cloud resources can be launched securely.

## Implementation

| Property | Value |
|----------|-------|
| Name | Enterprise VPC |
| CIDR | 10.0.0.0/16 |

### Purpose

- Isolate AWS resources
- Control network communication
- Provide secure networking
- Enable subnet segmentation

---

# 2. Public Subnet

The Public Subnet hosts resources that require internet access.

## CIDR

```
10.0.1.0/24
```

## Resources Deployed

- Bastion Host
- Apache Web Server
- NAT Gateway

### Purpose

- Internet-facing services
- Administrative access
- Outbound internet for private resources

---

# 3. Private Subnet

The Private Subnet hosts internal resources that should not be directly accessible from the internet.

## CIDR

```
10.0.2.0/24
```

## Resources Deployed

- Private Application Server
- Amazon EBS

### Purpose

- Secure internal workloads
- Restrict direct internet access
- Improve security

---

# 4. Internet Gateway

An Internet Gateway (IGW) allows communication between the VPC and the public internet.

## Implementation

- Attached to Enterprise VPC
- Connected through the Public Route Table

### Purpose

- Enable inbound HTTP/HTTPS traffic
- Enable SSH access to public instances

---

# 5. Route Tables

Route Tables determine how network traffic flows inside the VPC.

## Public Route Table

Routes

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |
| 0.0.0.0/0 | Internet Gateway |

Associated With

- Public Subnet

---

## Private Route Table

Initially

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |

After NAT Gateway

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | NAT Gateway |

After S3 Gateway Endpoint

Amazon S3 Prefix List → Gateway Endpoint

After VPC Peering

192.168.0.0/16 → VPC Peering

---

# 6. Security Groups

Security Groups act as virtual firewalls at the EC2 instance level.

## Bastion Security Group

Allowed

- SSH (22) from My Public IP

Purpose

Secure administrative access.

---

## Web Security Group

Allowed

- HTTP (80)
- HTTPS (443)
- SSH (22) from Bastion Host

Purpose

Allow public web traffic while restricting SSH access.

---

## App Security Group

Allowed

- SSH (22) from Bastion Host

Purpose

Prevent direct public access to the Private Application Server.

---

# 7. Network ACLs

Network ACLs operate at the subnet level.

## Public NACL

Allowed

- SSH
- HTTP
- HTTPS
- Ephemeral Ports
- Outbound All Traffic

### Practical Scenario

Initially, the Public NACL did not allow Ephemeral Ports, causing connectivity issues with the Apache Web Server.

After adding the required Ephemeral Port range, the web server became accessible.

---

## Private NACL

Allowed

- SSH from Public Subnet (10.0.1.0/24)
- Outbound All Traffic

Purpose

Protect resources inside the Private Subnet.

---

# 8. Bastion Host

The Bastion Host is a public EC2 instance used to securely access private instances.

### Access Flow

```
Laptop

↓

PowerShell

↓

SSH

↓

Bastion Host

↓

Private EC2
```

### Benefits

- No direct SSH to Private EC2
- Centralized administration
- Improved security

---

# 9. NAT Gateway

The NAT Gateway enables outbound internet connectivity for private instances.

### Implementation

- Deployed inside Public Subnet
- Associated with an Elastic IP

### Purpose

Allow the Private Application Server to

- Install software
- Download packages
- Access external repositories

without exposing it to inbound internet traffic.

---

# 10. Elastic IP

Elastic IP provides a static public IP address.

### Implementation

Used only for the NAT Gateway.

### Purpose

Maintain consistent outbound internet connectivity.

---

# 11. Gateway VPC Endpoint

A Gateway Endpoint provides private connectivity between the VPC and Amazon S3.

### Configuration

- Endpoint Type : Gateway
- Service : Amazon S3
- Associated with Private Route Table

### Benefits

- No Internet Gateway required
- No NAT Gateway required
- Traffic remains inside the AWS network

---

# 12. IAM Role

An IAM Role was attached to the Private Application Server.

Permission

```
AmazonS3FullAccess
```

Purpose

Allow secure access to Amazon S3 without storing AWS credentials on the EC2 instance.

---

# 13. VPC Peering

VPC Peering enables private communication between two VPCs.

## Connected Networks

Enterprise VPC

```
10.0.0.0/16
```

Development VPC

```
192.168.0.0/16
```

### Route Updates

Enterprise Route Table

```
192.168.0.0/16 → VPC Peering
```

Development Route Table

```
10.0.0.0/16 → VPC Peering
```

### Verification

Connectivity was verified using the `ping` command between EC2 instances in both VPCs.

---

# Networking Flow

```
Internet
        │
        ▼
Internet Gateway
        │
        ▼
Public Subnet
 ├── Bastion Host
 ├── Apache Web Server
 └── NAT Gateway
        │
        ▼
Private Route Table
        │
        ▼
Private Application Server
        │
        ├── Amazon EBS
        ├── IAM Role
        └── S3 Gateway Endpoint
                    │
                    ▼
              Amazon S3

Enterprise VPC
        │
        ▼
VPC Peering
        │
        ▼
Development VPC
```

---

# Key Networking Skills Demonstrated

- Amazon VPC
- Public & Private Subnets
- CIDR Planning
- Internet Gateway
- Route Tables
- Security Groups
- Network ACLs
- Bastion Host
- NAT Gateway
- Elastic IP
- Gateway VPC Endpoint
- IAM Role Integration
- VPC Peering
- Private Network Communication
- Network Troubleshooting
