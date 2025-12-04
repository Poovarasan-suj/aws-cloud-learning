
# **Day-02 — AWS IAM & AWS CLI**

This document contains everything learned on **Day-02** of the AWS Learning Tracker:
✔ IAM Basics
✔ IAM Users
✔ IAM Groups
✔ IAM Policies
✔ IAM Roles
✔ Trusted Entity
✔ AWS CLI Installation
✔ AWS CLI Testing from EC2

---

#  **1. What is IAM? (Identity and Access Management)**

IAM helps control **who** can access **what** in AWS.

IAM manages:

* Users
* Groups
* Policies
* Roles
* Permissions

IAM is required for every AWS service.

---

#  **2. IAM Users (Human Identity)**

IAM User = represents a real person.

A user has:

* Username
* Password (for AWS Console login)
* Access Key & Secret Key (for CLI login)

Example user created today:
`poovarasan-admin`

This user has **AdministratorAccess** to practice all AWS services safely (not using root).

---

# **3. IAM Groups (Collection of Users)**

A group is used to assign permissions to multiple users at once.

Groups created today:

| Group Name     | Permission          |
| -------------- | ------------------- |
| **Admins**     | AdministratorAccess |
| **Developers** | AmazonS3FullAccess  |
| **ReadOnly**   | ReadOnlyAccess      |

User `poovarasan-admin` was added to **Admins** group.

---

#  **4. IAM Policies (Permission Rules)**

A policy is a **JSON document** that defines:

* **Effect** → Allow or Deny
* **Action** → what the user/service can do
* **Resource** → on which AWS resource
* **Condition** → optional restrictions

Example simple policy structure:

```
{
  "Effect": "Allow",
  "Action": "s3:*",
  "Resource": "*"
}
```

Types of policies used today:

### ✔ AWS Managed Policies

(Provided by AWS — e.g., AdministratorAccess, S3FullAccess)

### ✔ Customer Managed Policies

(Custom policies created by you)

Example custom policy created today:
`S3CustomDeveloperPolicy`

---

#  **5. IAM Role (Temporary Permissions for Services)**

An IAM Role is not for humans — it is for **AWS services**, like:

* EC2
* Lambda
* ECS

A role has:

* **No password**
* **No access key**
* **Only permissions**

Today’s Role created:

```
EC2-S3-Role
```

This role allows EC2 to access S3 **without storing any access key**.

---

#  **6. What Is “Trusted Entity”?**

Trusted Entity means:

### 👉**Who is allowed to use (assume) this IAM role?**

Examples:

* AWS Service (EC2, Lambda, etc.)
* Another AWS Account
* Web Identity/SAML

Today’s trusted entity used:

```
AWS Service → EC2
```

This means **EC2 is trusted** to use this role.

---

# ⭐ **7. AWS CLI (Command Line Interface)**

AWS CLI lets you use AWS services from the terminal.

Examples:

```
aws s3 ls
aws iam list-users
aws sts get-caller-identity
```

---

#  **8. Local AWS CLI Setup**

Installed AWS CLI using:

```
aws --version
aws configure
```

Configured with:

* Access Key
* Secret Key
* Region → `ap-south-1`
* Output → `json`

---

#  **9. Install AWS CLI on EC2**

AWS CLI was installed using the official installer:

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip -y
unzip awscliv2.zip
sudo ./aws/install
```

Tested:

```
aws --version
```

---

#  **10. Test IAM Role From EC2**

To confirm EC2 is using the IAM Role:

```
aws sts get-caller-identity
```

Expected output:

```
assumed-role/EC2-S3-Role/i-xxxxxxxx
```

Test S3 access:

```
aws s3 ls
```

EC2 accessed S3 **without any access key**, proving IAM Role is working correctly.

---

# ⭐ **11. Day-02 Completed Items**

✔ IAM Overview
✔ Created IAM User
✔ Created IAM Groups
✔ Attached Managed Policies
✔ Created Custom Policy
✔ IAM Role for EC2
✔ Trusted Entity explanation
✔ EC2 key pair & SSH login
✔ AWS CLI setup (local & EC2)
✔ Tested EC2 → S3 access using IAM Role

---

#  **12. One-Line Revision (Quick Memory)**

* **IAM** → controls access
* **User** → humans account
* **Group** → multiple users
* **Policy** → allow/deny rules
* **Role** → temporary identity for EC2/Lambda
* **Trusted Entity** → who is allowed to use the role
* **AWS CLI** → manage AWS from terminal
* **EC2 IAM Role** → access AWS without access key



