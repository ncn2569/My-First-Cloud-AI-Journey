---
title: "Blog 2"
date: 2026-07-30
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# SECURITY IN SOFTWARE DEVELOPMENT ON AWS — REAL-WORLD LESSONS FROM OUR TEAM

### Introduction

Throughout our AWS learning journey, our team kept coming back to one uncomfortable truth: when you first start building a project, the only question that matters is **"how do I make it run?"** But the deeper we went, the more we realized the real question should be **"is it actually secure?"**

An application can work flawlessly from a functional standpoint, but a single misconfiguration — an exposed key pair, a security group opened too wide, an overly generous IAM policy — can have devastating consequences. AWS doesn't just provide infrastructure to deploy on. It offers an entire ecosystem of security services designed to be used **from day one**, not bolted on after an incident.

These are the real-world lessons our team collected — from studying, from building, and yes, from making mistakes.

---

### 1. Never Hardcode Access Keys — A Lesson from Real "Accidents"

This is the mistake almost every cloud newcomer makes at least once. Our team was no exception.

Early on, to speed up testing, a teammate wrote the Access Key and Secret Key directly into a Python file like this:

```
AWS_ACCESS_KEY = "AKIAxxxxxxxxxxxx"
AWS_SECRET_KEY = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

The plan was "I'll remove it later." Then they forgot. Fortunately, the repo was private so no one got access. But after researching further, the team realized just how serious this is. In reality, there are countless cases of AWS accounts being compromised because someone accidentally pushed credentials to a public GitHub repo. Hackers use those keys to mine cryptocurrency, spin up hundreds of EC2 instances — some people received bills of **thousands of dollars within a few hours**.

The lesson our team internalized: **credentials never belong in code**. Instead:

| Approach | Description |
|----------|-------------|
| **IAM Role** | Attach roles directly to EC2/Lambda — the SDK auto-retrieves credentials. No Access Keys needed. |
| **AWS Secrets Manager** | Store sensitive credentials with automatic rotation, native integration with RDS and Lambda. |
| **AWS Systems Manager Parameter Store** | Simple config & secret storage, extremely low cost — good for non-sensitive configs. |
| **Environment Variables** | Only for non-sensitive config. If you must use them for secrets, encrypt with KMS. |

The key takeaway isn't "which service to use" — it's the mindset: **separate code from credentials from the start**. Once this becomes a habit, the risk of key leakage drops dramatically.

---

### 2. Least Privilege — Grant Exactly What's Needed, Nothing More

This is the principle we heard repeated most often while studying IAM, and also the principle we found **easiest to ignore when rushing**.

A concrete example: an EC2 instance just needs to read images from a single S3 bucket to display on a web page. The knee-jerk reaction? "Just attach **AmazonS3FullAccess** — it's faster." But if that EC2 instance gets compromised, an attacker can now read, write, and delete **every bucket in the account**.

Instead, all you need is a minimal policy like this:

```json
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::my-images-bucket/*"
}
```

Our team spent an entire session reviewing all active IAM policies in our project and found quite a few over-permissioned ones. Regular checks using **IAM Access Analyzer** and **Credential Reports** help catch overly broad policies you might have missed.

The rule we now follow: **"If you're not sure what permissions you need, start by denying everything, then open one permission at a time as needed."**

---

### 3. Not Every Resource Should Be Public

Another common mistake we've seen (and nearly made ourselves when first designing architecture) is throwing everything into Public Subnets — Internet => Backend => Database, all with public IPs.

What's the consequence? If your database has a public IP, even with a strong password, it's still a target for port scanning from the Internet. And if a security group accidentally opens port 3306 (MySQL) or 5432 (PostgreSQL) to 0.0.0.0/0 — you've essentially left the door wide open.

The architecture our team found both reasonable and effective, which we adopted for our project:

```
Internet => Application Load Balancer (Public Subnet)
         => Backend EC2/Lambda (Public Subnet)
         => Database RDS (Private Subnet — NO public IP)
```

The database lives in a Private Subnet, accessible only by the backend through a specific security group rule. No Internet Gateway route points to the Private Subnet — there's literally no way for the outside world to "see" the database. This model is heavily emphasized in the **AWS Well-Architected Framework**, and we found it genuinely effective when put into practice.

---

### 4. AWS WAF — The Shield Before Web Attacks Hit Your App

Even if your backend code is carefully written, your application can still be attacked at the HTTP request layer — SQL Injection, Cross-Site Scripting (XSS), automated bot spam, or application-layer DDoS.

**AWS WAF (Web Application Firewall)** is a service our team found somewhat underrated — many people know about it but few use it, partly because they assume it's complex. In reality, WAF works quite intuitively:

- Define a **Web ACL** — a collection of rules that filter incoming requests.
- Each rule checks a condition: is the IP on a blocklist? Does the request contain SQL injection patterns? Has the request rate from a single IP exceeded the threshold?
- If violated, the request is blocked **before it reaches your application**.

Our team set up a simple Web ACL with 3 rules:
1. **AWS Managed Rule - SQL Database** — blocks SQL injection patterns.
2. **Rate-based Rule** — limits 100 requests/minute per IP.
3. **IP Set Rule** — blocks IPs already flagged by GuardDuty.

The result: the application experienced reduced load (bots could no longer spam), and it was significantly safer against malicious requests. A small tool with outsized impact.

---

### 5. The System Is Running — How Do You Know If It's Under Attack?

Security doesn't stop at configuration. After deploying, the next question is: **"how do we know if the system is being attacked?"** Our team spent time exploring three main AWS services for this:

#### Amazon GuardDuty

GuardDuty continuously analyzes three data sources: **CloudTrail logs** (API behavior), **VPC Flow Logs** (network traffic), and **DNS logs**. Its strength? It uses machine learning + threat intelligence to detect anomalies without any configuration. Some patterns it catches:

- Logins from unusual geographic locations (e.g., your account is used from Vietnam, and suddenly someone logs in from Russia).
- An EC2 instance unexpectedly pushing large volumes of data outbound (potential data exfiltration).
- Bot-like API call patterns — high frequency, repeating the same action.
- Access from IPs on the global threat intelligence blocklist.

The beauty is that GuardDuty auto-generates findings in the console — no need to manually sift through millions of log lines.

#### Amazon Inspector

While GuardDuty focuses on behavioral anomalies, Inspector tackles **internal vulnerabilities** — an application can run fine yet still carry critical CVEs. Inspector automatically scans:

- **EC2 instances**: which packages have reached end-of-support? Which security patches are missing?
- **Container images (ECR)**: does the image contain libraries with critical CVEs?
- **Lambda functions**: are there vulnerable dependencies in the function code?

Extremely useful for Docker-based or microservice architectures, where dependency counts can reach the hundreds and developers struggle to track them all.

#### AWS Security Hub

When you're using multiple security services simultaneously, the problem is that each has its own dashboard — to get an overview you'd need to open 3-4 tabs. Security Hub solves exactly this: it **aggregates findings** from GuardDuty, Inspector, IAM Access Analyzer, AWS Config, and Macie into a single dashboard, with severity scores following the **AWS Security Finding Format (ASFF)**.

Our team found Security Hub especially well-suited for production environments where you need a quick holistic view rather than checking each service individually.

---

### 6. Two "Real-Life" Situations That Are Shockingly Common

Beyond pure security principles, our team encountered two practical problems that, if overlooked, significantly impact user experience:

**Server slowdown under high traffic:** Our team's website ran smoothly with a few dozen testers. But on demo day in front of the review panel, nearly 100 people accessed it simultaneously — the server overloaded immediately. EC2 CPU spiked to 100%, requests kept timing out. The fix: combining **EC2 Auto Scaling** (auto-provision additional instances when CPU exceeds 70%) with an **Application Load Balancer** (distribute requests evenly). After setup, the system handled 3-4× normal traffic smoothly.

**Data loss after server replacement:** One teammate stored all uploaded images in an `uploads/` folder directly on the EC2 instance. When the instance needed replacing (the old one had issues), all those images vanished — no backup. After this incident, the team switched to using **S3** for static files and **EFS** for shared storage across EC2 instances. Separating storage from compute — a basic lesson we had to pay a price for to truly remember.

---

### 7. What Our Team Walked Away With

After everything, the biggest realization was this: **security is not a "feature" you add at the end of a project**. It needs to be part of the architectural design process from day one. Most security incidents don't come from bad code — they come from **how the system is configured and operated**: a security group opened too wide, an IAM policy that's too generous, a key pair that was forgotten.

The principles our team will carry into future projects:

- Separate code and credentials — use IAM Roles and Secrets Manager.
- Apply Least Privilege rigorously — review policies regularly.
- Clearly separate public and private subnets — never expose databases to the Internet.
- Use WAF as a default protection layer for every web application.
- Monitor continuously with GuardDuty + Inspector + Security Hub — don't wait for an incident to check.
- Separate storage from compute — S3/EFS for data, EC2/Lambda for processing.

For learning projects, you don't necessarily need to enable every service above. But **understanding why they exist and what problems they solve** will help us build the mindset needed to design safe and professional systems when we step into real-world environments.

---

**Team authors:** Thành Nhân, Nguyễn Bá Nam, Nam Phan, Nguyễn Trọng Nhân, Nguyễn Cảnh Nguyên

**Link Blog:** [Security in Software Development on AWS](https://www.facebook.com/groups/awsstudygroupfcj/?multi_permalinks=2228803837884576&notif_id=1785383944402087&notif_t=feedback_reaction_generic_tagged)


**References:**
- [IAM Best Practices — AWS Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Security Pillar — AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/)
- [AWS WAF Developer Guide](https://docs.aws.amazon.com/waf/latest/developerguide/)
- [Amazon GuardDuty User Guide](https://docs.aws.amazon.com/guardduty/latest/ug/)
- [Amazon Inspector — Automated Vulnerability Management](https://docs.aws.amazon.com/inspector/latest/user/)
- [AWS Security Hub User Guide](https://docs.aws.amazon.com/securityhub/latest/userguide/)
- [AWS Security Best Practices Whitepaper](https://docs.aws.amazon.com/whitepapers/latest/aws-security-best-practices/)