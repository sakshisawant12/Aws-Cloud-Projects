# 🚀 Deployment Guide - AWS S3 Static Website Hosting

This guide walks through the complete deployment of a static website using **Amazon S3**. It also covers enabling **Versioning** and configuring **Replication** for improved data protection.

---

# 📋 Prerequisites

Before starting, ensure you have:

- AWS Account
- Access to the AWS Management Console
- Basic knowledge of Amazon S3
- Website files ready (HTML, CSS, Images)

Example website files:

```text
index.html
style.css
hero.jpg
coffee1.jpg
coffee2.jpg
coffee3.jpg
coffee4.jpg
```

---

# Step 1: Create an Amazon S3 Bucket

1. Sign in to the AWS Management Console.
2. Search for **Amazon S3**.
3. Click **Create bucket**.
4. Enter a globally unique bucket name.

Example:

```text
brew-haven-static-website
```

5. Select your preferred AWS Region.
6. Leave other settings as default.
7. Click **Create bucket**.

---

# Step 2: Upload Website Files

Open the newly created bucket.

Click **Upload**.

Upload all website files.

Example:

```text
index.html
style.css
hero.jpg
coffee1.jpg
coffee2.jpg
coffee3.jpg
coffee4.jpg
```

Click **Upload** to store the files in the bucket.

---

# Step 3: Disable Block Public Access

Since this project hosts a public website, public access must be enabled.

Navigate to:

```
Permissions
```

Locate:

```
Block Public Access
```

Click **Edit**.

Uncheck all Block Public Access options.

Save the changes.

> **Note:** Public access is required only for this learning project. In production, use CloudFront with Origin Access Control (OAC) instead of making the bucket public.

---

# Step 4: Configure Bucket Policy

Go to:

```
Permissions
```

Open:

```
Bucket Policy
```

Paste the following policy and replace **YOUR-BUCKET-NAME** with your bucket name.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}
```

Click **Save Changes**.

This policy allows users to read objects from the bucket.

---

# Step 5: Enable Static Website Hosting

Open the bucket.

Navigate to:

```
Properties
```

Scroll to:

```
Static Website Hosting
```

Click **Edit**.

Choose:

```
Enable
```

Configuration:

```text
Hosting Type:
Host a Static Website

Index Document:
index.html

Error Document:
error.html
```

Save the configuration.

AWS generates a **Website Endpoint** similar to:

```text
http://brew-haven-static-website.s3-website-ap-south-1.amazonaws.com
```

---

# Step 6: Verify the Website

Copy the generated Website Endpoint.

Open it in a web browser.

If configured correctly, the website should load successfully.

Verify:

- Home page loads
- Images are displayed
- CSS styling works
- Navigation functions correctly

---

# Step 7: Enable Versioning

Open your bucket.

Navigate to:

```
Properties
```

Find:

```
Bucket Versioning
```

Click **Edit**.

Select:

```
Enable
```

Save the changes.

Versioning helps protect objects from accidental deletion or overwrite by maintaining multiple versions.

---

# Step 8: Test Versioning

Replace an existing file.

Example:

```
index.html
```

Upload the modified file.

Navigate to:

```
Objects
```

Enable:

```
Show Versions
```

You should see multiple versions of the uploaded object, each with a unique Version ID.

---

# Step 9: Create a Replica Bucket

Create another bucket.

Example:

```text
brew-haven-static-website-replica
```

Enable **Versioning** for the replica bucket as well.

Replication requires versioning to be enabled on both source and destination buckets.

---

# Step 10: Configure Replication

Open the source bucket.

Navigate to:

```
Management
```

Select:

```
Replication Rules
```

Click:

```
Create Replication Rule
```

Configure the following:

- Rule Name
- Entire Bucket (or specific prefix)
- Destination Bucket
- IAM Role (Create new or use existing)

Save the replication rule.

Amazon S3 will begin replicating eligible objects to the destination bucket.

---

# Step 11: Verify Replication

Open the replica bucket.

Confirm that the uploaded website files are present.

Example:

```text
index.html
style.css
hero.jpg
coffee1.jpg
coffee2.jpg
coffee3.jpg
coffee4.jpg
```

Replication is successful if the objects appear in the destination bucket.

---

# 📸 Screenshots

Include screenshots for each stage of the deployment.

Suggested order:

1. Architecture Diagram
2. Source Bucket
3. Live Website
4. Versioning Enabled
5. Replica Bucket
6. S3 Notes

---

# 🏗️ Architecture

```text
                User
                  │
                  ▼
              Internet
                  │
                  ▼
        Amazon S3 Source Bucket
                  │
                  ▼
       Static Website Hosting
                  │
                  ▼
         Brew Haven Website
                  │
                  ▼
        Amazon S3 Replication
                  │
                  ▼
      Replica S3 Bucket
```

---

# 🧪 Validation Checklist

- ✅ Bucket created
- ✅ Website files uploaded
- ✅ Block Public Access disabled
- ✅ Bucket Policy configured
- ✅ Static Website Hosting enabled
- ✅ Website accessible via endpoint
- ✅ Versioning enabled
- ✅ Replication configured
- ✅ Replica bucket contains copied objects

---

# ⚠️ Troubleshooting

### Access Denied

- Verify the bucket policy.
- Ensure Block Public Access is disabled.
- Confirm the object permissions are correct.

---

### Website Not Loading

- Check that `index.html` exists in the root of the bucket.
- Verify Static Website Hosting is enabled.
- Confirm the Website Endpoint is correct.

---

### Images Not Displaying

- Verify image file names and paths.
- Ensure the images were uploaded successfully.
- Check that the filenames in the HTML match the uploaded objects.

---

### Replication Not Working

- Ensure Versioning is enabled on both buckets.
- Verify the replication rule.
- Check the IAM role permissions.
- Allow a few minutes for replication to complete.

---

