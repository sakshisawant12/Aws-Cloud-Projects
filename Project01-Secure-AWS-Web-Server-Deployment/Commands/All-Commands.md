# 💻 All Commands Used – Secure AWS Web Server Deployment

This file contains all the Linux and AWS-related commands used in this project.

---

## 1. Connect to EC2

```bash
ssh -i web-key.pem ec2-user@<PUBLIC-IP>
```

---

## 2. Update the System

```bash
sudo yum update -y
```

---

## 3. Install Apache HTTP Server

```bash
sudo yum install httpd -y
```

---

## 4. Start Apache Service

```bash
sudo systemctl start httpd
```

---

## 5. Enable Apache on Boot

```bash
sudo systemctl enable httpd
```

---

## 6. Check Apache Status

```bash
sudo systemctl status httpd
```

---

## 7. Restart Apache

```bash
sudo systemctl restart httpd
```

---

## 8. Stop Apache

```bash
sudo systemctl stop httpd
```

---

## 9. Verify Apache is Listening

```bash
sudo ss -tulnp | grep :80
```

---

## 10. Open Website Locally

```bash
curl http://localhost
```

---

## 11. Check Available Disks

```bash
lsblk
```

---

## 12. Format the EBS Volume

```bash
sudo mkfs -t xfs /dev/nvme1n1
```

---

## 13. Create Mount Directory

```bash
sudo mkdir /data
```

---

## 14. Mount the EBS Volume

```bash
sudo mount /dev/nvme1n1 /data
```

---

## 15. Verify Mounted Volumes

```bash
df -h
```

---

## 16. Navigate to Mounted Volume

```bash
cd /data
```

---

## 17. Create Test File

```bash
sudo touch project.txt
```

---

## 18. List Files

```bash
ls
```

---

## 19. Get Volume UUID

```bash
sudo blkid
```

---

## 20. Edit fstab

```bash
sudo nano /etc/fstab
```

Example entry:

```text
UUID=<YOUR-UUID> /data xfs defaults,nofail 0 2
```

---

## 21. Test fstab Configuration

```bash
sudo mount -a
```

---

## 22. Verify Mount Again

```bash
df -h
```

---

## 23. Go to Website Directory

```bash
cd /var/www/html
```

---

## 24. Edit Website

```bash
sudo nano index.html
```

---

## 25. View Website File

```bash
cat index.html
```

---

## 26. Check Apache Configuration

```bash
sudo apachectl configtest
```

---

## 27. Check Current Directory

```bash
pwd
```

---

## 28. Display File Contents

```bash
cat /etc/fstab
```

---

## 29. Check Internet Connectivity

```bash
curl ifconfig.me
```

---

## 30. Open Website in Browser

```text
http://<PUBLIC-IP>
```

---

# Project Completed Successfully ✅

- EC2 Instance Created
- Apache Installed
- Security Group Configured
- Amazon EBS Attached
- EBS Mounted
- Persistent Mount Configured
- Custom Website Deployed
