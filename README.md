# AWS WordPress High Availability on AWS


This project demonstratess a highly available WordPress deployment on AWS by integrating multiple AWS services to achieve scalability, reliability, and fault tolerance.

## Architecture Overview
User traffic flows through the following components:

Route53 → Application Load Balancer → Auto Scaling EC2 Instances → RDS (MySQL)

## AWS Services Used
- Amazon EC2 – Hosts WordPress application
- Auto Scaling Group – Ensures high availability
- Application Load Balancer – Distributes traffic
- Amazon RDS (MySQL) – Managed database
- Amazon Route53 – Domain and DNS management

 | Service | Purpose |
|-------|--------|
| EC2 | Hosts WordPress application |
| Auto Scaling | Maintains availability |
| ALB | Distributes incoming traffic |
| RDS (MySQL) | Centralized database |
| Route53 | Domain and DNS routing |


## How the System Works
1. Users access the website using a custom domain.
2. Route53 routes traffic to the Application Load Balancer.
3. The Load Balancer forwards requests to EC2 instances.
4. Auto Scaling Group maintains availability during failures.
5. WordPress uses RDS as a centralized database.

## High Availability
- Multiple EC2 instances across availability zones
- Health checks via Application Load Balancer
- Automatic instance replacement using Auto Scaling


## Security Groups (Traffic Rules)

This deployment follows least-privilege rules between AWS components:

### 1: ALB Security Group (Public)
**Inbound**
- HTTP (80) from `0.0.0.0/0`
- HTTPS (443) from `0.0.0.0/0` (if using SSL)

**Outbound**
- HTTP (80) to EC2 Security Group

### 2: EC2 Security Group (Private App Tier)
**Inbound**
- HTTP (80) from ALB Security Group only
- SSH (22) from My IP only (optional for admin)

**Outbound**
- MySQL (3306) to RDS Security Group

### 3: RDS Security Group (Database Tier)
**Inbound**
- MySQL (3306) from EC2 Security Group only

**Outbound**
- Default (or restricted as per AWS defaults)
  
## Failure Scenario Test
To validate high availability, an EC2 instance was manually terminated.
The Auto Scaling Group automatically launched a new instance, which was registered as healthy in the Application Load Balancer.
The WordPress website remained accessible during the process.


## Outcome
This setup ensures that the WordPress website remains available even if individual EC2 instances fail.
