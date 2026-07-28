# 🚀 Enterprise AWS Secure Network Infrastructure

<p align="left">

![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)
![EC2](https://img.shields.io/badge/EC2-FF9900?style=for-the-badge)
![VPC](https://img.shields.io/badge/VPC-3F48CC?style=for-the-badge)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![RHEL](https://img.shields.io/badge/RHEL-EE0000?style=for-the-badge&logo=redhat&logoColor=white)
![Apache](https://img.shields.io/badge/Apache-CA2136?style=for-the-badge&logo=apache)
![Amazon EBS](https://img.shields.io/badge/Amazon_EBS-0A84FF?style=for-the-badge&logo=amazonaws&logoColor=white)
![Amazon S3](https://img.shields.io/badge/Amazon_S3-569A31?style=for-the-badge&logo=amazons3&logoColor=white)
![Project](https://img.shields.io/badge/Project-Completed-brightgreen?style=for-the-badge)

</p>

A hands-on AWS Cloud project demonstrating the design, deployment, and security of an enterprise network infrastructure using **Amazon VPC, EC2, IAM, Security Groups, Network ACLs, Bastion Host, NAT Gateway, Amazon EBS, Amazon S3 Gateway Endpoint, and VPC Peering**.

---

# 📖 Project Overview

This project focuses on building a secure AWS infrastructure following enterprise networking best practices.

The environment consists of:

- Enterprise VPC
- Public & Private Subnets
- Bastion Host
- Apache Web Server
- Private Application Server
- NAT Gateway
- Amazon EBS
- Amazon S3 Gateway Endpoint
- IAM Role
- VPC Peering

The project demonstrates secure administration, private networking, persistent storage, and private AWS service connectivity.

---

# 🏗️ Architecture

> Replace this image with your architecture diagram.

```text
Internet
    │
Internet Gateway
    │
──────── Public Subnet ────────
│  Bastion Host              │
│  Apache Web Server         │
│  NAT Gateway               │
──────────────────────────────
             │
             ▼
──────── Private Subnet ──────
│ Private Application Server │
│ Amazon EBS                 │
──────────────────────────────
             │
     IAM Role + Gateway Endpoint
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

# ✨ Features

- Enterprise VPC Architecture
- Public & Private Subnets
- Bastion Host Administration
- Apache Web Server Deployment
- Secure SSH Connectivity
- Security Groups
- Network ACLs
- NAT Gateway
- Amazon EBS Persistent Storage
- IAM Role Authentication
- Private Amazon S3 Access
- Gateway VPC Endpoint
- VPC Peering
- Linux Administration
- Network Troubleshooting

---

# 🛠️ AWS Services Used

| Service | Purpose |
|----------|---------|
| Amazon VPC | Virtual Network |
| EC2 | Compute |
| IAM | Identity & Access |
| Security Groups | Instance Firewall |
| Network ACL | Subnet Firewall |
| Internet Gateway | Internet Access |
| NAT Gateway | Private Internet Access |
| Route Tables | Traffic Routing |
| Amazon EBS | Persistent Storage |
| Amazon S3 | Object Storage |
| Gateway Endpoint | Private S3 Access |
| VPC Peering | Private VPC Communication |

---

# 📂 Repository Structure

```
Enterprise-AWS-Secure-Network-Infrastructure
│
├── Architecture/
├── Commands/
├── Documentation/
├── Images/
├── Screenshots/
├── README.md
└── LICENSE
```

---

# 🚀 Deployment Workflow

```
Create Enterprise VPC
        ↓
Create Public & Private Subnets
        ↓
Attach Internet Gateway
        ↓
Configure Route Tables
        ↓
Create Security Groups
        ↓
Configure Network ACLs
        ↓
Launch Bastion Host
        ↓
Launch Apache Web Server
        ↓
Configure NAT Gateway
        ↓
Launch Private EC2
        ↓
Attach Amazon EBS
        ↓
Configure Gateway Endpoint
        ↓
Attach IAM Role
        ↓
Create Development VPC
        ↓
Configure VPC Peering
        ↓
Verify Connectivity
```

---

# 🔒 Security Highlights

- Bastion Host for secure administration
- Private EC2 without Public IP
- Security Groups for instance-level protection
- Network ACLs for subnet-level filtering
- IAM Role for secure S3 access
- Gateway VPC Endpoint for private S3 connectivity
- NAT Gateway for outbound internet access
- VPC Peering for private inter-VPC communication

---

# 💻 Linux Commands Used

```bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
lsblk
mkfs.xfs
mount
blkid
mount -a
chmod 400 key.pem
ssh
scp
ping
```

---

# ☁️ AWS CLI Commands

```bash
aws configure
aws sts get-caller-identity
aws ec2 describe-instances
aws ec2 describe-vpcs
aws ec2 describe-subnets
aws ec2 describe-route-tables
aws ec2 describe-security-groups
aws ec2 describe-vpc-endpoints
aws ec2 describe-vpc-peering-connections
aws s3 ls
```

---

# 🔐 SSH Commands Used

### Connect to Bastion Host

```bash
ssh -i key.pem ec2-user@<Bastion-Public-IP>
```

### Copy Private Key to Bastion Host

```bash
scp -i key.pem key.pem ec2-user@<Bastion-Public-IP>:~
```

### Set Correct Permissions

```bash
chmod 400 key.pem
```

### Connect to Apache Web Server from Bastion

```bash
ssh -i key.pem ec2-user@<Web-Server-Private-IP>
```

### Connect to Private Application Server from Bastion

```bash
ssh -i key.pem ec2-user@<Private-App-Private-IP>
```

### SSH Connection Flow

```text
Laptop
   │
   ▼
Bastion Host
   │
   ├──► Apache Web Server
   │
   └──► Private Application Server
```

---

# 📸 Project Screenshots

| Section | Status |
|---------|--------|
| IAM | ✅ |
| Enterprise VPC | ✅ |
| Public & Private Subnets | ✅ |
| Internet Gateway | ✅ |
| Route Tables | ✅ |
| Security Groups | ✅ |
| Network ACLs | ✅ |
| Bastion Host | ✅ |
| Apache Web Server | ✅ |
| NAT Gateway | ✅ |
| Private EC2 | ✅ |
| Amazon EBS | ✅ |
| Amazon S3 | ✅ |
| Gateway Endpoint | ✅ |
| VPC Peering | ✅ |

> Screenshots are available in the `Screenshots/` directory.

---

# 📚 Documentation

| Document |
|----------|
| Project Overview |
| Deployment Steps |
| Networking Concepts |
| Security Implementation |
| Linux Commands |
| AWS CLI Commands |
| Troubleshooting |
| Learning Outcomes |

Detailed documentation is available in the **Documentation/** folder.

---

# 🎯 Skills Demonstrated

- AWS Cloud
- Amazon EC2
- Amazon VPC
- IAM
- Linux (RHEL)
- Apache HTTP Server
- Networking
- Security Groups
- Network ACLs
- NAT Gateway
- Amazon EBS
- Amazon S3
- Gateway VPC Endpoint
- VPC Peering
- SSH Administration
- Cloud Security
- Infrastructure Deployment

---

# 🚀 Future Improvements

- Application Load Balancer (ALB)
- Auto Scaling Group (ASG)
- Multi-AZ Deployment
- CloudWatch Monitoring
- CloudTrail Logging
- AWS Systems Manager
- Infrastructure as Code (Terraform / CloudFormation)

---

# 👩‍💻 Author

**Sakshi Sawant**



If you found this project helpful, consider giving it a ⭐ on GitHub!
