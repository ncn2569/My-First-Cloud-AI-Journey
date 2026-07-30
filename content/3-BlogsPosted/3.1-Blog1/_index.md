---
title: "Blog 1"
date: 2026-06-20
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# THE CONNECTION EXHAUSTION PROBLEM WHEN COMBINING AWS LAMBDA WITH RDS — AND HOW AMAZON RDS PROXY SOLVES IT

### 1. Introduction

When studying core subjects like Operating Systems or Database Management Systems, we are often taught to set up **Connection Pooling** in application source code to conserve resources. However, when applying these standard theories to a **Serverless** cloud computing environment, we run into a real architectural nightmare.

Today, we'll share a detailed look at the **Connection Exhaustion** problem that arises when combining AWS Lambda with a Relational Database (RDBMS), and how **Amazon RDS Proxy** comprehensively addresses this bottleneck.

---

### 2. The Root of the Disaster: A Clash Between Two Worlds

**Serverless architecture (AWS Lambda)** and **traditional relational databases (Amazon RDS** like PostgreSQL, MySQL) were born with two fundamentally opposing philosophies:

- **AWS Lambda (Flexible & Stateless):** Can scale out from 0 to thousands of execution environments in the blink of an eye when traffic spikes. It is completely stateless and has an extremely short lifecycle.

- **Amazon RDS (Fixed & Resource-Heavy):** Each connection established to RDS is not free. For PostgreSQL, for example, each new connection requires the underlying OS to allocate a separate process, consuming approximately **10MB of RAM**. The maximum number of connections (`max_connections`) is typically locked at a few hundred to a thousand, depending on the server's RAM.

**The problem occurs when:** A large traffic spike hits. API Gateway triggers 2,000 Lambda functions running in parallel. Each Lambda opens a new connection to the database. RDS can only handle 500 connections. The result? The database throws `Too many connections`, refuses service, and the **entire system collapses in a cascading failure**.

---

### 3. Why Traditional Connection Pooling Is Useless

Normally, developers use libraries like **pg-pool** (Node.js) or **HikariCP** (Java) to maintain a group of pre-opened connections. However, this approach **does not work on AWS Lambda**.

Because each Lambda function runs in an isolated environment, they cannot share memory with one another. If 2,000 Lambda functions all spin up, you end up with **2,000 independent Connection Pools**, each opening a few more connections. The resource crisis doesn't decrease — it **multiplies**!

---

### 4. The Solution: Amazon RDS Proxy as an Intermediate Filtering Layer

To solve this thorny problem, AWS introduced **Amazon RDS Proxy**. This is a fully managed database proxy service that sits between AWS Lambda and Amazon RDS.

Its operating mechanism and how it "saves" the system are demonstrated through three core features:

#### 4.1. Centralized Connection Pooling (Multiplexing)

Instead of letting thousands of Lambda functions hit the database directly, they connect to RDS Proxy. The Proxy maintains a **warm pool** of actual connections to RDS. When a Lambda function needs to execute a query, the Proxy borrows an idle connection from the pool, sends the SQL command, receives the result, and returns that connection to the pool for another Lambda function to reuse.

This **multiplexing** technique allows **thousands of Lambdas to share just a few dozen actual DB connections**.

#### 4.2. Graceful Failover Handling

In a distributed system, if the Primary DB server goes down, AWS automatically fails over to the Standby server. This process typically takes around **30–60 seconds** and causes application network drops.

With RDS Proxy, it proactively holds Lambda queries in a queue and automatically reroutes to the new DB once recovery is complete. The application only experiences slightly slower API responses — it **never encounters an outright error**.

#### 4.3. Enhanced Security with IAM Authentication

Managing plaintext DB passwords in environment variables is a major risk. RDS Proxy allows Lambda functions to authenticate via an **IAM Role** instead of using passwords. The Proxy then uses credentials on behalf of the application to communicate with the database, securing the system at its foundation.

---

### 5. Conclusion

Understanding the physical limits of OS processes underlying the database helps us clearly see why we cannot blindly scale Serverless services. By integrating **Amazon RDS Proxy**, we've transformed an architecture at risk of a "bottleneck" into a flexible system that can freely scale to handle tens of thousands of requests while the relational database behind it remains calm and stable.

---

**Author Team:** Thành Nhân, Nguyễn Cảnh Nguyên, Nguyễn Trọng Nhân, Nam Phan, Nguyễn Bá Nam

**References:**
- [Connection Management Overview with Amazon RDS Proxy](https://aws.amazon.com/rds/proxy/)
- [How RDS Proxy Works with AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/configuration-database.html)
- [Multiplexing Mechanism & Connection State Management](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html)