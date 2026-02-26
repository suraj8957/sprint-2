# Cloud Infrastructure Design – Development Environment (AWS)

---

# 1. Purpose

This contains the detailed design documentation for a Cloud Infrastructure built on Amazon Web Services (AWS) for a Development (DEV) environment.

The infrastructure is designed following industry best practices, AWS Well-Architected Framework principles, and enterprise security standards.

This document explains the concept of Cloud Infrastructure Design from basic to advanced and provides a production-aligned development environment setup.

---

# 2. What is Cloud Infrastructure Design?

Cloud Infrastructure Design is the process of architecting and organizing cloud resources (network, compute, storage, security, monitoring) in a structured, secure, scalable, and cost-optimized manner.

It includes:

- Network design (VPC, Subnets, Routing)
- Compute resource planning
- Database architecture
- Security implementation
- Monitoring & logging
- High availability planning
- Disaster recovery strategy
- Cost optimization

A well-designed infrastructure ensures:

- Security
- Scalability
- Reliability
- Performance
- Cost efficiency
- Operational excellence

---

# 3. Why Cloud Infrastructure Design is Important?

Proper cloud design:

- Prevents security vulnerabilities
- Reduces downtime
- Optimizes cost
- Supports scaling
- Improves system reliability
- Aligns development and production environments

Without proper design, cloud environments can become insecure, expensive, and difficult to manage.

---

# 4. Architecture Overview

This infrastructure follows a Three-Tier Architecture:

1. Presentation Layer (Public Subnet)
2. Application Layer (Private Subnet)
3. Database Layer (Private Subnet - Isolated)

Flow:

Internet  
→ Application Load Balancer  
→ Application Servers  
→ Database  

---

# 5. Cloud Provider

Cloud Provider: Amazon Web Services (AWS)  
Region: ap-south-1 (Mumbai)  
Availability Zones: ap-south-1a, ap-south-1b  

AWS services used:

- Amazon VPC
- EC2
- Application Load Balancer
- RDS
- IAM
- CloudWatch
- CloudTrail

---

# 6. Network Design

## 6.1 VPC

- CIDR: 10.0.0.0/16
- DNS enabled
- Provides network isolation

## 6.2 Subnet Structure

Public Subnets:
- Used for Load Balancer
- Internet accessible

Private App Subnets:
- Host application servers
- Not publicly accessible

Private DB Subnets:
- Host database
- Strictly isolated

## 6.3 Internet Gateway

Allows public subnet to communicate with internet.

## 6.4 NAT Gateway

Allows private instances outbound internet access without exposing them publicly.

---

# 7. Compute Layer

EC2 instances host the application.

Instance Type: t3.micro (DEV optimized)  
Auto Scaling enabled  
Minimum: 1  
Maximum: 3  

Purpose:
- Host backend services
- Handle application logic
- Scale based on traffic

---

# 8. Load Balancer

Application Load Balancer (ALB)

- Listens on HTTP (80) and HTTPS (443)
- Performs SSL termination
- Distributes traffic across instances
- Performs health checks

Benefits:
- High availability
- Improved reliability
- Traffic management

---

# 9. Database Layer

Amazon RDS (MySQL / PostgreSQL)

- Private subnet deployment
- Public access disabled
- Automated backups
- Encryption enabled
- Single-AZ (DEV) or Multi-AZ (Optional)

Benefits:
- Managed service
- Automated patching
- Failover support
- Reduced operational burden

---

# 10. Security Architecture

## 10.1 IAM

- Role-Based Access Control
- Least privilege policy
- MFA enabled
- No direct root usage

## 10.2 Security Groups (Stateful Firewall)

ALB:
- 80, 443 from internet

App Servers:
- 80 from ALB
- 22 from Bastion

Database:
- 3306 from App SG only

## 10.3 Network ACL (Stateless)

- Public subnet allows HTTP/HTTPS
- Private subnets restrict external traffic
- Internal traffic allowed as required

## 10.4 Encryption

- EBS encryption
- RDS encryption
- HTTPS enforced
- Secrets managed securely

---

# 11. High Availability

- Multi-AZ App deployment
- Load Balancer health checks
- Auto Scaling
- RDS Multi-AZ (Optional in DEV)

---

# 12. Disaster Recovery Strategy

- RDS automated backups
- EBS snapshots
- AMI backups
- Infrastructure as Code for redeployment

RTO: < 2 Hours  
RPO: < 30 Minutes  

---

# 13. Monitoring & Logging

Monitoring:
- CloudWatch Metrics
- CPU & Memory alarms
- Health checks

Logging:
- CloudTrail (Audit logs)
- VPC Flow Logs
- ALB Access Logs
- Application Logs

---

# 14. Cost Optimization Strategy

- Small instance sizes (DEV)
- Auto Scaling
- Scheduled shutdown
- Monitoring unused resources
- gp3 storage type

---

# 15. DevOps Readiness

Infrastructure supports:

- CI/CD integration
- Infrastructure as Code (Terraform recommended)
- Git version control
- Automated deployments
- Blue-Green deployment (future scope)

---

# 16. Resource Justification

| Resource | Reason |
|----------|--------|
| VPC | Network isolation |
| Subnets | Layer separation |
| ALB | Traffic distribution |
| EC2 | Application hosting |
| RDS | Managed database |
| NAT Gateway | Secure outbound access |
| IAM | Secure access control |

---

# 17. Conclusion

This AWS-based Development Cloud Infrastructure:

- Follows industry best practices
- Aligns with AWS Well-Architected Framework
- Ensures security and scalability
- Optimizes cost for development
- Mirrors production architecture in simplified form

It provides a structured, secure, and scalable cloud environment ready for DevOps workflows.

---

# 18. References

AWS Well-Architected Framework  
https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html  

Amazon VPC Documentation  
https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html  

Amazon EC2 Documentation  
https://docs.aws.amazon.com/ec2/index.html  

Elastic Load Balancing Documentation  
https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html  

Amazon RDS Documentation  
https://docs.aws.amazon.com/rds/index.html  

AWS IAM Documentation  
https://docs.aws.amazon.com/iam/index.html  

AWS CloudWatch Documentation  
https://docs.aws.amazon.com/cloudwatch/index.html  

AWS CloudTrail Documentation  
https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html  

---
