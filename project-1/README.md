# Project 1: Infrastructure Automation with Terraform & Ansible

## Overview
This project demonstrates the implementation of Infrastructure as Code (IaC) using Terraform for AWS resource provisioning and Ansible for configuration management. The infrastructure consists of multiple EC2 instances configured with different software stacks.

## Project Structure
```
project-1/
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   └── outputs.tf
├── ansible/
│   ├── inventory.yml
│   └── playbook.yml
├── screenshots/
│   ├── iam-roles.png
│   ├── instances.png
│   ├── terraform-execution.png
│   ├── ansible-setup.png
│   └── playbook-execution.png
└── README.md
```

## Implementation Details

### 1. Infrastructure Provisioning (Terraform)
- Created IAM roles for EC2 instances
- Provisioned 4 EC2 instances (1 master + 3 slaves)
- Configured security groups for SSH access
- Set up networking and access controls

### 2. Configuration Management (Ansible)
- Configured master-slave architecture
- Implemented role-based software distribution:
  - Slave1: Java + Python
  - Slave2: Java + MySQL
  - Slave3: MySQL + Python
- Automated installation and configuration process

## Prerequisites
- AWS Account with appropriate permissions
- Terraform installed (v1.0.0 or later)
- Ansible installed (v2.9 or later)
- AWS CLI configured with credentials

## Setup Instructions

### 1. Terraform Setup
```bash
cd terraform
terraform init
terraform plan
terraform apply
```

### 2. Ansible Setup
```bash
cd ansible
# Update inventory.yml with your EC2 instance IPs
ansible-playbook -i inventory.yml playbook.yml
```

## Screenshots
- IAM Roles Configuration
- EC2 Instances Creation
- Terraform Execution
- Ansible Configuration
- Playbook Execution Results

## Learning Outcomes
- Successfully implemented Infrastructure as Code
- Automated multi-instance deployment
- Configured different software stacks using Ansible
- Implemented secure access controls