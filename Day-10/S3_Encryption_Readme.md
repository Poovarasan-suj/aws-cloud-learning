
#  Day-10 — AWS Encryption & KMS (Cryptography Basics)

## 1️⃣ What is Encryption?

* Encryption means **converting readable data into unreadable format**
* Only an **authorized key** can convert it back to readable form (decryption)
* Purpose:

  * Protect data from hackers
  * Protect data if storage is compromised
  * Meet security & compliance requirements

---

## 2️⃣ Types of Encryption.

### 🔹 Encryption at Rest

* Data is encrypted **while stored**
* Example:

  * Data stored in S3
  * Data stored in EBS, RDS, DynamoDB
* If someone steals the disk or file → **they cannot read it**

### 🔹 Encryption in Transit

* Data is encrypted **while moving**
* Example:

  * Browser → S3 (HTTPS)
  * EC2 → S3
* Prevents network sniffing

 **Today’s topic is Encryption at Rest**

---

## 3️⃣ Server-Side Encryption (SSE) in S3

When you upload a file to S3:

* AWS encrypts it
* AWS decrypts it when you download
* You don’t manage encryption manually

### Types of SSE in S3

---

### 🔹 SSE-S3 (AWS-managed keys)

* Encryption keys fully managed by AWS
* You don’t see or control the key
* Easiest option

**Use when:**

* No strict compliance
* Simple workloads
* Default choice

---

### 🔹 SSE-KMS (AWS Key Management Service) ✅ (Industry Preferred)

* Encryption done using **KMS keys**
* AWS handles encryption, **you control the key**
* Key usage is logged in CloudTrail

**Use when:**

* Compliance required
* Audit required
* Fine-grained access control needed

---

### 🔹 SSE-C (Customer provided keys)

* You provide the key every time
* AWS does not store the key
* Rarely used (complex & risky)

---

## 4️⃣ AWS KMS (Key Management Service)

* Central service to create & manage encryption keys
* Used by:

  * S3
  * EBS
  * RDS
  * Lambda
  * Secrets Manager

---

## 5️⃣ Types of KMS Keys

### 🔹 AWS-Managed Keys (Example: `aws/s3`)

* Created automatically by AWS
* Cannot be deleted
* No fixed monthly cost
* Charged **only when used**

**Use when:**

* Simple encryption
* No need for custom control
* Cost-effective

---

### 🔹 Customer-Managed Keys (CMK)

* Created and owned by you
* You control:

  * Enable / Disable
  * Rotate
  * Key policy
  * Delete (schedule only)

**Cost:**

* Fixed monthly cost
* Charged even if unused

**Use when:**

* Compliance
* Strict access control
* Audit requirements

---

## 6️⃣ AWS-Managed vs Customer-Managed (Quick Difference)

| Feature        | AWS-Managed | Customer-Managed  |
| -------------- | ----------- | ----------------- |
| Key creation   | AWS         | You               |
| Delete key     | ❌ No        | ✅ Yes (scheduled) |
| Monthly cost   | ❌ No        | ✅ Yes             |
| Access control | Limited     | Full              |
| Compliance use | Basic       | Advanced          |

---

## 7️⃣ How Encryption Works in S3 (Real Flow)

1. User uploads file
2. S3 sends request to KMS
3. KMS encrypts data key
4. S3 stores encrypted object
5. On download → KMS decrypts key → data returned

👉 User always gets **plain readable file**, encryption is transparent

---

## 8️⃣ Client-Side Encryption (What I have  Practiced)

* I have  manually encrypted a file using AWS KMS CLI
* Encrypted file looked unreadable
* Decrypted only using same KMS key

**Use cases:**

* Extremely sensitive data
* Encrypt before upload
* Zero trust on storage layer

**Reality:**

* Used in limited, high-security systems
* Not common for daily S3 uploads

---

## 9️⃣ Enforcing Encryption using Bucket Policy 🔐

You enforced a rule:

* ❌ Upload fails if encryption is missing
* ✅ Upload succeeds only with SSE-KMS

**Why enforcement is used:**

* Prevent human mistakes
* Ensure every object is encrypted
* Mandatory in enterprise environments

---

## 🔟 Why Upload Failed Earlier (Important Learning)

* You enforced SSE-KMS
* Used a **disabled / deleting CMK**
* S3 could not encrypt → upload failed

**Fix:**

* Use active key
* Or use AWS-managed key (`aws/s3`)

---

## 1️⃣1️⃣ KMS Cost Understanding (Very Important)

### AWS-Managed Key

* No fixed cost
* Charged only per request
* Safe to keep

### Customer-Managed Key

* Monthly cost
* Must be deleted if unused
* Deletion = scheduled (cannot delete instantly)

---

## 1️⃣2️⃣ What i have Practiced Hands-On

* Created S3 bucket
* Enabled SSE-KMS
* Created customer-managed key
* Uploaded encrypted objects
* Enforced encryption via bucket policy
* Used AWS CLI to:

  * Encrypt file
  * Decrypt file
* Understood real upload failure reasons
* Cleaned up resources correctly

---

##  Final Takeaway (One-Line Memory)

> **Encryption protects data, KMS manages keys, SSE-KMS gives control, and bucket policies enforce security.**


