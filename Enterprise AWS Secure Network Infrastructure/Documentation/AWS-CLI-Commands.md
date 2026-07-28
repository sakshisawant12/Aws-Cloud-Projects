# AWS CLI Commands

This document contains commonly used AWS CLI commands related to the services implemented in the **Enterprise AWS Secure Network Infrastructure** project.

> **Note:** This project was primarily deployed using the AWS Management Console. The commands below demonstrate how the same resources can be viewed or managed using the AWS CLI.

---

# Configure AWS CLI

Configure AWS CLI with IAM user credentials.

```bash
aws configure
```

You'll be prompted to enter:

- AWS Access Key ID
- AWS Secret Access Key
- Default Region
- Output Format

---

# Verify AWS CLI Configuration

```bash
aws sts get-caller-identity
```

Purpose

- Verify AWS CLI authentication
- Display Account ID
- Display IAM User or Role

---

# Amazon EC2

## List EC2 Instances

```bash
aws ec2 describe-instances
```

Purpose

View all EC2 instances.

---

## Start an EC2 Instance

```bash
aws ec2 start-instances \
--instance-ids i-xxxxxxxxxxxxxxxxx
```

---

## Stop an EC2 Instance

```bash
aws ec2 stop-instances \
--instance-ids i-xxxxxxxxxxxxxxxxx
```

---

## Reboot an EC2 Instance

```bash
aws ec2 reboot-instances \
--instance-ids i-xxxxxxxxxxxxxxxxx
```

---

## Terminate an EC2 Instance

```bash
aws ec2 terminate-instances \
--instance-ids i-xxxxxxxxxxxxxxxxx
```

---

# Amazon VPC

## List VPCs

```bash
aws ec2 describe-vpcs
```

---

## List Subnets

```bash
aws ec2 describe-subnets
```

---

## List Route Tables

```bash
aws ec2 describe-route-tables
```

---

## List Security Groups

```bash
aws ec2 describe-security-groups
```

---

## List Network ACLs

```bash
aws ec2 describe-network-acls
```

---

## List Internet Gateways

```bash
aws ec2 describe-internet-gateways
```

---

## List NAT Gateways

```bash
aws ec2 describe-nat-gateways
```

---

## List VPC Peering Connections

```bash
aws ec2 describe-vpc-peering-connections
```

---

## List VPC Endpoints

```bash
aws ec2 describe-vpc-endpoints
```

---

# Amazon EBS

## List EBS Volumes

```bash
aws ec2 describe-volumes
```

---

## List Volume Attachments

```bash
aws ec2 describe-volumes \
--query "Volumes[*].Attachments"
```

---

## List Snapshots

```bash
aws ec2 describe-snapshots \
--owner-ids self
```

---

# Amazon S3

## List S3 Buckets

```bash
aws s3 ls
```

---

## List Objects in a Bucket

```bash
aws s3 ls s3://your-bucket-name
```

---

## Upload a File

```bash
aws s3 cp file.txt s3://your-bucket-name/
```

---

## Download a File

```bash
aws s3 cp s3://your-bucket-name/file.txt .
```

---

## Synchronize a Folder

```bash
aws s3 sync ./local-folder s3://your-bucket-name
```

---

# IAM

## List IAM Users

```bash
aws iam list-users
```

---

## List IAM Roles

```bash
aws iam list-roles
```

---

## List Attached Role Policies

```bash
aws iam list-attached-role-policies \
--role-name EC2-S3-Access-Role
```

---

# Useful Networking Commands

## View Elastic IP Addresses

```bash
aws ec2 describe-addresses
```

---

## View Network Interfaces

```bash
aws ec2 describe-network-interfaces
```

---

# Monitoring

## View EC2 Status

```bash
aws ec2 describe-instance-status
```

---

## List CloudWatch Metrics

```bash
aws cloudwatch list-metrics
```

---

# AWS CLI Summary

| Service | Common Command |
|----------|----------------|
| Configure CLI | `aws configure` |
| Verify Identity | `aws sts get-caller-identity` |
| EC2 | `describe-instances` |
| VPC | `describe-vpcs` |
| Subnets | `describe-subnets` |
| Route Tables | `describe-route-tables` |
| Security Groups | `describe-security-groups` |
| Network ACLs | `describe-network-acls` |
| NAT Gateway | `describe-nat-gateways` |
| VPC Endpoint | `describe-vpc-endpoints` |
| VPC Peering | `describe-vpc-peering-connections` |
| EBS | `describe-volumes` |
| S3 | `aws s3 ls` |
| IAM | `list-roles` |
| CloudWatch | `list-metrics` |

---

# Skills Demonstrated

- AWS CLI Configuration
- EC2 Management
- VPC Resource Inspection
- S3 Operations
- EBS Management
- IAM Administration
- Network Resource Management
- Basic AWS Automation
