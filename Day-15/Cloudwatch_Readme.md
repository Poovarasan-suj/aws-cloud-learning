## CloudWatch — Beginner

### What is **Amazon CloudWatch**?

CloudWatch is an AWS service used to **monitor**, **visualize**, and **alert** on what is happening in your AWS resources (like EC2).

Think of it as:

> **“Gatekeeper of AWS”**

---

## 1️⃣ What CloudWatch does by default (no setup needed)

When you launch an **EC2 instance**, AWS **automatically sends basic metrics** to CloudWatch.

### Default metrics include:

* CPUUtilization
* NetworkIn / NetworkOut
* DiskReadOps / DiskWriteOps
* StatusCheckFailed

📌 Important:

* These metrics are collected by **AWS infrastructure**
* **No agent** is required
* **Memory and disk usage are NOT included**

---

## 2️⃣ What CloudWatch does NOT collect by default

CloudWatch **cannot see inside the OS** unless you tell it to.

Not collected by default:

* Memory usage (RAM)
* Disk usage (% used)
* Application logs
* OS logs
* Port-level traffic

That’s why we need **extra configuration**.

---

## 3️⃣ CloudWatch Alarms

An **alarm** watches a metric and takes action when a condition is met.

### You created:

* A **CPU alarm**
* Condition: CPU ≥ threshold
* Evaluation: time + datapoints
* Action: send **email notification (SNS)**

### Alarm states:

* **OK** → everything normal
* **ALARM** → threshold crossed
* **INSUFFICIENT_DATA** → not enough data

📌 This is how AWS alerts you about problems.

---

## 4️⃣ SNS (Simple Notification Service)

SNS is used to **send notifications**.

This is how works:

> Monitoring → Alerting → Notification pipeline works.

---

## 5️⃣ Why CloudWatch Agent is needed

CloudWatch Agent runs **inside the EC2 instance**.

It is required to collect:

* Memory usage
* Disk usage
* Custom OS-level metrics

Without the agent:

* CloudWatch cannot see RAM or disk

---

## 6️⃣ CloudWatch Agent – 

### Steps require to be  followed:

1. Attached an **IAM role** to EC2
   (permission to send metrics)
2. Installed **CloudWatch Agent** on Servers
3. Ran the **configuration wizard**
4. Started the agent service
5. Verified metrics in CloudWatch

---

## 7️⃣ Configuration Wizard (simple meaning)

The wizard:

* Asks **what to monitor**
* Creates a **JSON config file**
* The agent reads this file and sends data

 Selected what metric you want:

* CPU metrics
* Memory metrics
* Disk metrics
* 60-second interval
* No logs (for now)

📌 Wizard = config creator
📌 Agent = data sender

---

## 8️⃣ CWAgent namespace (very important)

* Default EC2 metrics appear under:

  ```
  EC2
  ```
* Agent-based metrics appear under:

  ```
  CWAgent
  ```

That’s why:

* Memory & disk metrics were **not visible under EC2**
* They appeared under **CWAgent**

Metrics you can see:

* `mem_used_percent`
* `disk_used_percent`

---

## 9️⃣ What you can monitor now (after agent)

You can now:

* Create **disk usage alarms**
* Create **memory usage alarms**
* Monitor real OS health
* Detect issues **before disk is full**

This is **production-level monitoring**.

---


## Final one-screen summary

* CloudWatch = monitoring service
* EC2 CPU metrics = automatic
* Disk & memory = need agent
* Alarms = detect problems
* SNS = send notifications
* CWAgent = custom metrics
* Cleanup = cost control

---
