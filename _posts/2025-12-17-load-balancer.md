---
title: "Architectural Deep Dive: AWS Elastic Load Balancer (ELB) Overview "
date: 2025-12-17
categories: [AWS Architecture]
tags: [ELB, ALB, Quiz, High Availability, Scalability, Networking]
---

# Architectural Deep Dive: AWS Elastic Load Balancer (ELB) Overview


For any **AWS Solutions Architect Associate (SAA-C03)** candidate, understanding the **Elastic Load Balancer (ELB)** is essential.  
ELB is the backbone of **High Availability (HA)** and **scalability** in AWS architectures.

At its core, ELB ensures that traffic is distributed efficiently, securely, and reliably across your application infrastructure.

---

##  1. How ELB Works: The “Traffic Cop”

An Elastic Load Balancer acts as a **single entry point** for your application.  
Instead of users connecting directly to individual EC2 instances, they connect to the **ELB’s DNS name**.

### Key Behaviors

- **Round Robin Distribution**  
  Incoming requests are forwarded to healthy backend EC2 instances.

- **Abstraction Layer**  
  Users never see backend IP addresses — only the Load Balancer endpoint.

- **Horizontal Scalability**  
  As demand increases, ELB distributes traffic across all available instances.

---

##  2. Core Architecture & Features

ELB is considered a *“no-brainer”* in AWS because it provides critical functionality that would be complex and error-prone to manage manually.

### Built-In Capabilities

- **Health Checks**  
  ELB periodically checks instance health on a defined port or path (e.g., `TCP:80`, `/health`).  
  Unhealthy instances automatically stop receiving traffic.

- **SSL Termination**  
  ELB handles HTTPS decryption, offloading CPU-intensive work from EC2 instances.

- **Sticky Sessions (Session Affinity)**  
  Uses cookies to route a user to the same backend instance for the duration of a session  
  (useful for stateful applications like shopping carts).

- **High Availability by Design**  
  ELBs automatically distribute traffic across **multiple Availability Zones (AZs)**.

---

## 3. Security Group “Chaining” (Exam-Critical Concept)

To secure backend instances properly, **EC2 instances should only accept traffic from the Load Balancer** — not directly from the internet.

### Recommended Security Group Design

| Layer | Component | Protocol / Port | Source |
|------|-----------|-----------------|--------|
| **Public Tier** | Load Balancer SG | HTTPS (443) | `0.0.0.0/0` |
| **Private Tier** | EC2 Instance SG | HTTP (80) | **Load Balancer Security Group ID** |

> 💡 **Pro Tip (Exam Favorite):**  
> Always reference the **Security Group ID** of the Load Balancer — not IP ranges.  
> This ensures only traffic that passes through the ELB can reach your instances.

---

## 🧠 Knowledge Check: SAA-C03 Practice Quiz

### Question 1
**An application runs on multiple EC2 instances behind an ALB.  
Users lose session data (e.g., shopping cart items) when navigating between pages.  
Which feature should be enabled?**

- A) SSL Termination  
- B) Cross-Zone Load Balancing  
- C) Sticky Sessions (Session Affinity)  
- D) Connection Draining  

---

### Question 2
**How should an EC2 Security Group be configured so instances are accessible *only* through the ALB?**

- A) Allow port 80 from `0.0.0.0/0`  
- B) Allow port 80 from the VPC CIDR block  
- C) Allow port 80 from the Load Balancer’s Security Group ID  
- D) Allow port 443 from the Load Balancer’s public IP  

---

### Question 3
**A Load Balancer performs health checks on `/index.html`.  
An instance returns `404 Not Found`. What happens?**

- A) The instance is terminated  
- B) The instance is marked unhealthy and traffic stops  
- C) ELB searches for a new health check path  
- D) Traffic continues because a response was received  

---

### Question 4
**Why should SSL decryption be offloaded to the Elastic Load Balancer?**

- A) To encrypt traffic between the ELB and EC2 instances  
- B) To reduce CPU usage on backend EC2 instances  
- C) To allow packet inspection  
- D) To eliminate the need for Security Groups  

---

### Question 5
**You have a two-tier architecture:**
- Web servers in a public subnet  
- Database servers in a private subnet  

You want to load balance *internal traffic* between tiers.  
Which Load Balancer should you use?

- A) Internet-Facing Load Balancer  
- B) Internal Load Balancer  
- C) Classic Load Balancer  
- D) Gateway Load Balancer  

---

## ✅ Answer Key

1. **C** — Sticky Sessions preserve user state on the same backend instance  
2. **C** — Security Group referencing creates a secure traffic chain  
3. **B** — `404` is not a successful health check response  
4. **B** — SSL decryption is CPU-intensive and should be offloaded_+
5. **B** — Internal Load Balancers use private IPs within a VPC  

---

📌 **Final Tip:**  
If you understand **ELB behavior, security group chaining, and health checks**, you’ve covered a large portion of the **SAA-C03 networking and HA domain**.
