#  **Day-05 — EC2 EBS Volumes & Snapshots (Complete Summary)**

Today I learned and practiced the core concepts of **AWS Elastic Block Store (EBS)** — the block storage used by EC2 instances. This includes understanding volume types, performance metrics, snapshots, restore operations, and automation using Lifecycle Manager.

This day helped me build real Cloud Engineer skills, especially around storage, backups, and data recovery.

---

#  **1. What Are EBS Volumes?**

EBS (Elastic Block Store) provides **persistent block storage** for EC2 instances. It behaves like a hard disk for your server.

### Key Points:

* Data remains even after EC2 is stopped
* You can attach/detach volumes anytime
* Volumes are specific to an Availability Zone
* You can increase size anytime
* You can back up any volume using snapshots

**Real-time use:**
Applications, databases, logs, and OS files all run on EBS.

---

#  **2. Performance Terms — IOPS & Throughput (Simple Explanation)**

##  **IOPS (Input/Output Operations Per Second)**

* Measures **how many small read/write operations** a disk can perform in one second
* Important for **databases, web apps, login systems**, etc.
* High IOPS = faster response for small operations

### Example:

* 3000 IOPS → Can perform 3000 small read/write operations per second
* io2 volumes can reach very high IOPS (10,000+)

---

##  **Throughput (MB/s)**

* Measures how much **data per second** the disk can transfer
* Important for **big files**, analytics, logs, streaming

### Example:

* st1 HDD volumes provide high throughput, good for big data workloads

---

#  **3. Types of EBS Volumes (Simple Explanation)**

AWS offers different volume types depending on performance needs.

###  **1. gp3 — General Purpose SSD (Best Default)**

* Balanced IOPS + throughput
* Used for: web servers, app servers, boot volumes
* Most cost-efficient and recommended

---

###  **2. gp2 — Older SSD Type**

* Legacy version of gp3
* Only used for compatibility

---

###  **3. io1 / io2 — Provisioned IOPS SSD (High Performance)**

* Highest IOPS + low latency
* You can manually set IOPS
* Used for: MySQL, PostgreSQL, MongoDB, Oracle

**Best for databases and high-transaction systems.**

---

###  **4. st1 — Throughput Optimized HDD**

* High throughput, low IOPS
* Used for: big data, logs, analytics, streaming
* Not suitable for boot volumes

---

###  **5. sc1 — Cold HDD (Lowest Cost)**

* Used for rarely accessed data and archives
* Lowest performance

---

# 💾 **4. What Is an EBS Snapshot?**

A **snapshot is a point-in-time backup** of an EBS volume stored in S3.

### Why we take snapshots:

* Recover EC2 volume if data gets corrupted
* Backup before updates or changes
* Clone servers
* Move data to another AZ or region
* Disaster recovery

---

#  **5. How Snapshots Work (Incremental Backup)**

* **First snapshot = full backup** of entire volume
* **Next snapshots = only changed data blocks**
* Saves storage cost
* Faster backup

This is called **incremental snapshot**.

---

#  **6. How to Restore a Volume from Snapshot (Simple Steps)**

### ✔ Step 1: Create a snapshot

### ✔ Step 2: Go to Snapshots → Create Volume

### ✔ Step 3: Choose the same Availability Zone

### ✔ Step 4: Attach new volume to EC2

### ✔ Step 5: Mount it and access the restored data

**Important:**
The restored volume will contain **exactly the same data** as when the snapshot was taken.

---

#  **7. What I Practiced Today (Hands-On Tasks)**

### ✔ Created a 2GB EBS volume

### ✔ Mounted it on EC2

### ✔ Added real data (PDF files)

### ✔ Took a snapshot of the volume

### ✔ Deleted the original volume

### ✔ Restored a new volume from snapshot

### ✔ Attached restored volume and verified recovered data

### ✔ Reviewed Lifecycle Manager for automated snapshot policies

These are real Cloud Engineer tasks used in production for backup, restore, and data protection.

---

#  **8. AWS Lifecycle Manager (DLM)**

Lifecycle Manager automates:

* Snapshot scheduling
* Retention periods
* Automatic deletion of old snapshots

**Real-time use:**
Daily backups of production servers without manual effort.

---

#  **9. Cleanup**

To avoid charges, I cleaned up:

* Restored EBS volume
* Snapshot
* Temporary test data
* Confirmed no leftover resources

---

#  **Day-5 Summary **

* EBS volumes = block storage for EC2
* IOPS = number of read/write operations per second
* Throughput = amount of data transferred per second
* gp3 = balanced SSD
* io2 = high IOPS SSD for databases
* st1 = HDD for big data workloads
* Snapshots = backups stored in S3
* Snapshots are incremental
* You can restore volumes anytime
* Lifecycle Manager automates snapshot backups

This completes **Day-5** of my Cloud Engineer journey.

