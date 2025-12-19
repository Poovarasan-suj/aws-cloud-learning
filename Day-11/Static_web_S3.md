# Day-11: S3 Static Website Hosting

##  Topic

**Static Website Hosting using Amazon S3**

Today focuses on hosting a simple static website using Amazon S3 without any server (EC2, backend, or database). The website serves static content like HTML pages directly from S3.

---

##  What I Learned

### 1️⃣ What is a Static Website?

* A static website contains fixed content (HTML, CSS, JS)
* No backend processing or database is required
* Same content is served to all users

Examples:

* Portfolio websites
* Blog pages
* Documentation sites

---

### 2️ Why Use S3 for Static Websites?

* Fully serverless (no EC2 / no OS management)
* Highly durable and available
* Cost-effective
* Scales automatically
* Easy to configure

---

### 3️ Minimum Requirements

| File       | Required    | Purpose               |
| ---------- | ----------- | --------------------- |
| index.html | ✅ Yes       | Default homepage      |
| error.html | ⚠️ Optional | Custom error page     |
| CSS / JS   | ❌ Optional  | Styling & interaction |

---

##  What I Practiced (Hands-on)

### Step 1: Create S3 Bucket

* Created a unique S3 bucket
* Disabled **Block Public Access**

---

### Step 2: Upload Website Files

* Uploaded `index.html`
* Uploaded `error.html`

---

### Step 3: Enable Static Website Hosting

Configured under **Bucket → Properties**:

* Enabled static website hosting
* Set:

  * Index document: `index.html`
  * Error document: `error.html`

---

### Step 4: Apply Bucket Policy (Public Read)

Used bucket policy to allow public access:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadForStaticWebsite",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::<bucket-name>/*"
    }
  ]
}
```

This allows anyone on the internet to **read website files only**.

---

### 5️Fixed 403 Forbidden Error

Initially faced **403 Access Denied** error.

🔍 Root cause:

* Static website hosting was enabled
* But public read permission was missing

✅ Fixed by:

* Disabling Block Public Access
* Applying correct bucket policy

---

### 6️⃣ Access Website

Accessed website using **S3 Website Endpoint** (not object URL):

```
http://<bucket-name>.s3-website-<region>.amazonaws.com
```

Website loaded successfully 🎉

---

##  Key Takeaways

* Static website hosting does NOT automatically make bucket public
* Public access must be explicitly granted via bucket policy
* Always use **S3 website endpoint**, not object URL
* S3 is ideal for static content, not backend apps

---
