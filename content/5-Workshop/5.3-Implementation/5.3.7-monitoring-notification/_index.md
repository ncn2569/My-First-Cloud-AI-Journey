---
title : "Configure Monitoring & Notification (CloudWatch & SNS)"
date : 2026-07-27 
weight : 7
chapter : false
pre : " <b> 5.3.7 </b> "
---
#### Create SNS Topic
- Go to Amazon SNS $\rightarrow$ Topics $\rightarrow$ Click **Create topic** named `TelcoChurnAlerts`.
- Click **Create subscription** $\rightarrow$ Protocol: **Email** $\rightarrow$ Enter your Gmail address $\rightarrow$ Confirm the email in your inbox.
![sns](/images/5-Workshop/5.3-Implementation/sns.png)
#### Create an Alarm
- In the **CloudWatch Console**, navigate to **Alarms** and select **Create alarm**.
- Click the orange **Select metric** button under the **Metric** section.
![metric](/images/5-Workshop/5.3-Implementation/metric.png)
- In the **Select metric** window that appears, under the **Browse** tab, select **Lambda** $\rightarrow$ **By Function Name** $\rightarrow$ **telco-churn-api-handler** $\rightarrow$ **Select metric**.
![metric-name](/images/5-Workshop/5.3-Implementation/metric-name.png)
- After selecting the metric, the interface returns to the configuration page. Scroll down to **Conditions**:
   + **Threshold type**: Select **Static**
   + **Whenever Errors is...**: Select **Greater/Equal** (`>= threshold`)
   + **than...**: Enter the threshold value `1`
 ![cond](/images/5-Workshop/5.3-Implementation/cond.png)
- Under **Notification**:
   + **Alarm state trigger**: Select **In alarm** (triggers the action when the metric exceeds the threshold).
   + **Send a notification to the following SNS topic**: Select **Select an existing SNS topic**.
   + **Send a notification to...**: Select the pre-created SNS Topic from the dropdown (e.g., `Telco-Churn-Alarm-Topic`).
   + Check the notification email address shown under **Email (endpoints)** below (e.g., `trungnam2682005@gmail.com`).
   + Scroll to the bottom and click **Next**.
    ![notice](/images/5-Workshop/5.3-Implementation/notice.png)
- Under **Name and description**:
   + **Alarm name**: Enter an alarm name, e.g., `Telco-Churn-API-Error-Alarm`.
   + **Alarm description - optional**: Enter a description for the alarm if needed.
   + Click **Next** at the bottom.
    ![alarm-name](/images/5-Workshop/5.3-Implementation/alarm-name.png)