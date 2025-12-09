# Day 1 – AWS Fundamentals

##  Overview
Today marks the beginning of my AWS Cloud Journey.  
I focused on understanding the core foundation of cloud computing and set up my AWS account safely for hands-on learning.

This document contains all the important concepts I learned today, explained in simple language for future revision.

---

#  1. What is Cloud Computing?

Cloud computing means renting IT resources (servers, storage, databases, networking, security tools) from cloud providers like AWS **over the internet** instead of buying your own hardware.

### 🔹 Key Benefits:
- No upfront hardware cost  
- Pay only for what you use  
- Scale instantly (up/down)  
- High availability  
- Global access  
- Very fast deployment  
- Highly secure  

---

#  2. Types of Cloud Deployment

 1. Public Cloud
    
✔ What it actually means:

The cloud infrastructure is owned and managed by a cloud provider like AWS, Azure, or Google Cloud.

Anyone (any company or individual) can create an account and use the services.

Resources like EC2, S3, RDS are shared across many customers, but securely isolated using virtualization.

✔ Key Points

Accessible via the internet, but NOT publicly visible to everyone. Only you can access your resources.

Highly scalable → servers can be added or removed easily.

Cost-effective → pay only for what you use.

No maintenance → AWS manages hardware, networking, security of the cloud.

🔥 Example:

Your AWS account with EC2, S3, and RDS → Public Cloud.

 2. Private Cloud
✔ What it means:

Cloud infrastructure is owned and used by one single organization.

Can be located on-premises (company data center) or hosted by a private provider.

The organization has full control over hardware, security, and networking.

✔ When companies use it?

When they need high security, compliance (like banks, hospitals, government).

When they don't want data to run on shared public infrastructure.

 Example:

A bank running its own OpenStack cloud only for internal employees → Private Cloud.

 3. Hybrid Cloud
✔ What it means:

Combination of Public + Private Cloud working together.

Applications, data, and workloads can move between the two.

✔ Why companies use this?

They want flexibility.

Sensitive data → kept in private cloud.

Less-sensitive or high-traffic workloads → run in public cloud (AWS).

🔥 Example:

A hospital keeps patient data in a private cloud (security).

It uses AWS EC2 for analytics reports (scalability).
This is Hybrid Cloud.
---

#  3. Cloud Service Models (IaaS, PaaS, SaaS)

### **1️⃣ SaaS – Software as a Service**
You use the software directly.  
No servers, no installation.

Examples: Gmail, Zoom, Netflix

### **2️⃣ PaaS – Platform as a Service**
Cloud provides the platform, you deploy code.  
No OS or server management.

Examples:
- AWS Elastic Beanstalk
- Google App Engine

### **3️⃣ IaaS – Infrastructure as a Service**
You get full control of the server (OS, network, storage).

Examples:
- EC2 (compute)
- VPC (network)
- S3 (storage)

---

# 🌎 4. AWS Global Infrastructure

AWS infrastructure is based on three major components:

### ** Regions**
A geographic location where AWS has multiple data centers.

Examples:
- ap-south-1 (Mumbai)
- us-east-1 (Virginia)
- eu-west-1 (Ireland)

### **2️⃣ Availability Zones (AZs)**
Physically separate data centers inside a region.

Example:
- ap-south-1a  
- ap-south-1b  
- ap-south-1c  

If one AZ fails, others still work → high availability.

### ** Edge Locations**
Used mainly by Amazon CloudFront to deliver content faster.

Example:  
A user in Chennai gets cached content from the nearest Edge Location, reducing latency.

---

#  5. AWS Shared Responsibility Model

AWS and the customer share responsibility for security.

## 🔹 **AWS is responsible for:**
- Physical security  
- Hardware  
- Networking  
- Data center security  
- Power, cooling, servers  
- Hypervisors  

This is called **Security *of* the Cloud**.

## 🔹 **Customer is responsible for:**
- OS patches  
- Applications  
- IAM users  
- Access management  
- Security groups  
- Data encryption (optional)  

This is called **Security *in* the Cloud**.

---

#  6. AWS Billing Protection Setup

Before doing ANY hands-on, it's important to protect your AWS account from accidental charges.

### ✔️ Steps I completed today:
1. Enabled **Free Tier Usage Alerts**
2. Enabled **CloudWatch Billing Alerts**
3. Created a **Monthly AWS Budget**  
   - Budget amount: **₹200**  
   - Alert at: **80% of budget**  
4. Added my email for notifications

### ✔️ Why this is important?
- Prevents unexpected costs  
- Ensures learning stays within free-tier  
- Helps track monthly usage  
- Alerts you before crossing limits  

---

#  7. AWS Console Exploration
Today, I explored the AWS Console UI and got familiar with the layout of:

- EC2 (virtual servers)  
- S3 (object storage)  
- IAM (identity management)  
- VPC (networking)  
- RDS (managed databases)

No resources were created today — only interface exploration.

---

#  Summary of Day 1
**Concepts Learned:**
- Cloud computing basics  
- Types of cloud deployment  
- SaaS, PaaS, IaaS  
- Regions, AZs, Edge Locations  
- Shared Responsibility Model  

**Hands-on Completed:**
- Enabled free tier alerts  
- Enabled CloudWatch billing alerts  
- Created ₹200 monthly budget  
- Explored EC2, S3, IAM, VPC, RDS dashboard  

---

