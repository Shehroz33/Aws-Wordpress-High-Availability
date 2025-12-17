# AWS WordPress High Availability Architecture

This project demonstrates a highly available WordPress deployment on AWS by connecting multiple AWS services to ensure scalability, reliability, and fault tolerance.

## Architecture Overview
User traffic flows through the following components:

Route53 → Application Load Balancer → Auto Scaling EC2 Instances → RDS (MySQL)

## AWS Services Used
- Amazon EC2 – Hosts WordPress application
- Auto Scaling Group – Ensures high availability
- Application Load Balancer – Distributes traffic
- Amazon RDS (MySQL) – Managed database
- Amazon Route53 – Domain and DNS management

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

## Proof of Deployment
Screenshots showing the AWS configuration and working WordPress site are available in the Docs/Screenshots directory.

## Automation
EC2 instances use a User Data script to automatically install and configure WordPress during launch.


## Outcome
This setup ensures that the WordPress website remains available even if individual EC2 instances fail.
