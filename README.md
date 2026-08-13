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














