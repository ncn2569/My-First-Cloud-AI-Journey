---
title: "Blogs Posted"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

During our internship at FCAJ, our team researched, discussed, and co-authored 2 in-depth technical blogs sharing AWS knowledge with the [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj) community. Each blog is the result of hands-on exploration, distilled from real problems we encountered while working with AWS services.

---

###  [Blog 1 - THE CONNECTION EXHAUSTION PROBLEM WITH RDS PROXY](3.1-Blog1/)

The **Connection Exhaustion** problem arises when combining Serverless architecture (AWS Lambda) with a traditional relational database (Amazon RDS). Thousands of Lambda functions simultaneously opening connections can overwhelm RDS, causing it to refuse service. This blog analyzes the failure mechanism in detail and how **Amazon RDS Proxy** resolves it through 3 core features: Multiplexing, Graceful Failover, and IAM Authentication.

> **Published:** June 20, 2026 | **Authors:** Thành Nhân, Nguyễn Cảnh Nguyên, Nguyễn Trọng Nhân, Nam Phan, Nguyễn Bá Nam

---

###  [Blog 2 - SECURITY IN SOFTWARE DEVELOPMENT ON AWS](3.2-Blog2/)

This blog compiles 5 essential security lessons for developing and deploying applications on AWS: never hardcoding Access Keys, applying the **Least Privilege** principle, separating Public/Private Subnets, protecting applications with **AWS WAF**, and continuous monitoring with **GuardDuty, Inspector, and Security Hub**. It also covers common real-world scenarios such as server overload and data loss during server replacement.

> **Published:** July 10, 2026 | **Authors:** Thành Nhân, Nguyễn Bá Nam, Nam Phan, Nguyễn Trọng Nhân

---

{{% notice info %}}
Both blogs were published on the [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj) — a community space for sharing and learning AWS Cloud knowledge together.
{{% /notice %}}