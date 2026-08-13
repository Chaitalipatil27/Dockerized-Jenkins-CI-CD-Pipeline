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

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/ad92d0b45e405b9a9d8e6d8583740f867eb15bca/img/Create%20web.xml.png)

Create pom.xml

Go to the project root:

cd ~/dockerized-jenkins-cicd

Create:

nano pom.xml

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/1694ecbb9a522b8e2da1707e74eb4c0ccf3d8903/img/Create%20pom.xml.png)

Build the application

Now run:

mvn clean package

Maven will do:

pom.xml
   ↓
Compile/build
   ↓
Package WAR
   ↓
target/app.war

At the end you want:

BUILD SUCCESS

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/d5434311994fb12a15202aedb6ae5c28b1af1d40/img/mvn%20clean%20package.png)

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/d9704c446973a7b41e59469c9a4275797aa43e7b/img/Build%20Success.png)

Check the WAR file

Run:

ls

should see:

pom.xml
src
target

Then:

ls target

should see:

app.war

This is important because later our Dockerfile will copy:

target/app.war

into the Tomcat container.

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/cdb7a692efebc7daa8d584db7d27dfb1f154fe18/img/Check%20the%20WAR%20file.png)

Check the complete project

Run

find .

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/16711bb09b8d8f9cd4a2c5e0a63cadac399dcf41/img/Check%20the%20complete%20project.png)

# STEP 8: Create Dockerfile and Run Your Application in Docker

Make sure you are in the project folder

Run

pwd 

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/25dea405e5b87c180c49f4bcd8d06afb12a4c3f9/img/Make%20sure%20you%20are%20in%20the%20project%20folder.png)

Create the Dockerfile

Run:

nano Dockerfile

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/d9a5c835b25baacce3ee736b8539866f4621b034/img/Create%20the%20Dockerfile.png)

Build the Docker image

Now we create the Docker image.

Run:

docker build -t dockerized-app:1.0 .

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/c75f157e4b36173c7c812504574f1cc5511f5cf0/img/Build%20the%20Docker%20image.png)

Check the Docker image

Run:

docker images

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/b33d26bb730fca3b6361427b1295ef551512ef9e/img/Check%20the%20Docker%20image.png)

Run the application container

Now run:

docker run -d --name dockerized-app-container -p 8081:8080 dockerized-app:1.0

Check the container

Run:

docker ps

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/2a1915cb895b4fb127e9b81fbbdebd62b84c5deb/img/Run%20the%20application%20container.png)

# Access from your Windows browser

Remember the Public IPv4 address of your EC2.

Open your Windows browser and enter:

http://YOUR_EC2_PUBLIC_IP:8081/app/

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/dcc3db93973ac2a7ea1eca696eebd736a195d060/img/Access%20from%20your%20Windows%20browser.png)

# STEP 9: Install Jenkins Inside Docker on EC2

Our architecture becomes:

                    AWS EC2
                       │
                 Docker Engine
                       │
          ┌────────────┴────────────┐
          │                         │
     Jenkins Container       Application Container
          │                         │
       Port 8080                 Port 8081

Check that your application container is running

First run:

docker ps

You should see:

dockerized-app-container

with:

0.0.0.0:8081->8080/tcp
 
![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/ae370b9bb8e5928b2f2906e0713b3db91e5e6bf0/img/Check%20that%20your%20application%20container%20is%20running.png)

Create Jenkins Docker volume

We need persistent storage for Jenkins.

Run:

docker volume create jenkins_home

should get:

jenkins_home

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/e629e9418bc3390bdb0efb2e43eb0cb1a0d4a9f3/img/Create%20Jenkins%20Docker%20volume.png)

Download Jenkins image

Run:

docker pull jenkins/jenkins:lts

Docker will download the official Jenkins LTS image.

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/b27aba2ca489847cd3622e762310292ebb9fff7a/img/Download%20Jenkins%20image.png)

Create Jenkins container

Now run:

docker run -d \
  --name jenkins \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins/jenkins:lts

  ![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/fab1d8ada36f6a66a5384f173c86a1a2ee4457f4/img/Create%20Jenkins%20container.png)

Check Jenkins container

Run:

docker ps

should see two containers:

jenkins
dockerized-app-container

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/b69c9576092e1fd30da8e55ae458a9f1cbead181/img/Check%20Jenkins%20container.png)

Get the Jenkins initial password

Jenkins needs an administrator password during the first setup.

Run:

docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword

![image alt](https://github.com/Chaitalipatil27/Dockerized-Jenkins-CI-CD-Pipeline/blob/332d123aec330c87778324ec3d9a37ec82d255e4/img/Get%20the%20Jenkins%20initial%20password.png)





