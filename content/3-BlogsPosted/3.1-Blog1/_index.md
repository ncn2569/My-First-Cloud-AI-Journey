---
title: "Blog 1"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# THE CONNECTION EXHAUSTION PROBLEM: WHEN AWS LAMBDA MEETS RDS — AND HOW AMAZON RDS PROXY SAVES THE DAY

### Introduction

While learning AWS, our team had the chance to dive deep into cloud database services — RDS, DynamoDB, ElastiCache, you name it. But one problem sparked a lot of debate and eventually forced us all to sit down and figure it out together: what actually happens when you combine a **Serverless** model — specifically AWS Lambda — with a traditional relational database like RDS?

Back in university, we were all taught Connection Pooling as a textbook optimization technique. Apply it, and you save database resources. Simple enough. But when we tried to apply that same logic to a cloud environment with potentially thousands of Lambda functions running concurrently... well, let's just say the textbook didn't cover this part. Today, we want to share our team's full journey of researching the **Connection Exhaustion** problem and how **Amazon RDS Proxy** came to the rescue.

---

### 1. Two Opposing Philosophies — A Recipe for Disaster

The first thing our team noticed when analyzing this: **Lambda and RDS were born from two completely different worlds**.

**AWS Lambda** is designed to scale almost limitlessly. A sudden traffic spike? No problem — API Gateway can spin up thousands of execution environments simultaneously. Each environment is an isolated container, completely stateless, with an incredibly short lifecycle — sometimes existing for just a few hundred milliseconds before vanishing.

**Amazon RDS** is the polar opposite. Sure, it's a managed database service, but underneath the hood, it's still a traditional PostgreSQL or MySQL server. And like any traditional RDBMS, database connections aren't free. With PostgreSQL specifically, each new connection forces the OS to fork a separate process, consuming approximately **10MB of RAM** per connection. On a typical db.t3.medium instance with 4GB RAM — after accounting for the buffer pool and OS overhead — the max connections ceiling sits around a few hundred.

**Here's the collision scenario our team simulated:**

> A flash sale causes API traffic to spike 10x. API Gateway triggers 2,000 Lambda functions running simultaneously. Following the default logic, each function opens a direct connection to RDS. The database can only handle 500 connections max. The result? RDS immediately rejects all new connections with **"FATAL: remaining connection slots are reserved for non-replication superuser connections"** — the application crashes before anyone can react.

This isn't a code bug. This is a **fundamental design philosophy conflict** between two services.

---

### 2. Why Traditional Connection Pooling Can't Save You

Our team's first reaction when we hit this: "Just use a connection pool, what's the big deal?" In traditional monolithic applications, that's exactly right. Libraries like **pg-pool (Node.js)** or **HikariCP (Java)** maintain a ready pool of open connections, reused across requests — it works beautifully.

But when we tried applying this to Lambda, the cracks appeared immediately:

- Every Lambda function runs in a **completely isolated environment**. No shared memory. No shared state.
- If 2,000 Lambda functions cold-start simultaneously, you end up with **2,000 independent connection pools**, each opening another 5-10 connections of its own.
- The actual number of connections hitting RDS doesn't decrease — it **multiplies dramatically**.

The problem isn't Connection Pooling itself. The problem is that **connection pools operate at the application layer** — and Lambda scales at the infrastructure layer, completely outside the pool's control. We joked that this was a classic case of "right solution, wrong place."

---

### 3. Amazon RDS Proxy — The Right Middleman in the Right Place

After digging through documentation and running some tests, our team discovered AWS had already anticipated this problem. The answer: **Amazon RDS Proxy** — a fully managed database proxy service sitting between Lambda and RDS. The core idea is elegantly simple: instead of thousands of Lambda functions connecting directly to the database, all of them go through a single gatekeeper.

We found RDS Proxy solves three very valuable problems:

#### 3.1. Centralized Connection Pooling (Multiplexing)

Instead of each Lambda managing its own connection pool, RDS Proxy maintains a **single warm pool** of actual connections to RDS. Here's how it works in practice:

- Lambda A needs to run a query => sends a request to RDS Proxy.
- Proxy grabs an idle connection from the warm pool => executes the SQL => returns results to Lambda A => **returns the connection to the pool**.
- Lambda B, C, D... reuse those exact same connections.

This technique is called **connection multiplexing**. The critical insight: thousands of Lambda functions can share **just a few dozen actual database connections**. We tested this with 500 concurrent Lambda invocations — RDS Proxy opened exactly 20 connections to the database and handled everything smoothly.

#### 3.2. Graceful Failover — No Dropped Requests

Another detail that really impressed our team was failover handling. In an RDS Multi-AZ setup, when the primary database fails, AWS automatically promotes the standby to primary. This process typically takes **30–60 seconds** — and if your application connects directly to the database, every request during that window fails with "connection refused."

RDS Proxy handles it differently: it **holds pending requests** in an internal queue, waits for the new database to become available, then automatically reroutes. From Lambda's perspective? The API response was just slightly slower than usual — no errors, no dropped requests. A small detail that's absolutely critical for production systems.

#### 3.3. IAM Authentication — No More Plaintext Passwords

This was the feature our team appreciated most from a security standpoint. Instead of embedding database passwords as plaintext in Lambda environment variables (a huge security risk), RDS Proxy lets Lambda authenticate using its own **IAM Role**. The flow:

- Lambda sends a request to RDS Proxy with an IAM token auto-generated by the SDK.
- RDS Proxy validates that token against IAM, then **uses its own managed credentials** from AWS Secrets Manager to connect to RDS.
- Lambda never sees the database password. Ever.

This felt much cleaner and more secure than manually managing credentials — especially in environments with dozens of functions accessing the same database.

---

### 4. A Reality Check — Not Every Problem Needs RDS Proxy

After fully understanding the benefits, our team also discussed the flip side: **when do you NOT need RDS Proxy?** After all, it's a managed service with costs (billed per hour + per connection), and you shouldn't just enable it everywhere.

Through discussion, we agreed on several scenarios where it's unnecessary:

- Lambda functions that only run a few times per hour — no risk of connection explosion.
- Monolithic applications running on EC2 with traditional HikariCP/pg-pool — since the pool exists in a single process, it doesn't suffer from Lambda's fragmentation problem.
- Backend using DynamoDB instead of RDS — DynamoDB uses HTTP APIs and has no concept of connection pooling.

This was an important lesson: **understand the trade-offs before adopting a service, rather than enabling it just because it sounds cool.**

---

### 5. Closing Thoughts

What our team valued most from this deep dive wasn't just learning about another AWS service — it was understanding the **root cause** of the problem. Why two services under the same cloud provider can conflict with each other, and why the solution sits at the proxy layer rather than the application layer. That kind of systems thinking, we believe, will be useful in the long run — for any distributed system, not just on AWS.

We hope this article helps anyone exploring Serverless + RDS architectures. If you have questions or want to discuss further, drop a comment — our whole team will jump in and chat with you!

---

**Team authors:** Thành Nhân, Nguyễn Cảnh Nguyên, Nguyễn Trọng Nhân, Nam Phan, Nguyễn Bá Nam

**Link Blog:** [Amazon RDS Proxy](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2227947781303515/)

**References:**
- [Connection Management with Amazon RDS Proxy](https://aws.amazon.com/rds/proxy/)
- [Using RDS Proxy with AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/configuration-database.html)
- [Multiplexing & Connection Borrowing in RDS Proxy](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html)
- [RDS Proxy vs Direct Connection — AWS Database Blog](https://aws.amazon.com/blogs/database/using-amazon-rds-proxy-with-aws-lambda/)