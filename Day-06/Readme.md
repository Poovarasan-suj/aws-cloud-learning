
#  AWS DAY-06 — FULL SUMMARY ( ALB & EC2 Hands-On)**

Today, I have learned the **core real-time concepts** every Cloud Engineer must know.
We built a complete **Load Balanced Web Application** using:

* EC2 Instances
* Application Load Balancer (ALB)
* Target Groups
* Listener Rules
* Path-based Routing
* Health Checks
* Automatic Failover & Recovery

Let’s break everything down clearly.

---

# 1. What is a Load Balancer (LB)?

A **load balancer** is a service that distributes incoming traffic across multiple servers (EC2 instances).

### Why do we use it?

* Prevent servers from overload
* Provide high availability
* Automatically detect unhealthy servers
* Route traffic intelligently

---

# 2. What is ALB (Application Load Balancer)?

ALB is a **Layer 7 load balancer**.
It understands application-level data such as:

* URL paths ( /app1 , /api , etc.)
* Hostnames ( app.example.com )
* HTTP headers

It is used widely in **web applications, microservices, and APIs**.

---

# 3. What components does ALB use?

### ✔️ **Listeners**

* ALB listens on port 80 (HTTP) or 443 (HTTPS)
* This is the entry point for user requests

### ✔️ **Target Groups**

A target group contains backend servers (EC2 instances).
ALB forwards traffic to these targets.

### ✔️ **Health Checks**

ALB continuously checks if a server is healthy.

If unhealthy → ALB **stops sending traffic** to that server.

---

# 4. EC2 Setup You Performed

You launched **two EC2 instances**:

* Installed **Apache (httpd)**
* Configured `index.html`

  * Server 1 → “Server 1 – Poovarasan”
  * Server 2 → “Server 2 – Poovarasan”

This allowed us to clearly see which server ALB is sending traffic to.

---

# 5. Created a Target Group

You created a target group:

* Type → **Instances**
* Protocol → **HTTP**
* Port → **80**
* Registered both EC2 servers

Initially, status = **Unused**
ALB becomes attached later.

---

# 6. Security Group Setup (VERY IMPORTANT)

To make ALB work:

### ✔️ ALB Security Group

Inbound:

* HTTP 80 → **0.0.0.0/0**

This allows public traffic to reach load balancer.

### ✔️ EC2 Security Group

Inbound:

* HTTP 80 → **Source: ALB’s security group**

This allows **ALB → EC2** communication.

This is the MOST COMMON configuration mistake.
You fixed it perfectly today.

---

# 7. Creating the ALB

When creating ALB:

* Choose **internet-facing**
* Add **at least two subnets** (required by AWS)
* Attach security group
* Set Listener: **HTTP:80**
* Forward traffic to your **target group**

After creation, ALB DNS was:

```
alb-web-640467373.us-east-1.elb.amazonaws.com
```

---

# 8. DEMO: Round Robin Load Balancing

You tested:

* ALB request → Server 1
* Next request → Server 2
* Next → Server 1
* Next → Server 2

This is **Round Robin Algorithm**.

---

# 9. DEMO: Failover & Auto Recovery

This is REAL cloud engineering.

### What you did:

* Stopped Apache on Server 1
  (`sudo systemctl stop httpd`)

### What happened:

* Server 1 → **Unhealthy**
* ALB sent all traffic to **Server 2 only**

No downtime for users — perfect high availability.

### Auto Recovery

After restarting Apache:

* Server 1 became **Healthy again**
* ALB resumed balancing traffic equally

This is **self-healing infrastructure**.

---

# 10. Path-Based Routing (Microservices Style)

You created **two new target groups**:

* tg-app1 (Server 1)
* tg-app2 (Server 2)

Then created folders:

```
/app1/index.html
/app2/index.html
```

### Listener Rules Created:

Rule 1 → If path = `/app1/*` → forward to tg-app1
Rule 2 → If path = `/app2/*` → forward to tg-app2
Default Rule → forward to original group

### Test Results:

```
/app1/ → App 1 – Poovarasan
/app2/ → App 2 – Poovarasan
```

This is exactly how companies deploy multi-service apps.

---

# 11.What i have Learned About Listener Rules

### Listener rules decide:

* **Which target group** should receive the request
* Based on **path**, **host**, **headers**, etc

### Rule Priority:

* Lower number → evaluated first
* Default rule → last

This allows ALB to route traffic intelligently.

---

# 12. Why ALB Needed 2 Subnets?

Even if both EC2 were in same AZ, ALB requires **two subnets** (from two AZs) because:

* ALB nodes run in multiple AZs for **high availability**

EC2 does NOT need to be in both.
Only ALB nodes do.

---

# 13. Summary of FULL Architecture You Built Today

```
User → ALB Listener :80 
          ↓
     Listener Rules
          ↓
  ┌───────────────┬───────────────┐
  |  /app1/*      |   /app2/*     |
  v               v
tg-app1         tg-app2
  |               |
Server 1        Server 2
```

* Automatic health checks
* Automatic failover
* Automatic recovery
* Clean routing
* Secure SG configuration

#  FINAL WORD

I have understood:

* How ALB listens on ports
* How traffic flows to EC2
* Meaning of every setting
* Health checks
* Unhealthy → Healthy logic
* Path routing
* Listener rule priority
* Why SGs matter
* Why ALB needs 2 subnets

---
