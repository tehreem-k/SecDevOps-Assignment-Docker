# Spring Boot Dockerized Application

This repository contains a minimal Spring Boot web application that has been Dockerized and can run on any Linux host, including an AWS EC2 instance.

The application responds to `/` with a simple message:  
`Docker Spring App is running!`

---

## Table of Contents
1. [Prerequisites](#prerequisites)  
2. [Install Docker on Linux](#install-docker-on-linux)  
3. [Build and Run Locally](#build-and-run-locally)  
4. [Run on EC2](#run-on-ec2)  
5. [Optional: Push to Docker Hub](#optional-push-to-docker-hub)  
6. [Restart Policy / Production](#restart-policy--production)  

---

## Prerequisites
- Linux VM or EC2 instance (Ubuntu recommended)  
- Java 17 installed (handled in Docker image)  
- Docker installed on host  

---

## Install Docker on Linux (Ubuntu Example)

```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# verify docker installation and is running
docker --version
sudo systemctl status docker
```

---
Build and Run Locally
1. Clone repository
git clone <your-repo-url>
cd spring-docker-app

2. Build Docker image
docker build -t spring-docker-app:latest .


Sample output:

BUILD SUCCESSFUL in 25s

3. Run container
docker run -d -p 5000:5000 --name spring-app spring-docker-app:latest

4. Verify application
curl http://localhost:5000


Expected output:

Docker Spring App is running!

Run on EC2

Open TCP port 5000 in the EC2 security group.

Ensure Spring Boot binds to all interfaces (0.0.0.0) — handled in Dockerfile.

Run container as above:

docker run -d -p 5000:5000 --name spring-app spring-docker-app:latest


Access via browser using the EC2 public IP:

http://<EC2-public-IP>:5000/
