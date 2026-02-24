# AWS Service Control Policies (SCPs) – Setup & Implementation Guide

---

## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 12-02-2026 | v1.0 | Suraj Tripathi | 12-02-2026 |              | Aniruddh    | Shreya S    | Ashwani |

---

## Table of Contents

1. Introduction  
2. What are AWS Service Control Policies?  
3. Why Use SCPs for Cost Optimization?  
4. SCP Workflow  
5. Step-by-Step Setup Guide  
6. Different Measures to Minimize AWS Account Cost (Using SCPs)  
7. Testing & Validation  
8. Advantages and Disadvantages  
9. Best Practices  
10. Conclusion  
11. Contact Information  
12. References  

---

# 1. Introduction

This document provides a complete step-by-step setup guide to implement AWS Service Control Policies (SCPs) using AWS Organizations.

The goal of this implementation is to:

- Enforce centralized governance
- Restrict high-cost services
- Prevent misuse of AWS resources
- Optimize AWS cost proactively
- Demonstrate the setup to reviewers

This guide follows AWS official documentation and best practices.

---

## 2. What are AWS Service Control Policies?

AWS Service Control Policies (SCPs) are guardrail policies that define the maximum available permissions for AWS accounts within an AWS Organization.

Key Points:

- SCPs do NOT grant permissions.
- SCPs only restrict permissions.
- SCPs apply to:
  - Root
  - Organizational Units (OUs)
  - Individual member accounts
- SCPs do NOT apply to the Management Account.
- Explicit Deny in SCP overrides IAM Allow.

---

## 3. Why Use SCPs for Cost Optimization?

SCPs prevent unnecessary spending before it happens.

Instead of reacting to high bills, SCPs:

- Block costly services (EMR, Redshift)
- Restrict large EC2 instance types
- Allow only approved regions
- Enforce tagging for cost tracking
- Prevent accidental production-level resource creation

SCPs act as preventive cost control guardrails.

---

## 4. SCP Workflow

Workflow:

1. Cloud Admin creates SCP in Management Account.
2. SCP is attached to Root / OU / Account.
3. User attempts an action (e.g., Launch EC2).
4. AWS evaluates SCP first.
5. If SCP denies → Request blocked immediately.
6. If SCP allows → IAM policies are evaluated.

Important:

If SCP denies an action, IAM permission cannot override it.

---

## 5. Step-by-Step Setup Guide

----------------------------------------
PHASE 1 – Enable AWS Organizations
----------------------------------------

Step 1: Login to AWS Management Account

Go to:
AWS Console → AWS Organizations

Step 2: Create Organization

- Click Create Organization
- Choose Enable All Features
- Confirm setup
<img width="1918" height="500" alt="image" src="https://github.com/user-attachments/assets/9d28996d-4ee0-4c25-a411-0a577b5ed473" />

Now AWS Organization is active.

----------------------------------------
PHASE 2 – Create Organizational Units (OU)
----------------------------------------

Recommended Structure:

Root  
├── Production-OU  
├── Dev-OU  
└── Sandbox-OU  

Steps:

1. Select Root
2. Click Create Organizational Unit
3. Enter Name (e.g., Dev-OU)
4. Click Create
<img width="1898" height="788" alt="image" src="https://github.com/user-attachments/assets/9c5d0380-d42a-438e-8704-121827afb4a7" />

Repeat for required OUs.

----------------------------------------
PHASE 3 – Understand Default SCP
----------------------------------------

By default, AWS attaches:

FullAWSAccess

This allows all services.

Do NOT remove this unless implementing strict allow-list model.

----------------------------------------
PHASE 4 – Create Service Control Policy
----------------------------------------

Go to:

AWS Organizations → Policies → Service Control Policies

Click:

Create Policy

Enter:
- Policy Name
- Description
- JSON policy
<img width="1877" height="797" alt="image" src="https://github.com/user-attachments/assets/58ff481f-b904-4b0c-ace0-90f1467558b3" />


----------------------------------------
Example 1 – Restrict Region Usage
----------------------------------------

Allow only Mumbai region (ap-south-1):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyOutsideApprovedRegion",
      "Effect": "Deny",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "StringNotEquals": {
          "aws:RequestedRegion": "ap-south-1"
        }
      }
    }
  ]
}
```

----------------------------------------
Example 2 – Block Large EC2 Instances
----------------------------------------

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyLargeInstances",
      "Effect": "Deny",
      "Action": "ec2:RunInstances",
      "Resource": "*",
      "Condition": {
        "StringLike": {
          "ec2:InstanceType": [
            "p*",
            "x*",
            "*.8xlarge",
            "*.12xlarge"
          ]
        }
      }
    }
  ]
}
```

----------------------------------------
Example 3 – Deny High-Cost Services
----------------------------------------

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyExpensiveServices",
      "Effect": "Deny",
      "Action": [
        "elasticmapreduce:*",
        "redshift:*"
      ],
      "Resource": "*"
    }
  ]
}
```
<img width="1895" height="687" alt="image" src="https://github.com/user-attachments/assets/20e792ba-5445-4bb8-9f11-b23a6121a8dc" />


----------------------------------------
PHASE 5 – Attach SCP to OU
----------------------------------------

1. Go to AWS Organizations
2. Select OU (e.g., Dev-OU)
3. Click Policies
4. Click Attach
5. Select created SCP
6. Confirm attachment
<img width="1911" height="817" alt="image" src="https://github.com/user-attachments/assets/b2eb0d88-3958-4be7-a211-aade8ded66e8" />


SCP is now active.

----------------------------------------
PHASE 6 – Move Account to OU
----------------------------------------

1. Go to Accounts
2. Select Member Account
3. Click Move
4. Choose target OU
5. Confirm
<img width="1219" height="203" alt="image" src="https://github.com/user-attachments/assets/5c774876-1038-48ad-b637-a582ac683c72" />
<img width="1918" height="746" alt="image" src="https://github.com/user-attachments/assets/748e3810-160c-4ae8-8585-2d49f2f1e858" />

Now SCP applies to that account.

---

## 6. Different Measures to Minimize AWS Account Cost (Using SCPs)

| Measure | Description | Example |
|----------|-------------|----------|
| Restrict costly services | Block expensive services | Deny EMR |
| Region restriction | Limit resource creation | Allow only ap-south-1 |
| Limit EC2 types | Block GPU & high compute | Deny p*, x* |
| Enforce mandatory tags | Ensure cost tracking | Require CostCenter tag |
| Control IAM privilege escalation | Prevent admin misuse | Deny iam:CreatePolicy |
| Protect billing | Restrict billing access | Allow only finance role |
| Prevent public S3 | Avoid data leak risk | Deny s3:PutBucketAcl |

---

## 7. Testing & Validation

Login to Member Account and test:

Test 1:
Launch EC2 in us-east-1  
Expected: Denied
<img width="1918" height="746" alt="image" src="https://github.com/user-attachments/assets/41304aa0-d3cd-4756-8a51-d69dba45d5a3" />


Test 2:
Launch p3.2xlarge  
Expected: Denied
<img width="1366" height="731" alt="image" src="https://github.com/user-attachments/assets/1e7adcb2-e9f3-43bd-9333-ae65be360a31" />


Test 3:
Launch redshift  
Expected: Denied
<img width="1366" height="730" alt="image" src="https://github.com/user-attachments/assets/10de30a3-0be2-484c-bfcb-13fb30b65783" />


Verification:

- Check CloudTrail for denied events
- Confirm error message: "Explicit deny by SCP"

---

## 8. Advantages and Disadvantages

| Advantages | Disadvantages |
|------------|--------------|
| Centralized control | Incorrect SCP may block services |
| Prevents high cost | Needs testing |
| Strong governance | Cannot grant permissions |
| Automatic enforcement | Requires planning |

---

## 9. Best Practices

- Always test SCP in Sandbox first.
- Use Deny-based model (safer).
- Do not apply strict SCP directly to Root.
- Keep break-glass admin account.
- Document each SCP with:
  - Owner
  - Purpose
  - Date
- Review policies quarterly.
- Combine with:
  - AWS Budgets
  - Cost Explorer
  - Right sizing
  - Spot Instances

---

## 10. Conclusion

AWS Service Control Policies provide centralized governance across multiple AWS accounts.

When properly implemented, SCPs:

- Prevent unnecessary AWS spending
- Improve security posture
- Standardize account usage
- Enforce cost optimization policies

SCPs define the maximum permission boundary and act as preventive guardrails.

---

## 11. Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |

---

## 12. References

- AWS Service Control Policies Official Documentation  
  https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html

- AWS Organizations Documentation  
  https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html

---
