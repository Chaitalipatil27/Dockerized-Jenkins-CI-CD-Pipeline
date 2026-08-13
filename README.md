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
![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/ce55ee25924b6820642f017904e83fb719da6bf3/img/Create%20Instance.png)

# Step 2: Update Ubuntu
sudo apt update
![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/2f6ecab985116e2e09bede5eaf8c996b791a7643/img/Update%20ubuntu%20.png)

# Step 3: Install Docker
sudo apt install docker.io -y
![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/c522229688973fcd67071db3e86837e555cfa4d3/img/Install%20docker.png)

# Step 4: Start and Unable docker,Check Docker status
sudo systemctl start docker

sudo systemctl enable docker

sudo systemctl status docker
![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/8736d56be0ecfa53dbed064ab090fd1689212332/img/Start%20and%20unable%20docker.png)

# Step 5:Allow the ubuntu user to run Docker
Normally Docker commands require:

sudo docker ...

We don't want to type sudo for every Jenkins/Docker command.

Run:

sudo usermod -aG docker $USER

Then apply the new group membership:

newgrp docker
![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/bee932ef82f969c89f7f5be89543085cf5bfc06c/img/Allow%20the%20ubuntu%20user%20to%20run%20Docker.png)

# STEP 6 — Install Git, Java 17, and Maven on EC2
Install Git

sudo apt install git -y

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/f2702279c9373d51c2368a176452f0b06be51ebd/img/Git%20Installation.png)

Install Java 17

sudo apt install openjdk-17-jdk -y
![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/f9e1816ab34658c4dd1fb8f963180976509c582f/img/Java%20Installation.png)

Check JAVA_HOME

Run:

readlink -f $(which java)

get something like:

/usr/lib/jvm/java-17-openjdk-amd64/bin/java

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/a3dd4910fac604c3021df1330bb1d7b80639fabc/img/Check%20JAVA_HOME.png)

Install Maven

sudo apt install maven -y

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/71bdf9f8c27f13b56f1c622df1f4b068f2ab570e/img/Maven%20Installation.png)

# STEP 7 — Create the Project on EC2

Create the main project folder

mkdir dockerized-jenkins-cicd

cd dockerized-jenkins-cicd

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/83232a5cf1f6fee2825d2c6cd4a593ddb0243dd9/img/Create%20folder%20dockerized-jenkins-cicd.png)

Create the application folders

mkdir -p src/main/webapp/WEB-INF

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/a6da73c73164c3b54aa2aa4b3792229e6cae2b32/img/Create%20folder.png)

Create index.jsp

nano src/main/webapp/index.jsp

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/7b660708427b3f8271976d17126a4d46740b88a1/img/Create%20index.jsp.png)

Create web.xml

nano src/main/webapp/WEB-INF/web.xml














