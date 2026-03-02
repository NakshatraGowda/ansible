This project demonstrates infrastructure automation using ansible by provisioning and configuring nginx on AWS EC2 instances.

The setup ncludes:
- An ansible controller node(ubuntu EC2)
- Multiple Target nodes(ubuntu EC2)
- Automated installation and configuration of Nginx
- Cloning a repository and deploying a static web page

This project was built to practice:
- Configuration management
- Infrastructure as Code (IaC)
- SSH-based automation
- AWS EC2 provisioning concepts


Architecture is very simple :
Controller Node -> SSH -> Target servers
Ansible Playbook -> Install nginx -> Clone Repo -> Restart service

Prerequisites:
- AWS account
- 1 EC2 instance (Controller) - Ubuntu
- 1 or more EC2 instances (target servers) - ubuntu
- Same key pair used for all instances
- Ansible installed on controller

Setup and execution steps
1. Launch EC2 instances
    - Create one ubuntu EC2 instance (controller)
    - Create one or more ubuntu EC2 instances (Target servers).
    - Ensure:
        - Same key pair is used
        - security group allows:
            a. Port 22 (SSH)
            b. Port 80 (HTTP)

2. Install ansible on controller 
    sudo apt update
    sudo apt install ansible -y

    Verify installation:
    ansible --version

3. Configuration inventory file
    Add target server IP addresses in the inventory file:
    [web]
<target-server-public-ip> ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/key.pem

4. Test connectivity
    Verify SSH connection between controller and target:
    ansible web -i inventory -m ping
    Expected Output:
    "ping": "pong"

5. Run ansible playbook
    execute the deployment playbook:
    ansible-playbook -i inventory nginx-deployment.yml

    This playbook will:
    - Install nginx
    - Enable and start nginx service
    - install git
    - clone the project repository
    - restart nginx

Expected outcome:
    After successfull execution:
    - Nginx will be installed and running
    - The static website will be deployed on each target server
    - Access the application via:
        http://<target-server-public-ip>