# **AWS Day 08 – Auto Scaling with ALB (My Complete Learning)**

Today, I worked on one of the most important topics in AWS Cloud Engineering:
**Auto Scaling Groups (ASG) with Application Load Balancer (ALB)**.

I practiced everything end-to-end and understood how AWS maintains scalability, availability, and fault tolerance automatically.
Below are my complete notes written from my perspective.

---

#  **What I Understood About Auto Scaling**

Auto Scaling automatically increases or decreases the number of EC2 instances based on demand.

It handles three things:

### ✔ **Scale-Out**

When traffic or CPU load increases, Auto Scaling automatically launches new EC2 instances.

### ✔ **Scale-In**

When traffic or CPU load decreases, Auto Scaling automatically removes extra EC2 instances.

### ✔ **Self-Healing**

If an instance becomes unhealthy, ASG replaces it with a new one.

This gives:

* Better performance
* High availability
* Lower cost

---

#  **Stateful vs Stateless Applications (My Understanding)**

Before doing Auto Scaling, I learned an important concept:

### **Stateful Application**

* Stores data inside the EC2 instance
* If EC2 terminates, data is lost
* Not suitable for Auto Scaling

### **Stateless Application**

* Does NOT store data inside EC2
* Stores data in external systems (S3, RDS, DynamoDB, EFS)
* Any instance can be added or removed
* Perfect for Auto Scaling

This concept helped me understand why Auto Scaling requires stateless architecture.

---

# ⭐ **Architecture I Practiced (ASG + ALB)**

```
                 ┌──────────────────────────┐
                 │  Application Load Balancer│
                 └──────────────┬───────────┘
                                │
                     ┌──────────┴───────────┐
                     │     Target Group      │
                     └──────────┬───────────┘
                                │
                ┌──────────────┴───────────────┐
                │     Auto Scaling Group (ASG)  │
                │                                │
       ┌────────┴────────┐             ┌────────┴────────┐
       │   EC2 Instance 1 │             │   EC2 Instance 2 │
       └──────────────────┘             └──────────────────┘
```

What happens here:

* ALB receives all the traffic
* ALB forwards traffic to Target Group
* ASG launches EC2 instances and registers them automatically
* ALB sends traffic only to healthy instances
* ASG maintains performance by scaling in and out

---

#  **Step-By-Step Work I Did Today**

## **1️⃣ Launch Template**

I created a Launch Template that included:

* AMI
* Instance type
* Security group
* User Data to install Apache and show hostname

So whenever ASG launches a new instance, it automatically becomes a working web server.

---

## **2️⃣ Target Group**

I created a Target Group with:

* Target type: Instances
* Port: 80
* Health check: `/`

This allowed ALB to check if instances are healthy.

---

## **3️⃣ Application Load Balancer (ALB)**

I created an ALB with:

* Public subnets
* HTTP listener on port 80
* Forwarding to the Target Group

ALB gives a DNS URL which I used to test my website.

---

## **4️⃣ Auto Scaling Group (ASG)**

I created an ASG with:

* Minimum: 1
* Desired: 1
* Maximum: 3
* Public subnets
* Attached Target Group
* Enabled ELB health checks

Then I added a **Target Tracking Scaling Policy**:

```
Average CPU Utilization = 50%
Scale out if CPU > 50%
Scale in if CPU < 50%
```

---

#  **Scale-Out Test (My Practical Test)**

I connected to the EC2 instance using SSH and generated CPU load:

```bash
yes > /dev/null
```

or

```bash
stress --cpu 4
```

What happened:

✔ CPU reached 100%
✔ CloudWatch detected high CPU
✔ ASG automatically launched new EC2 instances
✔ Target Group registered the new instances
✔ ALB started load balancing traffic
✔ When I refreshed the ALB DNS, I saw different instance hostnames

This confirmed that **Auto Scaling Scale-Out is working perfectly.**

---

#  **Scale-In Test (My Practical Test)**

After stopping the stress command:

```
CTRL + C
```

CPU dropped.

Then:

✔ ASG waited for warm-up and cooldown
✔ ASG automatically terminated extra EC2 instances
✔ Returned to only 1 running instance

This confirmed that **Scale-In also works correctly.**

---



#  **My Day 08 Summary**

### Today I learned:

✔ What Auto Scaling is
✔ How ASG + ALB work together
✔ Why stateless architecture is required
✔ How Launch Template works
✔ How Target Group + ALB health checks work
✔ How to create Auto Scaling Group
✔ How to configure scaling policies
✔ How scaling actually happens in real time
✔ How to test scale-out with CPU load
✔ How to test scale-in
✔ How to observe ALB balancing requests
✔ How to clean up AWS resources

I now clearly understand how AWS handles **scalability, elasticity, and fault-tolerance** in production environments.
