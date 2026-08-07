# Project Name
# Dockerized-Jenkins-CI-CD-Pipeline
Project Objective

Automatically build and deploy an application whenever code is pushed to GitHub using Jenkins running inside Docker.
# Architecture
 Developer
      │
 GitHub Repository
      │
 Jenkins (Docker Container)
      │
 Build Docker Image
      │
 Run Docker Container
      │
 Application Running

# Why is this project required?

In many companies:

Developers write code every day.
Manually building and deploying is slow.
Manual deployment causes mistakes.
Different environments behave differently.

To solve this problem companies use:

GitHub
Jenkins
Docker
CI/CD Pipeline

This automates the complete deployment process.

# Step 1: Launch an Ubuntu Server

You need a Linux machine (Ubuntu 22.04 LTS).

This can be:

AWS EC2 Ubuntu instance
VirtualBox Ubuntu VM
VMware Ubuntu VM

Minimum requirements:

2 GB RAM
20 GB Storage

Connect to the server using SSH:

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/6387e5cf94fed169580649a679a1a5b2f6979d22/img/Create%20Instance.png)

# Step 2: Update Server 
apt update
![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/337902b62c45bce441fdfb1c6eb97b951d810f65/img/apt%20update.png)

# Step 3: Install Docker
apt install docker.io -y

# Enable Docker

systemctl enable docker

systemctl start docker

Verify

docker --version

# Add Ubuntu user to Docker group

usermod -aG docker ubuntu
![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/0c71be3eda65a44e135c421924607729c30d9147/img/Install%20Docker.png)

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/10087f234ee8eb90934b3c2216881eeccb975ffa/img/Enable%20and%20start%20docker.png)




