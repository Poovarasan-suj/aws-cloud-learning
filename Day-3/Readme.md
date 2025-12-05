
# **Day 03 — IAM Advanced (Roles, Trust Policy, Permission Policy, STS, MFA)**

This document summarizes everything learned today from **basic → advanced**, with very simple explanations so I can quickly revise anytime.

---

#  1. **What Is a Role? (Simple Definition)**

An **IAM Role** is a **temporary identity** used by AWS services (like EC2, Lambda) to access other AWS resources.

### ✔ A role is NOT a user

### ✔ A role has NO password

### ✔ A role has NO access key

### ✔ A role receives **temporary credentials** through STS

Roles are used when AWS services need permissions without storing keys.

---

# ⭐ 2. **Why Roles Are Used (Real Meaning)**

### ✔ Secure → No long-term keys

### ✔ Automatic → AWS rotates temporary credentials

### ✔ Recommended in all companies

### ✔ Used for service-to-service access

Example:
“EC2 needs to access S3 bucket” → Attach IAM Role → EC2 gets permissions safely.

---

#  3. **Types of Policies Inside a Role**

A role contains **two types of policies**.
This is VERY important:

---

## 3.1 **Permission Policy (What the role can do)**

This policy tells AWS:

###  **What actions the role is allowed to perform**

Example:

* Read S3
* Write S3
* Start EC2
* Access DynamoDB

This is the permission part.

---

## 3.2 **Trust Policy (Who is allowed to use the role)**

This policy tells AWS:

###  **Which AWS service or account can assume this role**

Example trust policy for EC2:

```
"Principal": { "Service": "ec2.amazonaws.com" }
```

Meaning → Only EC2 instances can use this role.

### The difference is VERY important:

| Policy Type           | Meaning                           |
| --------------------- | --------------------------------- |
| **Permission Policy** | What the role is allowed to do    |
| **Trust Policy**      | Who is allowed to assume the role |

---

#  4. **STS (Security Token Service)**

STS is the AWS service that gives **temporary security credentials** to IAM Roles.

### STS provides 3 things:

* **AccessKeyId**
* **SecretAccessKey**
* **SessionToken**
* **Expiration Time** (keys expire automatically)

### STS = the engine behind IAM Roles

It refreshes credentials every few hours so you never need to store any access key on EC2.

---

#  5. **AssumeRole (Advanced but simple)**

When EC2 uses a role, it **assumes** the role using STS.

Example identity output:

```
arn:aws:sts::account-id:assumed-role/EC2-Advanced-S3-Role/i-xxxxxxxx
```

This means:

### ✔ EC2 is successfully using the role

### ✔ STS temporary credentials are active

### ✔ The IAM Role is working

This is the MOST important verification.

---

#  6. **MFA (Multi-Factor Authentication)**

MFA = extra layer of security for **human IAM users**.

### MFA needed for:

* Logging in to AWS Console
* Performing sensitive actions
* Protecting against password leaks

### MFA NOT used for:

* EC2
* Lambda
* IAM Roles
* Service access

Because these services use STS tokens, not passwords.

---

#  7. **Identity-Based vs Resource-Based Policies**

### ✔ Identity-Based Policies

Attached to:

* IAM Users
* IAM Groups
* IAM Roles

They define:

>> **What actions this identity can perform on AWS resources**

Example:
“Allow user to read S3 bucket.”

---

### ✔ Resource-Based Policies

Attached to:

* S3 bucket
* SQS
* SNS
* API Gateway

They define:

>> **Who is allowed to access this resource**

Example:
“This S3 bucket allows user A to GetObject.”

---

#  8. **Today’s Practical Tasks Completed**

### ✔ Created `EC2-Advanced-S3-Role`

### ✔ Attached permission policy (S3 access)

### ✔ Verified trust policy

### ✔ Attached role to EC2 instance

### ✔ Verified EC2 assumed the role using:

```
aws sts get-caller-identity
```

### ✔ Confirmed MFA for IAM user

### ✔ Completed identity-based vs resource-based explanation

---

#  9. **Super Simple Memory Summary**

* **Role = Temporary identity for AWS services**
* **Permission Policy = What the role can do**
* **Trust Policy = Who can use the role**
* **STS = Creates temporary keys for the role**
* **MFA = Extra security for IAM users, not EC2**
* **Identity-Based Policy = Permissions for users/roles**
* **Resource-Based Policy = Permissions set on resources (like S3)**

This is ALL you need to understand IAM at a strong beginner-to-intermediate level.



If you want, I can format this even more beautifully for GitHub (with tables, emojis, headings).
Just tell me **“Make it GitHub style”**.

When you're ready, I will prepare your **Day-03 LinkedIn post (short + professional)**.
