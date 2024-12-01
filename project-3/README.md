Here's a **README.md** file for your assignment:

---

# DevOps Assignment: Pipeline Creation for Website Deployment

## Objective

The objective of this assignment is to create a pipeline for the deployment of a website using Terraform, Ansible, and Jenkins.

---

## Prerequisites

1. **Terraform** installed on a manually created instance.
2. AWS account with permissions to create EC2 instances.
3. SSH key pair for password-less connections.
4. Ansible installed on the master machine.

---

## Steps to Implement

### 1. Manual Setup
- Launch an EC2 instance manually and install Terraform on it:
  ```bash
  sudo apt update
  sudo apt install -y gnupg software-properties-common curl
  curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
  echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
  sudo apt update
  sudo apt install terraform
  terraform --version
  ```

---

### 2. Terraform Configuration
- Write a `main.tf` file to create 3 EC2 instances in the default VPC and Subnet.
- Ensure you provide the path to the user data script:
  ```hcl
  provider "aws" {
    region = "us-east-1"
  }

  resource "aws_instance" "example" {
    count         = 3
    ami           = "ami-0c02fb55956c7d316"
    instance_type = "t2.micro"
    key_name      = "your-key-name"

    user_data = file("user_data.sh")

    tags = {
      Name = "Instance-${count.index + 1}"
    }
  }
  ```
- Commands to execute:
  ```bash
  terraform init
  terraform plan
  terraform apply
  ```

---

### 3. User Data Script
- Create a `user_data.sh` script for initial setup:
  ```bash
  #!/bin/bash
  apt update
  apt install -y ansible
  ```

---

### 4. Ansible Setup
- Install Ansible on one instance to act as the master.
- Configure password-less SSH for the two slave machines:
  ```bash
  ssh-keygen -t rsa
  ssh-copy-id user@slave-ip-1
  ssh-copy-id user@slave-ip-2
  ```
- Update `/etc/ansible/hosts`:
  ```bash
  echo "slave1 ansible_host=slave-ip-1 ansible_user=ubuntu" | sudo tee -a /etc/ansible/hosts
  echo "slave2 ansible_host=slave-ip-2 ansible_user=ubuntu" | sudo tee -a /etc/ansible/hosts
  ```

---

### 5. Ansible Playbook
- Write a playbook `install_java_jenkins.yml`:
  ```yaml
  ---
  - name: Setup Java and Jenkins
    hosts: slave1
    tasks:
      - name: Install Java
        apt:
          name: default-jdk
          state: present
      - name: Install Jenkins
        apt:
          name: jenkins
          state: present

  - name: Setup Java Only
    hosts: slave2
    tasks:
      - name: Install Java
        apt:
          name: default-jdk
          state: present
  ```
- Run the playbook:
  ```bash
  ansible-playbook install_java_jenkins.yml
  ```

---

### 6. Jenkins Setup
- Access Jenkins on Slave 1: `http://<slave-ip-1>:8080`.
- Complete setup using the initial admin password (`/var/lib/jenkins/secrets/initialAdminPassword`).
- Add Slave 2 as a **Jenkins Agent**:
  - Navigate to **Manage Jenkins > Manage Nodes and Clouds > New Node**.
  - Configure SSH credentials for the agent.

---

### 7. Jenkins Pipeline Job
- Create a Jenkins pipeline job using the following script:
  ```groovy
  pipeline {
      agent any

      stages {
          stage('Clone Repository') {
              steps {
                  git branch: 'main', url: 'https://github.com/mdn/beginner-html-site-styled'
              }
          }
      }
  }
  ```

---

## Repository URL
The GitHub repository to be cloned:
[https://github.com/mdn/beginner-html-site-styled](https://github.com/mdn/beginner-html-site-styled)

---

## Deliverables
1. `main.tf` (Terraform configuration file).
2. `user_data.sh` script.
3. `install_java_jenkins.yml` (Ansible Playbook).
4. Screenshots or logs for:
   - Terraform execution.
   - Ansible playbook run.
   - Jenkins setup and pipeline execution.

---

## Notes
- Ensure all configurations are properly secured, including key management.
- Use default VPC and Subnet to avoid loss of marks.

--- 

This README file documents all steps for successful implementation of the assignment. Let me know if you need any adjustments!