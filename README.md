# 🔧 Hello-World Ansible Nginx Deployment

> This repository demonstrates **infrastructure automation** with Ansible by provisioning and configuring Nginx on AWS EC2 instances.

<br/>

## 🚀 Overview

A simple architecture:

```
Controller Node ↔ SSH ↔ Target Servers
       │
Ansible Playbook: install nginx → clone repo → restart service
```

**Key components:**

- Ansible controller (Ubuntu EC2)
- One or more target Ubuntu EC2 servers
- Automated Nginx installation and configuration
- Static web site deployment from a Git repository

<br/>

## 📦 Features

- Configuration management with Ansible
- Infrastructure as Code (IaC) workflow
- SSH‑based automation across EC2 instances
- Hands‑on AWS EC2 provisioning concepts

<br/>

## ✅ Prerequisites

- AWS account
- Ansible installed on the controller node
- EC2 instances:
  - 1 controller (Ubuntu)
  - ≥1 target servers (Ubuntu)
- Same SSH key pair for all instances
- Security group allowing:
  - Port **22** (SSH)
  - Port **80** (HTTP)

<br/>

## 🛠️ Setup & Execution

1. **Launch EC2 instances**
   - Create Ubuntu instances for controller and targets.
   - Verify the shared key pair and security group ports.

2. **Install Ansible on controller**
   ```bash
   sudo apt update
   sudo apt install ansible -y
   ansible --version        # verify installation
   ```

3. **Edit inventory file** (`ansible/inventory`):
   ```ini
   [web]
   <target-server-public-ip> ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/key.pem
   ```

4. **Test connectivity**
   ```bash
   ansible web -i ansible/inventory -m ping
   # expected output: "pong"
   ```

5. **Run deployment playbook**
   ```bash
   ansible-playbook -i ansible/inventory ansible/nginx-deployment.yml
   ```
   The playbook will:
   - install and start Nginx
   - install Git
   - clone this project's repo
   - restart the Nginx service

<br/>

## 🎯 Expected Outcome

After successful execution:

- **Nginx** is running on each target server
- The **static website** from this repo is deployed
- Access via: `http://<target-server-public-ip>`

<br/>

## 📁 Repository Structure

```
├── ansible/
│   ├── inventory
│   ├── nginx-deployment.yml
│   └── templates/
│       └── nginx.conf.j2
├── index.html
└── README.md
```

<br/>

## 🤝 Contributing

Feel free to submit issues or pull requests. Add roles, extend playbooks, or improve docs!

<br/>

## 📝 License

Include your preferred license here (e.g., MIT, Apache 2.0).

<br/>

## 📬 Contact

For questions or support, reach out at `you@example.com` (replace with your email).
