# Project 3: Infrastructure Automation with Terraform, Ansible, and Jenkins

## Project Overview
This project demonstrates a complete infrastructure automation solution using Terraform for provisioning, Ansible for configuration management, and Jenkins for CI/CD pipeline implementation.

## Architecture
- Terraform manages AWS infrastructure
- Ansible handles configuration management
- Jenkins provides CI/CD capabilities
- Multi-node setup with 1 master and 2 slave nodes

## Project Structure
```
project-3/
├── terraform/
│   └── main.tf                # AWS infrastructure configuration
├── ansible/
│   ├── inventory.yml          # Host inventory configuration
│   └── playbook.yml          # Ansible automation playbook
├── scripts/
│   └── user_data.sh          # EC2 instance initialization script
├── screenshots/              # Implementation documentation
└── README.md
```

## Implementation Steps

### 1. Infrastructure Provisioning (Terraform)
- Create security group for required ports (22, 80, 8080)
- Launch 3 EC2 instances (1 master, 2 slaves)
- Configure user data for initial setup
- Output instance IPs for further configuration

### 2. Configuration Management (Ansible)
- Configure Jenkins master node
- Set up Java environment on all nodes
- Install and configure Jenkins on master
- Prepare slave nodes for Jenkins agent setup

### 3. CI/CD Setup (Jenkins)
- Configure Jenkins master-slave architecture
- Set up build agents
- Create and configure pipeline
- Implement automated deployment

## Security Configurations
- Restricted security group access
- SSH key-based authentication
- Jenkins security best practices
- Proper user management

## Implementation Screenshots

1. Infrastructure Setup
   - [Terraform Instance Creation](./screenshots/01-terraform-instances.png)
   - [Ansible Installation](./screenshots/02-ansible-installation.png)
   - [Ansible Configuration](./screenshots/03-ansible-configuration.png)

2. Jenkins Configuration
   - [Jenkins Service Status](./screenshots/04-jenkins-service.png)
   - [Jenkins Dashboard](./screenshots/05-jenkins-dashboard.png)
   - [Jenkins Nodes Setup](./screenshots/06-jenkins-nodes.png)
   - [Jenkins Pipeline](./screenshots/07-jenkins-pipeline.png)

3. Deployment
   - [Final Deployment](./screenshots/08-deployment-output.png)

## Prerequisites
- AWS Account with appropriate permissions
- Terraform installed (v1.0.0 or later)
- Ansible installed (v2.9 or later)
- SSH key pair for EC2 instances

## Setup Instructions

### 1. Infrastructure Setup
```bash
cd terraform
terraform init
terraform plan
terraform apply
```

### 2. Ansible Configuration
```bash
cd ansible
# Update inventory.yml with actual IPs
ansible-playbook -i inventory.yml playbook.yml
```

### 3. Jenkins Setup
- Access Jenkins UI: http://<master-ip>:8080
- Complete initial setup using admin password
- Configure build agents using slave node IPs
- Set up pipeline job

## Notes
- Ensure all security group ports are properly configured
- Keep SSH keys secure and never commit them to Git
- Update inventory.yml with actual IPs after infrastructure creation
- Follow Jenkins security best practices

## Troubleshooting
- Check security group configurations if connection issues occur
- Verify SSH key permissions
- Ensure all required ports are open
- Check instance user data logs if setup fails