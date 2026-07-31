---
title: "Blogs Posted"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

During our internship at FCAJ, our team researched, discussed, and co-authored 3 in-depth technical blogs sharing AWS knowledge with the [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj) community. Each blog is the result of hands-on exploration, distilled from real problems we encountered while working with AWS services.

---

###  [Blog 1 - THE CONNECTION EXHAUSTION PROBLEM WITH RDS PROXY](3.1-Blog1/)

The **Connection Exhaustion** problem arises when combining Serverless architecture (AWS Lambda) with a traditional relational database (Amazon RDS). Thousands of Lambda functions simultaneously opening connections can overwhelm RDS, causing it to refuse service. This blog analyzes the failure mechanism in detail and how **Amazon RDS Proxy** resolves it through 3 core features: Multiplexing, Graceful Failover, and IAM Authentication.


---

###  [Blog 2 - SECURITY IN SOFTWARE DEVELOPMENT ON AWS](3.2-Blog2/)

This blog compiles 5 essential security lessons for developing and deploying applications on AWS: never hardcoding Access Keys, applying the **Least Privilege** principle, separating Public/Private Subnets, protecting applications with **AWS WAF**, and continuous monitoring with **GuardDuty, Inspector, and Security Hub**. It also covers common real-world scenarios such as server overload and data loss during server replacement.

---

###  [Blog 3 - INFRASTRUCTURE MANAGEMENT WITH TERRAFORM](3.3-Blog3/)

This blog shares the team's journey from managing cloud infrastructure manually through the AWS Console to adopting **Infrastructure as Code (IaC)** with **Terraform**. We cover the core concepts: defining infrastructure in HCL code files, the Plan/Apply safety workflow, managing state securely with S3 Remote Backend + DynamoDB Locking, building reusable Terraform Modules, and detecting/controlling Infrastructure Drift. The key takeaway: infrastructure is not just hardware or cloud services — infrastructure is code.
