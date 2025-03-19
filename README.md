# MemoryLane Application Infrastructure

This CloudFormation template creates a comprehensive AWS infrastructure for a containerized application with S3 access, featuring blue-green deployments via CodeDeploy.

## Architecture Overview

- **Networking**: VPC with public and private subnets across 2 availability zones
- **Compute**: ECS Fargate service with auto-scaling
- **Load Balancing**: Application Load Balancer with blue-green deployment configuration
- **CI/CD**: CodeDeploy for zero-downtime deployments
- **Security**: IAM roles with least privilege permissions

## Resources Created

### Networking

- VPC with CIDR block `10.0.0.0/16`
- 2 public subnets for the load balancer
- 2 private subnets for the ECS service
- NAT Gateway for outbound internet access from private subnets
- Internet Gateway for public subnet internet access

### Compute

- ECS Cluster with Fargate launch type
- Auto-scaling configuration based on CPU utilization
- Container runs on port `3000`

### Load Balancing

- Application Load Balancer with:
  - Production listener (port `80`)
  - Test listener (port `8081`) for validating new deployments
- Blue and green target groups for zero-downtime deployments

### Security

- IAM roles for task execution and S3 access
- Security groups for load balancer and ECS service

### CI/CD

- CodeDeploy application and deployment group
- Blue-green deployment configuration

## Outputs

- Load Balancer DNS name and URL
- CodeDeploy application and deployment group names

## Usage

Deploy this template using the AWS CloudFormation console or AWS CLI:

```bash
aws cloudformation create-stack --stack-name s3-application-stack --template-body file://template.yaml --capabilities CAPABILITY_IAM

## After deployment, you can access the application through the load balancer URL provided in the outputs.
