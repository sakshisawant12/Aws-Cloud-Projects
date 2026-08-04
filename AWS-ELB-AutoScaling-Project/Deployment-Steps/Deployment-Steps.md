# 🚀 Deployment Steps

This document explains how to deploy an **AWS Application Load Balancer (ALB) with an Auto Scaling Group (ASG)** using a Launch Template.

---

# Architecture Overview

```
Users
   │
   ▼
Internet
   │
   ▼
Application Load Balancer
   │
   ▼
Target Group
   │
   ▼
Auto Scaling Group
   │
   ▼
EC2 Instances
```

---

# Step 1: Create a VPC

- Create a custom VPC.
- CIDR Block:
  ```
  10.0.0.0/16
  ```

---

# Step 2: Create Public Subnets

Create two public subnets in different Availability Zones.

| Subnet | CIDR | Availability Zone |
|---------|------|-------------------|
| Public Subnet 1 | 10.0.1.0/24 | ap-south-1a |
| Public Subnet 2 | 10.0.2.0/24 | ap-south-1b |

---

# Step 3: Create Internet Gateway

1. Create an Internet Gateway.
2. Attach it to the VPC.

---

# Step 4: Configure Route Table

Create a Public Route Table.

Add route:

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | Internet Gateway |

Associate both public subnets with the route table.

---

# Step 5: Create Security Groups

## ALB Security Group

Inbound Rules

| Type | Port | Source |
|------|------|--------|
| HTTP | 80 | 0.0.0.0/0 |

Outbound

- Allow All

---

## EC2 Security Group

Inbound Rules

| Type | Port | Source |
|------|------|--------|
| HTTP | 80 | ALB Security Group |
| SSH | 22 | My IP |

Outbound

- Allow All

---

# Step 6: Create a Launch Template

Navigate to

```
EC2
→ Launch Templates
→ Create Launch Template
```

Configure

- Amazon Linux 2023
- t3.micro
- Key Pair
- EC2 Security Group
- IAM Role (Optional)

Paste the following User Data script.

```bash
#!/bin/bash

dnf update -y
dnf install -y httpd

systemctl enable httpd
systemctl start httpd

TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
-H "X-aws-ec2-metadata-token-ttl-seconds: 21600")

INSTANCE_ID=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" \
http://169.254.169.254/latest/meta-data/instance-id)

HOSTNAME=$(hostname)

AZ=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" \
http://169.254.169.254/latest/meta-data/placement/availability-zone)

PRIVATE_IP=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" \
http://169.254.169.254/latest/meta-data/local-ipv4)

cat <<EOF > /var/www/html/index.html
<!DOCTYPE html>
<html>
<head>
<title>AWS ELB & Auto Scaling Project</title>
<style>
body{
font-family:Arial;
background:#0f172a;
color:white;
text-align:center;
padding-top:60px;
}
.card{
width:650px;
margin:auto;
background:#1e293b;
padding:30px;
border-radius:12px;
box-shadow:0 0 15px rgba(0,0,0,.4);
}
h1{
color:#38bdf8;
}
table{
margin:auto;
font-size:18px;
}
td{
padding:10px 20px;
}
</style>
</head>
<body>

<div class="card">

<h1>AWS ELB & Auto Scaling Project</h1>

<h2>Application Load Balancer + Auto Scaling Group</h2>

<table>

<tr>
<td><b>Instance ID</b></td>
<td>$INSTANCE_ID</td>
</tr>

<tr>
<td><b>Hostname</b></td>
<td>$HOSTNAME</td>
</tr>

<tr>
<td><b>Availability Zone</b></td>
<td>$AZ</td>
</tr>

<tr>
<td><b>Private IP</b></td>
<td>$PRIVATE_IP</td>
</tr>

</table>

</div>

</body>
</html>
EOF
```

Create the Launch Template.

---

# Step 7: Create Target Group

Navigate to

```
EC2
→ Target Groups
```

Configuration

- Target Type: Instance
- Protocol: HTTP
- Port: 80
- Health Check Path: /

Register EC2 instances.

---

# Step 8: Create Application Load Balancer

Navigate to

```
EC2
→ Load Balancers
```

Configuration

- Internet Facing
- Application Load Balancer
- IPv4
- Select VPC
- Select both Public Subnets
- Attach ALB Security Group
- Add HTTP Listener (Port 80)
- Forward requests to Target Group

Create the ALB.

---

# Step 9: Create Auto Scaling Group

Navigate to

```
EC2
→ Auto Scaling Groups
```

Configuration

Launch Template

```
WebServer-LT
```

Network

- Select VPC
- Select both Public Subnets

Load Balancing

- Attach existing Load Balancer
- Select Target Group

Capacity

| Setting | Value |
|----------|-------|
| Desired | 2 |
| Minimum | 2 |
| Maximum | 4 |

Health Check

- EC2
- ELB

Create the Auto Scaling Group.

---

# Step 10: Configure Scaling Policy

Create a Target Tracking Scaling Policy.

Configuration

| Setting | Value |
|----------|-------|
| Metric | Average CPU Utilization |
| Target Value | 50% |

This automatically creates CloudWatch alarms to manage scaling.

---

# Step 11: Validate Load Balancer

Open the ALB DNS Name.

Example

```
http://<ALB-DNS>
```

Verify the webpage displays:

- Instance ID
- Hostname
- Availability Zone
- Private IP

Refresh the page multiple times to observe requests being served by different EC2 instances.

---

# Step 12: Simulate High CPU Load

Connect to the EC2 instances.

Install the stress utility.

```bash
sudo dnf install stress -y
```

Generate CPU load.

```bash
sudo stress --cpu 2 --timeout 900
```

Run the command on multiple instances simultaneously.

---

# Step 13: Verify Auto Scaling

Navigate to

```
EC2
→ Auto Scaling Groups
```

Observe that:

- CPU utilization increases.
- Auto Scaling launches additional EC2 instances.
- New instances register automatically with the Target Group.
- The Application Load Balancer starts routing traffic to healthy instances.

---

# Step 14: Cleanup Resources

To avoid AWS charges, delete resources in the following order:

1. Delete Auto Scaling Group
2. Delete Load Balancer
3. Delete Target Group
4. Delete Launch Template
5. Terminate EC2 Instances
6. Delete Security Groups
7. Delete Route Tables
8. Detach and Delete Internet Gateway
9. Delete Public Subnets
10. Delete VPC

---

# Deployment Summary

✅ Custom VPC

✅ Public Subnets across Multiple Availability Zones

✅ Internet Gateway

✅ Route Tables

✅ Security Groups

✅ Launch Template

✅ User Data Automation

✅ EC2 Instances

✅ Target Group

✅ Application Load Balancer

✅ Auto Scaling Group

✅ Target Tracking Scaling Policy

✅ CPU Load Testing

✅ Automatic Scale-Out Validation
