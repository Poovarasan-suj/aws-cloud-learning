
#  AWS VPC – Complete Basics (Day 12)

This document summarizes my hands-on learning and understanding of **AWS Virtual Private Cloud (VPC)**, including **CIDR, subnets, routing, Internet Gateway, NAT Gateway, and Bastion Host**.

---

##  What is a VPC?

A **VPC (Virtual Private Cloud)** is a **logically isolated network** in AWS where we can launch resources such as EC2 instances.

* We control:

  * IP address range
  * Subnets
  * Routing
  * Internet access
  * Security

A VPC works like a **virtual data center** in the cloud.

---

## CIDR Basics (Very Important)

### What is CIDR?

**CIDR (Classless Inter-Domain Routing)** defines a **range of IP addresses**.

Example:

```
10.0.0.0/16
```

* `/16` → network size
* Total IPs = **65,536**
* CIDR is used at:

  * VPC level
  * Subnet level

CIDR helps in:

* IP allocation
* Subnetting
* Network planning

---

##  Subnets

A **subnet** is a **smaller network created from a VPC CIDR**.

Example:

* VPC CIDR: `10.0.0.0/16`
* Subnets:

  * `10.0.1.0/24` (Public Subnet)
  * `10.0.2.0/24` (Private Subnet)

### Key rules:

* One subnet belongs to **one Availability Zone**
* Subnets divide the VPC CIDR
* Subnets themselves are not public or private — **route tables decide that**

---

##  Public vs Private Subnet

### Public Subnet

A subnet is **public** if:

* Its **route table** has:

  ```
  0.0.0.0/0 → Internet Gateway (IGW)
  ```

* EC2 instances can have:

  * Public IP
  * Internet access

---

### Private Subnet

A subnet is **private** if:

* Its route table **does NOT** point to IGW

* EC2 instances:

  * Have only private IP
  * Cannot be accessed directly from the internet

---

##  Internet Gateway (IGW)

* IGW is attached to the **VPC**, not the subnet
* It enables **internet connectivity**
* Used only by **public subnets** via route tables

---

##  Route Tables

Route tables control **where network traffic goes**.

### Public Route Table

```
Destination: 0.0.0.0/0
Target: Internet Gateway
```

Attached to **public subnet**

---

### Private Route Table

* No IGW route
* Later updated with NAT Gateway for outbound internet

Attached to **private subnet**

---

##  Bastion Host

A **Bastion Host** is an EC2 instance placed in a **public subnet**.

Purpose:

* Securely access EC2 instances in **private subnets**

How it works:

* Bastion has a public IP
* Private EC2 has only private IP
* Both are in the **same VPC**
* Access happens using **private IP communication**

---

##  NAT Gateway

A **NAT Gateway** allows **private EC2 instances to access the internet**, without exposing them to inbound traffic.

### Key points:

* NAT Gateway is placed in a **public subnet**
* It uses an **Elastic IP**
* Private route table is updated:

  ```
  0.0.0.0/0 → NAT Gateway
  ```

### Result:

* Private EC2:

  * Can access internet (outbound)
  * Cannot be accessed from internet (inbound blocked)

---

##  Traffic Flow Summary

### Public EC2

```
EC2 → Route Table → IGW → Internet
```

### Private EC2 (with NAT)

```
Private EC2 → Private Route Table → NAT Gateway → IGW → Internet
```

---

##  Hands-On Validation Performed

✔️ SSH to Bastion from laptop
✔️ SSH from Bastion to Private EC2
✔️ Private EC2 blocked internet before NAT
✔️ Private EC2 internet access works after NAT
✔️ Cleanup done to avoid charges

---

## 🎯 Key Takeaways

* CIDR defines IP range
* Subnets divide CIDR
* Route tables decide public/private behavior
* IGW enables internet access
* NAT Gateway enables **outbound-only** internet
* Bastion host enables secure admin access
* Proper cleanup is essential to avoid billing

---


