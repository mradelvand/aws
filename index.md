# My Learning Blog 

Welcome to my personal documentation space — a collection of hands-on notes, architectural deep dives, and practical guides from my journey in **Cloud, DevOps, and Network Automation**.

---

##  Explore by Category

- [aws-architecture](archive.html#aws-architecture)
- [AWS Storage](archive.html#aws-storage)
- [AWS Networking](archive.html#aws-networking)
- [AWS Security](archive.html#aws-security)
- [AWS Cost Management](archive.html#aws-cost-management)
- [DevOps & Automation](archive.html#devops--automation)
- [AWS DevOps](archive.html#aws-devops)

> [📁 Blog Archive](archive.html).

---

##  Featured Learning Module
**[AWS Networking Overview](2025/10/20/aws-networking-overview.html)**  
An introductory guide to **Virtual Private Clouds (VPCs)** — covering subnets, routing, and how AWS isolates networking environments. Perfect for beginners transitioning into AWS or network automation.

---

###  About Me

Hi, I'm **Reza** — passionate about **Cloud + Network Automation (NetDevOps)**.  
This blog documents my continuous learning journey across AWS, DevOps, and Infrastructure Engineering.  
Expect practical notes, architectural insights, and publishable mini-projects built from real-world experience.

---

### ❤️ A Dedication

> **To my father**  
> Who recently passed away — my passion for technology and learning comes from him,  
> and this blog is a way to honor his influence and memory.

*In his memory, I keep learning — one post at a time.*
— *Reza*

---

##  Latest Posts

{% for post in site.posts limit:5 %}
- [{{ post.title }}]({{ post.url | relative_url }}) — *{{ post.date | date: "%B %Y" }}*
{% endfor %}

---
