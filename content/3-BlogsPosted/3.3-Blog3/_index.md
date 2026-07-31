---
title: "Blog 3"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# INFRASTRUCTURE MANAGEMENT WITH TERRAFORM — BEYOND CLICKING ON THE CONSOLE

### 1. How it started

When you first start building on the cloud, whether it's a VPC, an EC2, an RDS database, or an S3 bucket, everyone kind of does the same thing: open the AWS Console, click here, click there, and it works. Honestly, it feels pretty satisfying at first, and it's a great way to learn.

But then the project grows. You need to replicate everything to a staging environment. Or someone on the team accidentally changes a Security Group on the console, and nobody knows how to roll it back. That's when the question hits: **"Wait... how do we reliably manage all this?"**

That question is what pushed the team toward **Terraform** and the **Infrastructure as Code (IaC)** approach — treating infrastructure like software, version-controlled, reviewable, and reproducible.

---

### 2. 5 Things we learned about managing infrastructure with Terraform

#### 2.1. Infrastructure as Code — Your infrastructure becomes source code

Instead of memorizing click sequences in the console, everything is defined in HCL (HashiCorp Configuration Language) files. Servers, networks, databases, firewalls — all written down.

A basic EC2 definition looks like this:
```hcl
resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t3.micro"

  tags = {
    Name = "WebServer-Dev"
  }
}
```

Once it's in code, you can store it in Git, track who changed what, get peer reviews before deploying, and reuse it anywhere. No more guessing what someone clicked last week.

#### 2.2. Plan and Apply — See what's about to happen before it happens

This might be the feature everyone in the team appreciated most: Terraform shows you exactly what it's going to change before it does anything. The standard workflow has three steps:

- **terraform init:** Set up the working directory and download provider plugins (AWS, Azure, GCP, etc.).
- **terraform plan:** Compare your code against what's actually running and show every addition (+), modification (~), and deletion (-).
- **terraform apply:** Only after you type "yes" does Terraform make the actual API calls to AWS.

Having the `plan` command is like a safety net. It catches things like accidentally deleting a database or misconfiguring a security group — mistakes that are way too easy to make when operating through the console manually.

#### 2.3. The real brain — terraform.tfstate

Working as a team raises a tricky question: **How does Terraform know what resources already exist and which ones don't?**

The answer is a file called **terraform.tfstate**. It keeps track of the current state of everything Terraform manages. When we first started, we made the classic beginner mistake: storing the `.tfstate` file on our local machines or even committing it to Git.

- Two people run `apply` at the same time → state gets corrupted
- State files contain sensitive data (passwords, tokens) → pushing them to GitHub is a massive security risk

**The standard fix:** Use a **Remote Backend** (Amazon S3 to store the state file) with a **DynamoDB table** for state locking. When one person is deploying, DynamoDB locks the state so nobody else can touch it at the same time.

#### 2.4. Don't write everything in one file — Use Modules

As the project grew, cramming all resources into a single `main.tf` file became messy fast. Everything was in one place, hard to read, hard to debug.

The solution is to package related resources into reusable **Modules** — a VPC module, an RDS module, an EKS module. Then you call them from anywhere:

```hcl
module "vpc_dev" {
  source     = "./modules/vpc"
  cidr_block = "10.0.0.0/16"
  env        = "dev"
}

module "vpc_prod" {
  source     = "./modules/vpc"
  cidr_block = "10.1.0.0/16"
  env        = "prod"
}
```

This keeps dev and prod 100% architecturally consistent. The only difference is what scale parameters you pass in.

#### 2.5. Dealing with Drift — When someone changes things on the Console

Let's be honest: in real life, someone is occasionally going to log into the AWS Console and tweak a Security Group or resize an Instance without updating the Terraform code. This is called **Infrastructure Drift**.

When someone runs `terraform plan` afterward, Terraform scans the live environment, notices the mismatch between code and reality, and proposes changes to bring everything back in line with what's defined in the code. It keeps your infrastructure governed by a **Single Source of Truth** — the code.

---

### 3. What this means in practice

#### 3.1. Centralized state management

When multiple people work on the same infrastructure, keeping the state file consistent is critical. Using S3 as a remote backend with DynamoDB for locking prevents write conflicts and keeps sensitive data encrypted.

#### 3.2. Consistent environments across dev, staging, and production

Manually keeping dev, staging, and prod in sync is a recipe for configuration drift. Wrapping infrastructure into standardized modules lets you spin up new environments quickly and guarantees the same architecture across every tier.

---

### 4. Where we landed

Working with Terraform changed how the team thinks about infrastructure. The biggest realization was simple: **Infrastructure is not just hardware or cloud services. Infrastructure is code.**

A few principles we now follow:

- Don't touch the console for anything managed by Terraform
- Always use a remote backend (S3 + DynamoDB) with state encryption
- Make `terraform plan` part of the CI pipeline — review it in pull requests before merging and applying
- Structure code in modules from day one for maintainability and reuse

Moving from "ClickOps" to "Infrastructure as Code" takes some upfront investment in learning the syntax and tooling. But once your systems reach a certain size, it stops being optional. It's how you build infrastructure that's reliable, reproducible, and ready for production.

---

**Authors:** Thành Nhân, Nguyễn Cảnh Nguyên, Nguyễn Trọng Nhân, Nam Phan, Nguyễn Bá Nam.

**Link Blog:** [Manage Infrastructure with Terraform — Beyond Clicking on the Console](https://www.facebook.com/groups/awsstudygroupfcj/posts/2229938421104451?notif_id=1785478381072886&notif_t=tagged_with_story&ref=notif)

**References:**
- [Terraform AWS Provider Docs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Terraform Recommended Best Practices](https://developer.hashicorp.com/terraform/tutorials)
- [AWS Backend S3 & DynamoDB](https://developer.hashicorp.com/terraform/language/settings/backends/s3)