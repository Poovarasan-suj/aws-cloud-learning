# AWS RDS – Hands-On Learning Summary

## 1. What is Amazon RDS

Amazon RDS is a **managed relational database service**.

What AWS manages:

* OS
* MySQL installation
* Patching
* Backups
* Monitoring
* Failover (if enabled)

What **I** manage:

* Database
* Schema
* Users
* Queries
* Connectivity & security

👉 RDS = MySQL without OS headache.

---

## 2. RDS vs MySQL on EC2 (Practical Difference)

| MySQL on EC2                | RDS               |
| --------------------------- | ----------------- |
| Full OS access              | No OS access      |
| Manual backup (`mysqldump`) | Automated backups |
| Manual restore              | Snapshot restore  |
| Manual HA                   | Multi-AZ          |
| IP-based access             | DNS endpoint      |

---

## 3. Key RDS Components (Must Remember)

* **DB Instance** → Running database
* **DB Engine** → MySQL
* **Endpoint** → DNS name to connect
* **Port** → 3306
* **Security Group** → Controls access
* **Subnet Group** → Where DB runs
* **Storage** → AWS-managed EBS

---

## 4. Endpoint (Very Important Concept)

* RDS gives a **DNS endpoint**, not an IP
* Underlying instance can change
* Endpoint remains the same

👉 This enables:

* Restore
* Failover
* Maintenance
* High availability

---

## 5. Backups in RDS (Clear Difference)

### Automated Backups

* Enabled by default
* Retention: 1–35 days
* Used for **point-in-time recovery**
* Deleted when DB is deleted

### Manual Snapshots

* Created by user
* Stored until user deletes
* Used for:

  * Cloning DB
  * Disaster recovery
  * Cross-region copy
* Survives DB deletion

**Rule**

> System snapshot = AWS-managed
> Manual snapshot = User-managed

---

## 6. Snapshot Restore (What I Practiced)

Steps:

1. Create RDS MySQL
2. Take manual snapshot
3. Restore new DB from snapshot
4. New DB gets:

   * Same data
   * New endpoint
   * Independent lifecycle

👉 Snapshot = **Time machine**

---

## 7. Multi-AZ (Conceptual Understanding)

* One **Primary DB**
* One **Standby DB** in another AZ
* Synchronous replication
* Automatic failover
* Same endpoint

Used for:

* High availability
* Production workloads

Not used for:

* Read scaling
* Cost-sensitive dev environments

👉 Multi-AZ costs more → enabled only when needed.

---

## 8. Security & Networking

* RDS runs inside a **VPC**
* Access controlled by **Security Groups**
* Publicly accessible ≠ Open to internet
* Best practice:

  * Private RDS
  * EC2 inside VPC connects to it

---

## 9. Real Engineer Cost Discipline

After lab:

* Deleted DB instances
* Avoided unnecessary paid features
* Understood cost vs benefit

👉 Cost awareness is part of cloud engineering.

---

## 10. What I Can Confidently Do Now

* Create RDS MySQL
* Connect securely using endpoint
* Understand backups & snapshots
* Restore DB from snapshot
* Decide when to use Multi-AZ
* Clean up resources safely

---

## Final One-Line Understanding

> **RDS is not about SQL — it’s about managed availability, backup, and reliability.**


