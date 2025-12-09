
# **AWS Day 07 – Application Load Balancer (Host-Based Routing)**

Today, I have  practiced **Host-Based Routing** using AWS Application Load Balancer (ALB).
This setup allows routing incoming traffic to different backend servers based on the **hostname** provided by the client.

---

## 🔹 **1. Created Two EC2 Web Servers**

* Launched **Web-Server-1** and **Web-Server-2**
* Installed Apache on both servers
* Updated HTML pages:

**Server 1 Output**

```
App 1 – Web Server
```

**Server 2 Output**

```
App 2 – Web Server
```

These two EC2 instances act as backend applications for ALB.

---

## 🔹 **2. Created Two Target Groups**

* **tg-app1** → Registered Web-Server-1
* **tg-app2** → Registered Web-Server-2
* Health checks configured and instances became **Healthy**

Target groups represent where ALB should forward traffic.

---

## 🔹 **3. Created Application Load Balancer (ALB)**

* Type: **Application Load Balancer**
* Scheme: **Internet-facing**
* Listener: **HTTP : 80**
* Selected two subnets (multi-AZ)
* Security Group: Allowed **HTTP (80)** from anywhere
* After ALB creation, noted down the **ALB DNS name**

---

## 🔹 **4. Configured Host-Based Routing Rules**

Added two custom listener rules under ALB → Listener → Port 80:

### **Rule 1 – For App1**

```
If Host = app1.mydemo.local
Forward to tg-app1
Priority: 1
```

### **Rule 2 – For App2**

```
If Host = app2.mydemo.local
Forward to tg-app2
Priority: 2
```

This allows ALB to intelligently route traffic based on hostname.

---

## 🔹 **5. Local DNS Override Using Windows Hosts File**

Since I do not own a domain, I used **local DNS mapping** to test host-based routing.

### ✔ Step 1 — Get ALB IPv4 Address

Used:

```
nslookup <ALB-DNS-Name>
```

This returned one or more IPv4 addresses.

### ✔ Step 2 — Update Hosts File

Edited:

```
C:\Windows\System32\drivers\etc\hosts
```

Added:

```
<ALB-IP>   app1.mydemo.local
<ALB-IP>   app2.mydemo.local
```

### ✔ Step 3 — Flushed DNS Cache

```
ipconfig /flushdns
```

This forces Windows to resolve the custom hostname to the ALB.

---

## 🔹 **6. Testing Host-Based Routing**

Opened browser:

### Test App1

```
http://app1.mydemo.local
```

Result → **App 1 – Web Server**

### Test App2

```
http://app2.mydemo.local
```

Result → **App 2 – Web Server**

Both routes successfully forwarded to the correct backend instances.

---

#  **Key Learnings Today**

* ALB is a **Layer 7 (Application Layer)** load balancer
* Host-based routing uses **Host header** to decide routing
* Target groups define backend servers
* Health checks automatically remove unhealthy servers
* We can test routing locally using the **hosts file**
* ALB has multiple IPs; any of them must be used for host mapping
* Real domain is NOT required for learning host-based routing

---

