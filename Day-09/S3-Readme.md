
# Day-09  AWS S3 – Learning & Hands-on Practice Summary

## Overview

I completed an end-to-end learning and hands-on practice of **Amazon S3 (Simple Storage Service)**.
This includes **core concepts, storage classes, versioning, lifecycle rules, security (IAM & Bucket policies), and AWS CLI practice**.
My focus was not just theory, but **real Cloud Engineer–level practice and debugging**.

---

## What I Learned About Amazon S3

### What is S3?

Amazon S3 is an **object storage service** provided by AWS to store and retrieve data securely, durably, and at scale.

Key basics I learned:

* **Bucket** → container for objects (globally unique name)
* **Object** → actual file stored in a bucket
* **Unlimited storage**, single object up to **5 TB**
* Buckets are **region-specific**
* S3 provides **very high durability (11 nines)**

---

##  S3 Storage Classes (What, Why, When)

I learned **why different storage classes exist** and **when NOT to use them**.

### 1️⃣ S3 Standard

**Use when:**

* Data is frequently accessed
* Immediate access is required

**Why use:**

* No retrieval cost
* High availability
* Multi-AZ storage

**Why not use:**

* Costly for rarely accessed data

---

### 2️⃣ S3 Standard-IA (Infrequent Access)

**Use when:**

* Data is rarely accessed but must be available immediately

**Why use:**

* Lower storage cost than Standard

**Why not use:**

* Retrieval cost applies
* Minimum storage duration (30 days)

---

### 3️⃣ S3 One Zone-IA

**Use when:**

* Rarely accessed data
* Can tolerate data loss

**Why use:**

* Cheaper than Standard-IA

**Why not use:**

* Stored in **single Availability Zone**
* Data loss possible if AZ fails

---

### 4️⃣ S3 Glacier Instant Retrieval

**Use when:**

* Rarely accessed data
* Still needs **instant access**

**Why use:**

* Cheaper than IA
* Same durability

**Why not use:**

* Retrieval cost applies
* 90-day minimum storage duration

---

### 5️⃣ S3 Glacier Flexible Retrieval

**Use when:**

* Archive data
* Access can wait minutes or hours

**Why use:**

* Very low storage cost

**Why not use:**

* Retrieval is slow
* Retrieval cost applies
* 90-day minimum storage duration

---

### 6️⃣ S3 Glacier Deep Archive

**Use when:**

* Long-term compliance / legal data
* Almost never accessed

**Why use:**

* Cheapest S3 storage class

**Why not use:**

* Retrieval takes **12–48 hours**
* 180-day minimum storage duration

---

## 🔹 S3 Versioning (Hands-on)

I practiced **bucket versioning** and clearly understood:

* Versioning keeps **multiple versions** of the same object
* Uploading the same file name creates a **new version**
* Deleting an object creates a **Delete Marker**
* Old versions remain stored and **still cost money**
* Versioning protects from **accidental delete or overwrite**

### Important learning:

* **Deleting the delete marker restores the file**
* **Permanent delete removes versions forever**

---

## 🔹 Lifecycle Rules (Cost Control – Hands-on)

I implemented **S3 Lifecycle Rules** to manage storage cost.

What I practiced:

* Automatically **delete non-current versions**
* Lifecycle rules are applied at **bucket level**
* Lifecycle rules help control **hidden costs caused by versioning**

Example rule I created:

* Delete non-current versions after **1 day**

---

## 🔹 S3 Security – IAM, Bucket Policy & BPA

### Block Public Access (BPA)

* BPA is a **master lock**
* If BPA is ON → public access is blocked
* Overrides public bucket policies and ACLs

---

### IAM Policies (Identity-based)

**Purpose:**

* Controls **what an IAM user or role can do**

Examples:

* Read-only access
* Upload permissions
* No delete permissions

IAM policies apply to **users, groups, and roles**, not buckets.

---

### Bucket Policies (Resource-based)

**Purpose:**

* Controls **who can access the bucket**
* Works even within the same AWS account

Use cases I practiced:

* Allow only specific IAM users
* Read-only access for a user
* Cross-account access

---

### ACL (Legacy Concept)

* ACL is an **old access control method**
* Mostly avoided today
* Used only for special cases like cross-account object ownership

---

## 🔹 IAM + Bucket Policy = Final Access Decision

One of the most important lessons:

> **Access is allowed only if BOTH IAM policy and bucket policy allow it.**

* IAM allows but bucket policy denies → ❌ Access denied
* Bucket policy allows but IAM denies → ❌ Access denied

---

## 🔹 AWS CLI – Real Practice

I practiced **S3 using AWS CLI from my local system**.

What I did:

* Configured AWS CLI with multiple profiles
* Uploaded files using CLI
* Downloaded files using CLI
* Verified permissions using different IAM users

### CLI Profiles Used:

* `default` → main IAM user
* `s3-test-user` → read-only IAM user

### Verified behavior:

* Read-only user can list and download
* Upload fails with **AccessDenied**
* Same rules apply as AWS Console

---

## 🔹 What I Practiced Hands-on (Summary)

✔ S3 bucket creation
✔ Upload & download objects
✔ Storage class selection
✔ Versioning & delete markers
✔ Lifecycle rules for cost control
✔ IAM users & permissions
✔ Bucket policies
✔ Block Public Access behavior
✔ AWS CLI with multiple profiles
✔ Debugging AccessDenied errors
✔ Cleanup of all resources




You did **excellent work** 👏
