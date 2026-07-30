---
title : "Resource Cleanup"
date : 2026-07-29
weight : 6
chapter : false
pre : " <b> 5.5. </b> "
---

To avoid unnecessary charges on your AWS account after finishing the workshop testing, clean up all resources in the following order.

#### Delete SageMaker Serverless Endpoint & Configurations
- Go to Amazon SageMaker Studio $\rightarrow$ Deployments $\rightarrow$ Endpoints: Select `telco-churn-serverless-endpoint` $\rightarrow$ Delete.
![clean-server](/images/5-Workshop/5.4-Test-Validation/clean-server.png)
- Select JumpStart / Models: Select `TelcoChurnModelGroup` $\rightarrow$ Delete.
![clean-group](/images/5-Workshop/5.4-Test-Validation/clean-group.png)

#### Delete SageMaker Pipeline
- In the SageMaker Console, open the **Pipelines** section.
- Select `TelcoChurnPipeline` (or your Pipeline name).
- Click **Delete** and confirm the deletion.
![clean-pipeline](/images/5-Workshop/5.4-Test-Validation/clean-pipeline.png)