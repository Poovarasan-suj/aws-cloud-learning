#  **Day-04 — Amazon EC2 Hands-On**

This document covers everything I practiced today with EC2 — from launching an instance to attaching storage and configuring a web server.
I also added **real-time explanations** so you understand *why* each step matters in real cloud environments.

---

#  **1. What is Amazon EC2?**

Amazon EC2 (Elastic Compute Cloud) is a virtual server in the cloud that we can use to run applications, deploy websites, host backend services, etc.

**Real-time example:**
Instead of buying physical servers for hosting a website, a company launches EC2 instances instantly with flexible hardware choices.

---

#  **2. Key EC2 Concepts**

## ✔ **AMI (Amazon Machine Image)**

The OS image used to launch the EC2 instance.
Examples: Amazon Linux, Ubuntu, Windows.

**Real-time use:**
Companies create **custom AMIs** with pre-installed software to launch identical servers easily.

---

## ✔ **Instance Type**

Defines the CPU, RAM, and network performance of the instance.
Examples: t2.micro, c5.large, r5.large.

**Real-time use:**

* t2.micro → free tier, testing
* c5 → CPU-heavy tasks
* r5 → database workloads

---

## ✔ **Key Pair**

A private key (.pem file) used to securely SSH into the EC2 instance.

**Real-time use:**
No passwords — only the key holder can access the server.

---

## ✔ **Security Group (Stateful Firewall)**

Controls inbound and outbound traffic to EC2.

**Why Stateful?**
If you allow inbound on a port (e.g., 80), the response outbound traffic is automatically allowed.

**Real-time use:**
Allows only specific traffic like HTTP (80), HTTPS (443), SSH (22).

---

## ✔ **Public vs Private IP**

* **Public IP** → Accessible from the internet
* **Private IP** → Used only inside AWS VPC

**Real-time use:**
App servers use private IP to talk to database servers securely inside the VPC.

---

## ✔ **Elastic IP (Static Public IP)**

A permanent IP that does NOT change when the instance stops or starts.

**Real-time use:**
Used for production websites, payment gateway callbacks, APIs, etc.

---

#  **3. Launching an EC2 Instance**

Steps I followed:

### 1️⃣ Choose AMI

→ Amazon Linux 2023 (lightweight & optimized for AWS)

### 2️⃣ Choose Instance Type

→ t2.micro (Free Tier)

### 3️⃣ Create Key Pair

→ Used for SSH authentication

### 4️⃣ Configure Security Group

Allowed:

* SSH (22) — My IP
* HTTP (80) — Anywhere

### 5️⃣ Launch Instance

Captured:

* **Public IP**
* **Private IP**
* **Instance ID**
* **Root EBS Volume (8GB)**

---

#  **4. Connecting to EC2 via SSH**

I connected using:

```
ssh -i mykey.pem ec2-user@<public-ip>
```

Verified instance details:

```
hostname
cat /etc/os-release
df -h
```

---

#  **5. Installing Apache Web Server**

Commands:

```
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

Created a webpage:

```
echo "Welcome, this is Poovarasan’s EC2 Web Server (Day-4)" | sudo tee /var/www/html/index.html
```

Website accessible at:

```
http://<public-ip>
```

---

#  **6. Security Group Test (Very Important)**

I removed HTTP (80) inbound rule and tested the website.

**Result:** Website failed
➡️ Confirms security group controls access

Added HTTP (80) rule again
➡️ Website worked

**Real-time use:** Useful for troubleshooting “site not reachable” issues.

---

#  **7. Working with EBS Volumes**

## ✔ Creating an Additional EBS Volume (3GB)

Steps:

* Created new 3GB volume
* Attached to EC2
* Formatted using EXT4
* Mounted to `/mnt/data`

Commands:

```
sudo mkfs.ext4 /dev/xvdf
sudo mkdir /mnt/data
sudo mount /dev/xvdf /mnt/data
df -h
```

**Real-time use:**
Extra volumes are used for:

* Application data
* Logs
* Database storage
* Scaling storage without stopping the server

---

#  **8. Elastic IP Test**

* Allocated Elastic IP
* Attached to EC2
* Verified website using Elastic IP
* Stopped → Started instance
* Verified that **Elastic IP remained same**

**Real-time use:**
Required for production servers that need consistent public IP.

Later → Released Elastic IP to avoid charges.

---

#  **9. Cleanup (Important to Avoid Charges)**

Checklist I followed:

* Released Elastic IP
* Terminated EC2 instance
* Deleted additional EBS volume
* Confirmed no snapshots
* Verified Free Tier usage



---

#  **Summary of What I Learned on Day-4**

* EC2 fundamentals
* How to launch and configure an instance
* Importance of AMI, instance type, key pair
* Security group behavior (stateful firewall)
* Apache server installation
* EBS storage operations
* Elastic IP usage and billing safety
* Safe cleanup using AWS best practices

---


