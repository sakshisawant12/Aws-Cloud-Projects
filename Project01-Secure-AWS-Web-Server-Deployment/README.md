# 🚀 Secure AWS Web Server Deployment

![AWS](https://img.shields.io/badge/AWS-EC2-orange?style=for-the-badge&logo=amazon-aws)
![Linux](https://img.shields.io/badge/Linux-RHEL-red?style=for-the-badge&logo=redhat)
![Apache](https://img.shields.io/badge/Web%20Server-Apache-D22128?style=for-the-badge&logo=apache)
![Storage](https://img.shields.io/badge/Storage-Amazon%20EBS-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen?style=for-the-badge)

A hands-on AWS Cloud project demonstrating how to deploy, secure, and manage a web server using **Amazon EC2**, **Red Hat Enterprise Linux**, **Apache HTTP Server**, **IAM**, **Security Groups**, and **Amazon EBS** with persistent storage.

---

# 📖 Project Overview

This project demonstrates the deployment of a secure Linux web server on AWS. The infrastructure was built from scratch using AWS best practices, including secure SSH access, least-privilege IAM permissions, Apache web server configuration, and persistent storage using Amazon EBS.

The project also covers Linux storage management by formatting, mounting, and configuring automatic EBS mounting using `/etc/fstab`.

---

# 🏗 Architecture



```text
                    Internet
                        │
                Public IPv4 Address
                        │
                Security Group
              (22 SSH, 80 HTTP)
                        │
                  Amazon EC2
             (Red Hat Enterprise Linux)
                        │
                Apache HTTP Server
                        │
                Hosted Static Website
                        │
          ┌─────────────┴─────────────┐
          │                           │
     Root EBS (10 GB)          Extra EBS (5 GB)
       Linux OS                   Mounted at /data
                               Persistent via /etc/fstab
```

---

# ⚙️ Technologies Used

| Category | Technology |
|----------|------------|
| Cloud Platform | Amazon Web Services (AWS) |
| Compute | Amazon EC2 |
| Storage | Amazon EBS |
| Operating System | Red Hat Enterprise Linux (RHEL) |
| Web Server | Apache HTTP Server |
| Identity & Access | AWS IAM |
| Networking | Security Groups |
| Remote Access | SSH |
| File System | XFS |
| Administration | Linux CLI |

---

# 🎯 Project Objectives

- Deploy a secure EC2 instance
- Configure IAM for secure access
- Configure Security Groups
- Connect using SSH
- Install Apache HTTP Server
- Host a static website
- Create and attach an Amazon EBS volume
- Format the volume using XFS
- Mount the EBS volume
- Configure automatic mounting using `/etc/fstab`

---


# 🚀 Step-by-Step Implementation

### ✅ Step 1 - IAM

- Created an IAM User
- Applied least privilege access
- Generated programmatic credentials

---

### ✅ Step 2 - Launch EC2

- Launched a Red Hat Enterprise Linux EC2 instance
- Configured Key Pair
- Configured Security Groups

---

### ✅ Step 3 - Connect using SSH

```bash
ssh -i web-key.pem ec2-user@PUBLIC_IP
```

---

### ✅ Step 4 - Install Apache

```bash
sudo yum update -y

sudo yum install httpd -y

sudo systemctl start httpd

sudo systemctl enable httpd
```

---

### ✅ Step 5 - Host Website

Created a custom HTML webpage and hosted it using Apache HTTP Server.

---

### ✅ Step 6 - Create Amazon EBS Volume

- Created a 5 GB General Purpose SSD (gp3) volume
- Attached it to the EC2 instance

---

### ✅ Step 7 - Configure Storage

```bash
sudo mkfs -t xfs /dev/nvme1n1

sudo mkdir /data

sudo mount /dev/nvme1n1 /data
```

---

### ✅ Step 8 - Persistent Mount

Configured automatic mounting using:

```text
/etc/fstab
```

using the filesystem UUID.

---

# 💻 Linux Commands Used

```bash
whoami
pwd
hostname
lsblk
df -h
blkid
mount
mkfs
mkdir
systemctl
yum
nano
```

---



# 🧠 Key Concepts Learned

- AWS IAM
- EC2 Deployment
- Linux Administration
- Apache HTTP Server
- SSH Authentication
- Security Groups
- Amazon EBS
- Linux File Systems
- UUID
- XFS
- `/etc/fstab`
- Persistent Storage

---

# 🎤 Interview Questions Covered

- Why use IAM Users instead of the Root User?
- What is Amazon EBS?
- Difference between Root Volume and Additional EBS Volume?
- What is UUID?
- Why use UUID in `/etc/fstab`?
- Difference between `lsblk` and `df -h`?
- Why do we format a new EBS volume?
- Why use XFS?
- What is a mount point?
- Why configure persistent storage?

---

# 🎯 Learning Outcomes

After completing this project, I gained hands-on experience in:

- Deploying secure cloud infrastructure on AWS
- Linux server administration
- Configuring Apache Web Server
- Managing Amazon EBS volumes
- Persistent storage configuration
- Linux filesystem management
- Troubleshooting common deployment issues

---

# 👩‍💻 Author

**Sakshi Sawant**

AWS Cloud Engineer Learning Journey 🚀

📌 GitHub: *https://github.com/sakshisawant12*

📌 LinkedIn: *www.linkedin.com/in/sakshi-sawant-508792392*

---

# ⭐ If you found this project helpful

Please consider giving this repository a ⭐.

