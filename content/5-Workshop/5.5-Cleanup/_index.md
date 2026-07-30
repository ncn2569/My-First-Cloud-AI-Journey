---
title : "Clean-up Resources"
date : 2026-07-29
weight : 6
chapter : false
pre : " <b> 5.5. </b> "
---

To avoid incurring unnecessary charges on your AWS account after completing workshop testing, perform resource clean-up following the sequence of steps below.

#### Delete SageMaker Serverless Endpoint & Configurations
- Access Amazon SageMaker Studio  => Deployments  => Endpoints: Select telco-churn-serverless-endpoint  => Delete.
![clean-server](/images/5-Workshop/5.4-Test-Validation/clean-server.png)
- Select JumpStart / Models: Select TelcoChurnModelGroup  => Delete.
![clean-group](/images/5-Workshop/5.4-Test-Validation/clean-group.png)

#### Delete SageMaker Pipeline
- In SageMaker Console, open Pipelines section.
- Select TelcoChurnPipeline (or your Pipeline name).
- Click Delete and confirm Pipeline deletion.
![clean-pipeline](/images/5-Workshop/5.4-Test-Validation/clean-pipeline.png)

#### Delete Amazon CloudFront Distribution & AWS WAF
##### Disable and Delete CloudFront Distribution
- Go to **Amazon CloudFront**  => **Distributions**.
- Select the telco-churn-cloudfront-waf distribution.
- Click **Disable** and wait until the status changes to Disabled.
![disable](/images/5-Workshop/5.3-Implementation/disable.png)
- Once disabled, select the distribution again and click **Delete**.

##### Delete AWS WAF Web ACLs
- Go to **AWS WAF & Shield**  => **Web ACLs**.
- Set the region filter to **Global (CloudFront)**.
- Select the Web ACL associated with your CloudFront distribution  => Click **Action**  => **Delete**.
![acls](/images/5-Workshop/5.3-Implementation/acls.png)
