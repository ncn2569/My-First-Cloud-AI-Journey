---
title : "Test Real-time Inference Flow"
date : 2026-07-29
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

#### 1. Prepare the Input Data Payload (JSON)
Create a `payload.json` file containing the features of a telecom customer to predict Churn probability:
```json
{
    "raw_data": {
        "gender": "Female",
        "SeniorCitizen": 1,
        "Partner": "Yes",
        "Dependents": "No",
        "tenure": 1,
        "PhoneService": "No",
        "MultipleLines": "No phone service",
        "InternetService": "DSL",
        "OnlineSecurity": "No",
        "OnlineBackup": "Yes",
        "DeviceProtection": "No",
        "TechSupport": "No",
        "StreamingTV": "No",
        "StreamingMovies": "No",
        "Contract": "Month-to-month",
        "PaperlessBilling": "Yes",
        "PaymentMethod": "Electronic check",
        "MonthlyCharges": 29.85,
        "TotalCharges": 29.85
    }
}
```

#### 2. Execute the Request via cURL / Postman
Open a Terminal and send a POST request to the API Gateway Invoke URL just deployed:
```powershell
curl.exe -X POST https://c6kbjaktj9.execute-api.ap-southeast-1.amazonaws.com/predict \
         -H "Content-Type: application/json" \
         -d "@payload.json"
```

#### 3. Analyze the API Response
Successful result (HTTP 200 OK):

![inference](/images/5-Workshop/5.4-Test-Validation/inference.png)


#### 4. Check Logs & Metrics on Amazon CloudWatch
- Go to CloudWatch $\rightarrow$ Log groups $\rightarrow$ open the log for `/aws/lambda/telco-churn-api-handler`
   ![api-logs](/images/5-Workshop/5.4-Test-Validation/api-logs.png)
- Init Duration: 442.40 ms: 
  - This is the time to initialize the Lambda execution environment (Cold Start) for the very first time.
- Duration: 6746.15 ms (Billed Duration: 7189 ms):
  - Taking ~6.7 seconds for the first call is due to the SageMaker Serverless Endpoint just going through a Cold Start (re-initializing the container with the XGBoost model for a few seconds). Subsequent curl calls once the Endpoint is "warmed up" will drop to just tens to hundreds of milliseconds.