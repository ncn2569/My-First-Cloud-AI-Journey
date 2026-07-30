---
title: "Week 2 Worklog"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Master IAM: Users, Groups, Roles, Policies, and the Policy Evaluation Logic mechanism.
* Apply the Least Privilege principle when assigning permissions.
* Secure the account with MFA, Password Policy, and Credential Reports.
* Learn S3: buckets, versioning, lifecycle policies, encryption, static website hosting.
* Attend FCAJ Meetup #2.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - IAM Overview: Users, Groups, Roles, Policy Evaluation Logic <br> - Root User vs IAM User <br> - AWS Managed vs Customer Managed Policies | 06/08/2026 | 06/08/2026 | [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) |
| 3   | - IAM Roles: Service Role (EC2 => S3), Cross-Account Role <br> - **Practice:** create IAM Role for EC2 instead of hardcoding Access Keys <br> - Enable MFA, Password Policy, Credential Report | 06/09/2026 | 06/09/2026 | [IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) |
| 4   | - S3: buckets, objects, storage classes (Standard, IA, Glacier, Deep Archive) <br> - S3 Versioning, Lifecycle Policy, Encryption (SSE-S3, SSE-KMS) <br> - **Practice:** create a bucket, upload objects, configure versioning + lifecycle | 06/10/2026 | 06/10/2026 | [S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/) |
| 5   | - S3 Static Website Hosting + CloudFront CDN + Route 53 <br> - S3 Bucket Policy & Pre-signed URLs <br> - **Practice:** host a static website on S3 + CloudFront | 06/11/2026 | 06/11/2026 | [S3 Static Website](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html) |
| 6   | - **Attend FCAJ Meetup #2 (13/06/2026):** <br>&emsp; + What does a DevOps Engineer really do? <br>&emsp; + Career Path in the AWS Ecosystem <br>&emsp; + Data Analytics & MNC Culture | 06/13/2026 | 06/13/2026 | AWS Study Group Community |
| 7   | - Write Event 2 recap <br> - Write worklog notes | 06/14/2026 | 06/14/2026 | |

### Week 2 Achievements:

* Mastered IAM: Users, Groups, Roles; understood Policy Evaluation Logic (Explicit Deny > Allow > Implicit Deny).

* Deployed IAM Role for EC2 replacing Access Keys - reduced credential leakage risk. Secured the account with MFA and Password Policy.

* Mastered S3: buckets, storage classes, versioning, lifecycle auto-transition, encryption, static website hosting. Selected the right storage class based on access frequency.

* Configured CloudFront CDN + S3 for faster, cheaper website hosting.

* Attended FCAJ Meetup #2 - gained deep insights into DevOps, MNC Culture, and Data Analytics.
