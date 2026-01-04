
#  AWS VPC – Advanced Networking (Peering, Endpoint, Flow Logs, DNS)

This README explains **advanced VPC concepts** that are commonly used in **real projects**.
These topics are usually confusing for beginners, so this file explains them in a **simple and practical way**, based on **hands-on practice**.

---

## 1️⃣ VPC Peering

### What is VPC Peering?

**VPC Peering** allows **two VPCs to communicate privately** using **private IP addresses**.

* No internet is used
* No NAT Gateway is required
* Traffic stays inside AWS network

Think of it like **connecting two private networks using a private cable**.

---

### Why do we need VPC Peering?

* When applications are split across multiple VPCs
* When teams or environments (dev/prod) use different VPCs
* For secure, low-latency communication

---

### Important Rules of VPC Peering

* CIDR blocks **must NOT overlap**
* Routes must be added in **both VPCs**
* **No transitive routing**

  * If VPC-A ↔ VPC-B
  * VPC-A cannot reach VPC-C through VPC-B

---

### How VPC Peering Works (Practical Steps)

1. Create **two VPCs** with non-overlapping CIDR
2. Create a **VPC Peering connection**
3. Accept the peering request
4. Update **route tables** on both sides:

   * VPC-A route → VPC-B CIDR → Peering
   * VPC-B route → VPC-A CIDR → Peering
5. Update **Security Groups** to allow traffic from peer VPC CIDR
6. Test using `ping` or `ssh` via private IP

---

### What we tested

* Same-region and cross-region peering
* Ping between EC2 instances using private IP
* Verified no internet involvement

---

## 2️⃣ VPC Endpoint

### What is a VPC Endpoint?

A **VPC Endpoint** allows resources inside a VPC to access **AWS services privately**, **without**:

* Internet Gateway
* NAT Gateway
* Public IP

Traffic never leaves the AWS network.

---

### Why VPC Endpoint is important

* More secure
* Saves cost (no NAT)
* Required in private environments

---

### Types of VPC Endpoints

#### 🔹 Gateway Endpoint

* Used only for:

  * **S3**
  * **DynamoDB**
* Works via **route table**
* No ENI, no Security Group
* Free of cost

**Example use case:**
Private EC2 accessing S3 without internet

---

#### 🔹 Interface Endpoint

* Used for most AWS services:

  * EC2
  * SSM
  * CloudWatch
  * ECR
* Creates **Elastic Network Interface (ENI)**
* Uses **Security Groups**
* Has private IP
* Paid service

---

### How we practiced S3 Gateway Endpoint

1. Created EC2 instance
2. Installed AWS CLI
3. Verified S3 access via internet
4. Created **S3 Gateway Endpoint**
5. Attached endpoint to route table
6. Removed internet route
7. Verified `aws s3 ls` still works

✔️ This proved S3 access works **without internet**

---

## 3️⃣ VPC Flow Logs

### What are VPC Flow Logs?

**VPC Flow Logs capture network traffic metadata** for troubleshooting and monitoring.

They do NOT capture packet data, only metadata.

---

### What Flow Logs Capture

* Source IP
* Destination IP
* Source/Destination port
* Protocol
* ACCEPT or REJECT

---

### Levels of Flow Logs

* VPC level
* Subnet level
* ENI (instance) level

---

### Why Flow Logs are used

* Debug connectivity issues
* Identify blocked traffic
* Audit network behavior

---

### Important Behavior

* **Security Group rejects are NOT logged**
* **NACL rejects ARE logged**
* Metadata traffic (`169.254.169.254`) is NOT logged because it never leaves the instance

---

### What we practiced

* Enabled flow logs
* Sent logs to CloudWatch
* Generated traffic
* Verified ACCEPT and REJECT entries

---

## 4️⃣ DNS Inside VPC

### How DNS works inside a VPC

AWS provides **built-in DNS** for every VPC.

You do NOT need to create DNS records manually for:

* EC2 instances
* VPC Peering
* VPC Endpoints

---

### What AWS DNS does automatically

* Resolves public domains (google.com)
* Resolves private EC2 hostnames
* Resolves AWS service endpoints

---

### Important Points

* DNS resolution must be **enabled in VPC**
* Private DNS works automatically inside VPC
* Same works across VPC Peering

---

### What we learned

* DNS works internally without Route 53
* Private IP communication does not need extra DNS setup
* AWS manages DNS behind the scenes

---

## ✅ Final Outcome

After completing these labs, I have clearly understood:

* How private networking works in AWS
* How VPCs communicate securely
* How AWS services can be accessed without internet
* How to debug network traffic

---

## 🧹 Cleanup

All resources were cleaned up to avoid charges:

* EC2
* NAT Gateway
* Endpoints
* Peering
* Route tables
* Subnets
* VPCs

---

