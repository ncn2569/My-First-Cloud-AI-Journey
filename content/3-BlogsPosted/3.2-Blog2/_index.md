---
title: "Blog 2"
date: 2026-07-10
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# SECURITY IN SOFTWARE DEVELOPMENT — IT'S NOT JUST ABOUT WRITING SECURE CODE

### 1. Introduction

While learning AWS, our group noticed something quite interesting. When starting a project, most of us focus solely on **"how to make the application run."** But once the application goes online, a far more important question emerges: **how to keep the application secure?**

An application can run flawlessly in terms of functionality, yet a single misconfiguration or a small vulnerability can expose data or compromise the entire system at any moment. AWS provides not just the infrastructure to deploy applications, but an entire suite of services to build a security architecture from the ground up — not just patch holes after an incident occurs.

---

### 2. Five Critical Security Lessons on AWS

#### 2.1. Never Store Access Keys in Source Code

This is a mistake that many cloud newcomers have made. A typical example:

```
AWS_ACCESS_KEY="AKIAxxxxxxxx"
AWS_SECRET_KEY="xxxxxxxxxxxxxxxx"
```

Then the entire project gets accidentally pushed to GitHub. If the repo is public, anyone can grab this key pair and use your AWS resources immediately. In reality, there have been numerous cases of compromised accounts being exploited for cryptocurrency mining or spinning up hundreds of EC2 instances simultaneously, generating massive bills within just a few hours.

Instead of hardcoding Access Keys directly into source code, AWS recommends using:

- **IAM Roles**
- **Environment Variables**
- **AWS Secrets Manager**
- **AWS Systems Manager Parameter Store**

These are all approaches that reduce the risk of credential leakage compared to hardcoding.

#### 2.2. The Principle of Least Privilege

A concept our group found particularly important when learning IAM: **grant only the permissions needed, nothing more**.

For example, if an EC2 instance only needs to read data from Amazon S3, instead of granting `AmazonS3FullAccess`, you only need to grant `s3:GetObject` on the specific bucket required. This minimizes the damage if that account or service is ever compromised — and it's a very common principle in enterprise systems.

#### 2.3. Not Every Resource Should Be Exposed to the Internet

A fairly common deployment mistake is putting every service in a Public Subnet — essentially Internet directly connecting to Backend, then Backend directly connecting to Database. If the database has a public IP and the Security Group is loosely configured, the risk of port scanning or attacks increases significantly.

A more secure architecture typically maintains a clear separation:

> **Internet → Load Balancer → Backend (Public Subnet) → Database (Private Subnet)**

The database sits in a Private Subnet, accessible only by the Backend — not directly exposed to the outside. This architectural pattern is heavily referenced in the **AWS Well-Architected Framework**.

#### 2.4. Protecting Applications from Web Attacks

Even when code is well-written, applications can still be attacked with malicious requests — SQL Injection, Cross-Site Scripting (XSS), automated bots flooding thousands of requests, or application-layer DDoS.

**AWS WAF (Web Application Firewall)** was designed to filter these requests before they reach the application. WAF can:

- Block suspicious IPs
- Rate-limit requests from a single IP address
- Detect common attack patterns based on OWASP standards
- Block requests containing malicious payloads

As a result, the application experiences reduced load and improved resilience against Internet-based attacks.

#### 2.5. The System Is Running — How Do You Know If It's Under Attack?

Security doesn't stop at correct initial configuration — it requires **continuous monitoring**. AWS offers several services to support this:

- **Amazon GuardDuty:** Analyzes data from AWS CloudTrail, VPC Flow Logs, and DNS Logs to detect anomalous behavior — logins from unusual geographic locations, an EC2 suddenly pushing large volumes of data outward, bot-like API calls, or access from known-malicious IPs. Instead of manually sifting through millions of log lines, GuardDuty automatically generates alerts for administrators to investigate.

- **Amazon Inspector:** Addresses a different problem — an application may run normally yet still harbor internal vulnerabilities. Inspector scans EC2 instances, container images, and software libraries to detect unsupported packages, libraries with CVE vulnerabilities, or insecure configurations — especially valuable for Docker-based or microservices architectures.

- **AWS Security Hub:** Acts as a central aggregation hub when an enterprise uses multiple security services simultaneously. It consolidates findings from GuardDuty, Inspector, IAM Access Analyzer, AWS Config, and Macie into a single dashboard, making it much easier for operations teams to grasp the overall security posture.

---

### 3. Common Deployment Challenges

#### 3.1. Server Slowness Under High Traffic

This isn't exactly an error, but a very common situation. A team's website might run smoothly with a few dozen visitors, but on project defense day, 200 students access it simultaneously — and the server overloads immediately: pages load very slowly, APIs respond sluggishly, some requests time out.

Combining **Amazon EC2 Auto Scaling** with **Elastic Load Balancer**, the system can automatically provision additional servers when needed and distribute requests evenly across multiple instances, allowing the application to maintain performance even during sudden traffic spikes.

#### 3.2. Data Loss After Server Replacement

Another common beginner mistake is storing all images or uploaded files directly on the server (e.g., an `uploads/` folder living right on the EC2 instance). The problem is, if a new EC2 instance is created or the server encounters an issue, these files can disappear if not backed up in time.

That's why **Amazon S3** is typically used to store images, videos, PDFs, backups, and system logs — while EC2 focuses solely on application logic. Separating data storage from application execution reduces the risk of data loss and makes future scaling easier.

---

### 4. What Our Team Learned

After studying AWS and exploring security solutions further, what our team realized is: **security is not a feature bolted on after the project is finished** — it should be part of the system design process from the very beginning. Similarly, most deployment incidents don't stem from "bad code" — they come from how the system is configured and operated.

Some useful principles to remember:

- Never store credentials in source code
- Apply the Principle of Least Privilege
- Clearly separate Public and Private resources
- Monitor systems continuously, not just react to incidents
- Regularly scan for vulnerabilities and update libraries
- Track operational status and log comprehensively
- Design systems with fault tolerance and scalability in mind

For learning projects, it may not always be necessary to deploy full GuardDuty or Security Hub. But understanding why they exist and what problems they solve helps our team develop the mindset to build more secure and professional systems when stepping into real-world projects.

That is also why AWS doesn't just provide compute or storage services — it builds an entire ecosystem supporting deployment, monitoring, and operation in real-world environments.

---

**Author Team:** Thành Nhân, Nguyễn Bá Nam, Nam Phan, Nguyễn Trọng Nhân

**References:**
- [IAM Best Practices (AWS Docs)](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Well-Architected – Security – IAM](https://docs.aws.amazon.com/wellarchitected/latest/framework/sec-iam.html)
- [AWS WAF](https://docs.aws.amazon.com/waf/latest/developerguide/what-is-aws-waf.html)
- [Amazon GuardDuty](https://docs.aws.amazon.com/guardduty/latest/ug/what-is-guardduty.html)
- [Amazon Inspector](https://aws.amazon.com/inspector/)