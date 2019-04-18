#tanya-ro
#Created by Tanya Stephens
#Last Update - 4/17/19

This repo contains the files to complete the challenge.

A properly configured Ansible host is required. In addition, the user must have sudo privileges.

These instructions are for an Ubuntu installation with a username of ubuntu.

# Create user ubuntu and add to sudo users (if necessary)
The commands should be run as root user

Commands
- adduser ubuntu
- usermod -aG sudo ubuntu

Exit as root user

# Install Software
Commands
- sudo apt-get update
- sudo apt install python-pip -y
- sudo pip install --upgrade pip
- sudo apt-get install software-properties-common
- sudo add-apt-repository ppa:ansible/ansible
- sudo apt-get update
- sudo apt-get install ansible -y
- sudo apt install python -y
- sudo pip install boto
- sudo pip install botocore
- sudo pip install boto3
- sudo apt-get update
- sudo pip install awscli --upgrade
- sudo apt-get update
- sudo apt-get install git -y
- sudo apt-get update

# Change to home directory of the Ubuntu user
- cd /home/ubuntu

# Clone the Repo
- git clone https://github.com/tanyawms/tanya-ro1

# Change to the Repo directory
- cd /home/ubuntu/tanya-ro1

# Move the ansible directory
- mv ansible ../

# Create SSH keys
- ssh-agent bash

### Accept the default location and value of id_rsa and do not enter a passphrase
- ssh-keygen 

# Copy the AWS Keypair from the Repo
- cd ~/.ssh
- cp /home/ubuntu/tanya-ro1/.ssh/tas_react1.pem ./
- chmod 600 tas_react1.pem

# Add the SSH keys
- ssh-add ~/.ssh/id_rsa
- ssh-add ~/.ssh/tas_react1.pem

# Verify addition of SSH keys
- ssh-add -l

# Remove unused Repo files
- sudo rm -r /home/ubuntu/tanya-ro1

# Create a file with AWS credentials
- vi ~/.boto
### This is the file content
--  [Credentials]
--  aws_access_key_id = [your access key id]
--  aws_secret_access_key = [your secret access key]
  
# Run these commands as root
- wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py -O /etc/ansible/ec2.py
- wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.ini -O /etc/ansible/ec2.ini
- chmod +x /etc/ansible/ec2.py

# Edit /etc/ansible/ansible.cfg
Uncomment the line and/or make the change

- vi /etc/ansible/ansible.cfg
- inventory      = /home/ubuntu/ansible/hosts
- host_key_checking=False

Exit as root

# Run the playbook
- cd /home/ubuntu/ansible/CreatingEC2
- ansible-playbook deploy.yml -vv(optional)

# Get the IP address of the application
The IP address is listed in the PLAY RECAP. The application is at port 8080

#########  Application Rules  ##########
##### Easy - Guess numbers between 1 and 10     #####
##### Medium - Guess numbers between 1 and 100  #####
##### Hard - Guess numbers between 1 and 1000   #####
