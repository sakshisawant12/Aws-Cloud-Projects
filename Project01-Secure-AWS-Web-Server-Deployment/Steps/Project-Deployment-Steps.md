# 🚀 Secure AWS Web Server Deployment - Step-by-Step Guide

This document explains the complete deployment process of the Secure AWS Web Server project.

---

# Step 1: Launch an EC2 Instance

- Open the AWS Management Console.
- Navigate to EC2.
- Click **Launch Instance**.
- Enter the instance name.
- Select **Red Hat Enterprise Linux** AMI.
- Choose **t3.micro** instance type.
- Create or select an existing Key Pair.
- Configure the Security Group.
- Allow:
  - SSH (Port 22)
  - HTTP (Port 80)
- Launch the instance.

---

# Step 2: Connect to EC2

Open PowerShell or Terminal.

```bash
ssh -i web-key.pem ec2-user@<Public-IP>
```

Verify the connection.

---

# Step 3: Update the Server

```bash
sudo yum update -y
```

---

# Step 4: Install Apache HTTP Server

```bash
sudo yum install httpd -y
```

---

# Step 5: Start Apache

```bash
sudo systemctl start httpd
```

---

# Step 6: Enable Apache at Boot

```bash
sudo systemctl enable httpd
```

---

# Step 7: Verify Apache Status

```bash
sudo systemctl status httpd
```

---

# Step 8: Test Apache

Open the browser.

```
http://<Public-IP>
```

The Apache test page should appear.

---

# Step 9: Create Amazon EBS Volume

- Open the EC2 Console.
- Navigate to **Elastic Block Store → Volumes**.
- Create a new volume.
- Select the same Availability Zone as the EC2 instance.
- Attach the volume to the EC2 instance.

---

# Step 10: Verify Attached Disk

```bash
lsblk
```

---

# Step 11: Format the EBS Volume

```bash
sudo mkfs -t xfs /dev/nvme1n1
```

---

# Step 12: Create Mount Directory

```bash
sudo mkdir /data
```

---

# Step 13: Mount the Volume

```bash
sudo mount /dev/nvme1n1 /data
```

---

# Step 14: Verify Mount

```bash
df -h
```

---

# Step 15: Create a Test File

```bash
cd /data
sudo touch project.txt
ls
```

---

# Step 16: Configure Persistent Mount

Find the UUID.

```bash
sudo blkid
```

Edit the fstab file.

```bash
sudo nano /etc/fstab
```

Add:

```text
UUID=<Volume-UUID>   /data   xfs   defaults,nofail   0   2
```

---

# Step 17: Verify fstab Configuration

```bash
sudo mount -a
```

Check again.

```bash
df -h
```

---

# Step 18: Deploy the Website

Go to the Apache web directory.

```bash
cd /var/www/html
```

Edit the webpage.

```bash
sudo nano index.html
```

Paste your custom HTML.

Save the file.

---

# Step 19: Restart Apache

```bash
sudo systemctl restart httpd
```

---

# Step 20: Verify Website

Open:

```
http://<Public-IP>
```

The custom website should load successfully.

---

# Project Outcome

✔ Amazon EC2 instance deployed

✔ Apache HTTP Server installed

✔ Security Groups configured

✔ Amazon EBS attached and mounted

✔ Persistent storage configured using `/etc/fstab`

✔ Custom website successfully hosted on AWS
