


# Spring Boot Dockerized Application

This repository contains a minimal Spring Boot web application that has been Dockerized and can run on any Linux host, including an AWS EC2 instance.

The application responds to `/` with a simple message:  
`Docker Spring App is running!`

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

## Build and Run Locally

 **1. Clone repository**
```bash
git clone https://github.com/tehreem-k/SecDevOps-Assignment-Docker.git
cd spring-docker-app
```
**2. Build Docker image**
```bash
docker build -t spring-docker-app:latest .
```
**3. Run container**
```bash
docker run -d -p 5000:5000 --name spring-app spring-docker-app:latest
```

**4. Verify application locally**
```bash
curl http://localhost:5000

```
**Expected output:**

Keep it small and easy to run.

**5. Verify application from external (if it is on EC2 Instance )**

 - [x] make sure port 5000 is allowed for inbound

Access via browser using the EC2 public IP:

    http://< EC2 public IP>:5000/

