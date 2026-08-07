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

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/6a5fe926511838917e37649f719f5ecb806851a3/img/Add%20ubuntu%20usr.png)

# Step 4 Pull Jenkins Docker Image
docker pull jenkins/jenkins:lts

Check

docker images

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/8ab9484f089ce49d2527b66ce915b5275bb3f952/img/Pull%20Jenkins%20Image.png)

# Step 5 Create Jenkins Container
docker run -d \
--name jenkins \
-p 8080:8080 \
-p 50000:50000 \
-v jenkins_home:/var/jenkins_home \
jenkins/jenkins:lts

Check

docker ps

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/321a40564431cd5e29b283d1d95b698378f3c481/img/Create%20Jenkins%20container.png)

# Step 6: Open Jenkins

Browser

http://Public-IP:8080

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/409197ac0224c99420a52bdab62d1e6c5f50ce9f/img/Open%20jenkins.png)

# Step 7: Unlock Jenkins
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
Copy password.

Paste in browser.

Install Suggested Plugins.

Create Admin User.
![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/bfdad0623222ef9bab860697c17d21931a000a56/img/Unlock%20Jenkins.png)

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/8256f4bdc8d5667cd4479f29aa76f3461560b89a/img/Insatll%20suggested%20plugins.png)

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/758ee9dffa900652a7a1b474fcf327c6818e3710/img/Create%20user.png)

# Step 8: Install Required Plugins

Go

Manage Jenkins

↓

Plugins

Install

Git

Pipeline

Docker Pipeline

Docker

GitHub

Maven Integration

Restart Jenkins.
![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/5ad8b3ecce616293007c869c4533491a599a973c/img/Plugin%20Installation.png)

# Step 9 Install Docker Inside Jenkins Container




