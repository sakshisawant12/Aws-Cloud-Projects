# Linux Commands

This document contains the Linux commands used while deploying and managing the **Enterprise AWS Secure Network Infrastructure** project.

---

# 1. System Update

Update installed packages.

```bash
sudo yum update -y
```

Purpose

- Install the latest security patches
- Update system packages

---

# 2. Install Apache HTTP Server

Install Apache.

```bash
sudo yum install httpd -y
```

Purpose

Deploy the Apache Web Server.

---

# 3. Enable Apache Service

```bash
sudo systemctl enable httpd
```

Purpose

Start Apache automatically after every reboot.

---

# 4. Start Apache

```bash
sudo systemctl start httpd
```

Purpose

Start the Apache Web Server.

---

# 5. Check Apache Status

```bash
sudo systemctl status httpd
```

Purpose

Verify that Apache is running.

---

# 6. Restart Apache

```bash
sudo systemctl restart httpd
```

Purpose

Restart Apache after configuration changes.

---

# 7. Stop Apache

```bash
sudo systemctl stop httpd
```

Purpose

Stop the Apache service.

---

# 8. Edit Web Page

Open the default web page.

```bash
sudo nano /var/www/html/index.html
```

Purpose

Create a custom Apache landing page.

---

# 9. List Storage Devices

```bash
lsblk
```

Purpose

Display all attached block storage devices before configuring Amazon EBS.

---

# 10. Create File System

```bash
sudo mkfs.xfs /dev/nvme1n1
```

Purpose

Format the newly attached Amazon EBS volume.

---

# 11. Create Mount Directory

```bash
sudo mkdir /data
```

Purpose

Create a directory to mount the Amazon EBS volume.

---

# 12. Mount EBS Volume

```bash
sudo mount /dev/nvme1n1 /data
```

Purpose

Mount the EBS volume.

---

# 13. Verify Mounted File Systems

```bash
df -h
```

Purpose

Verify that the EBS volume is mounted successfully.

---

# 14. Display UUID

```bash
sudo blkid
```

Purpose

Retrieve the UUID of the EBS volume for persistent mounting.

---

# 15. Configure Automatic Mounting

```bash
sudo nano /etc/fstab
```

Purpose

Configure the EBS volume to mount automatically after system reboot.

---

# 16. Verify fstab Configuration

```bash
sudo mount -a
```

Purpose

Test the `/etc/fstab` configuration without rebooting.

---

# 17. Change File Permission

```bash
chmod 400 key.pem
```

Purpose

Restrict permissions on the private key before using SSH.

---

# 18. Secure Copy (SCP)

Copy the PEM file to the Bastion Host.

```bash
scp -i key.pem key.pem ec2-user@<Bastion-Public-IP>:~
```

Purpose

Transfer the private key securely to the Bastion Host.

---

# 19. SSH into Bastion Host

```bash
ssh -i key.pem ec2-user@<Bastion-Public-IP>
```

Purpose

Connect to the Bastion Host.

---

# 20. SSH into Apache Web Server

```bash
ssh -i key.pem ec2-user@<Web-Server-Private-IP>
```

Purpose

Access the Apache Web Server through the Bastion Host.

---

# 21. SSH into Private Application Server

```bash
ssh -i key.pem ec2-user@<Private-App-Private-IP>
```

Purpose

Securely access the Private Application Server through the Bastion Host.

---

# 22. Verify Network Connectivity

```bash
ping <Private-IP>
```

Purpose

Verify connectivity between Enterprise VPC and Development VPC after configuring VPC Peering.

---

# Linux Commands Summary

| Command | Purpose |
|----------|---------|
| yum update | Update packages |
| yum install httpd | Install Apache |
| systemctl enable | Enable Apache |
| systemctl start | Start Apache |
| systemctl status | Check Apache |
| systemctl restart | Restart Apache |
| systemctl stop | Stop Apache |
| nano | Edit files |
| lsblk | View storage devices |
| mkfs.xfs | Create filesystem |
| mkdir | Create mount directory |
| mount | Mount EBS volume |
| df -h | Verify mounted storage |
| blkid | Display UUID |
| mount -a | Test fstab |
| chmod 400 | Secure PEM key |
| scp | Copy files securely |
| ssh | Remote login |
| ping | Test network connectivity |

---

# Skills Demonstrated

- Linux Administration
- File System Management
- Storage Management
- SSH Administration
- Apache Web Server Management
- Amazon EBS Configuration
- Network Connectivity Testing
