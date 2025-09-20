# MEAN Stack Implementation on AWS
---
## Diagram
![MERN AWS_Architecture](../4.MEAN_Stack/images/mean_stack.png)
---
## Overview
The **MEAN Stack** is a web service solution stack consisting of:
- **M**ongoDB – Document-based NO-SQL Database
- **E**xpressJS – Server side Web Application for Node.js
- **A**ngular – A Frontend Framework based on Javascript
- **N**odeJS – A JavaScript Runtime Environment

We will deploy the MEAN stack on an Amazon EC2 instance running Ubuntu.

---

## 1. Prerequisites
Before starting, ensure you have:
1. An **AWS Account**.
2. Basic knowledge of **Linux commands**.
3. A **key pair** for SSH access.
4. AWS **security group rules** allowing:
   - HTTP (Port 80)
   - SSH (Port 22)
   - Custom Port (Port 3300) - For the Frontend
5. A local terminal (Linux/Mac/git bash) or **PuTTY** (Windows).

---

## 2. Step-by-Step Implementation

### Step 1: Launch an EC2 Instance
- Log into the AWS Management Console to setup the EC2 Instance.
---
![EC2-Dashboard](../1.LAMP_Stack/images/a.PNG)
---
- Search for **EC2  on the search bar**.
---
![EC2 Search](../1.LAMP_Stack/images/1a.PNG)
---
- Click on Launch Instance.
---
![EC2 Search](../1.LAMP_Stack/images/1.PNG)
---
- Enter the name of your web server
---
![EC2 Name](../1.LAMP_Stack/images/1b.PNG)
---
- Choose **Ubuntu Server 22.04 LTS** (or latest version).
---
![Ubuntu](../1.LAMP_Stack/images/1c.PNG)
- Select an **instance type** (e.g., t2.micro for free tier).
---
![Instance-Type](../1.LAMP_Stack/images/1e.PNG)
- Configure **Security Group** to allow HTTP, HTTPS, SSH.
---
![Instance-Type](../1.LAMP_Stack/images/1h.PNG)
---
- Launch and download the `.pem` key pair or use an already created key pair.
---
![key pair](../1.LAMP_Stack/images/1f.PNG)
---
![key pair 2](../1.LAMP_Stack/images/1g.PNG)
---
- Configure the storage to what you prefer but we will leave everything default.
---
![configure-storage](../1.LAMP_Stack/images/1j.PNG)
---
- Scroll down and at your right, click on Launch Instance.
---
![launch-instance](../1.LAMP_Stack/images/1k.PNG)
---
- You should see this if everything is successful
---
![ec2-success](../1.LAMP_Stack/images/1l.PNG)
---
- Make sure the status checks are all checked ensuring that our instance has been launched and running
---
![ec2-success](../1.LAMP_Stack/images/2d.PNG)
---
- Now, copy the public IP Address of your instance
---
![ec2-success](../1.LAMP_Stack/images/2.PNG)
---
- Another way to retrieve your IP Address is to use this command
```bash
 TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` && curl -H "X-aws-ec2-metadata-token: $TOKEN" -s http://169.254.169.254/latest/meta-data/public-ipv4
```
- OR by this
```bash
 curl -s http://169.254.169.254/latest/meta-data/public-ipv4
```
---
### Step 2: Connect to Your Instance
From your terminal, cd Downloads/:
```bash
chmod 400 lamp-stack-kp.pem
ssh -i lamp-stack-kp.pem ubuntu@<EC2_PUBLIC_IP>
```
- Type `yes` 
---
![ec2-success](../1.LAMP_Stack/images/2b.PNG)
---
- You're in when you see this
---
![ssh-success](../1.LAMP_Stack/images/2c.PNG)
---

### Step 3: Update and Upgrade the System
```bash
sudo apt update && sudo apt upgrade -y
```
---
### Step 4: Add Certificates and Install Nodejs
```bash
sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates
```
---
- Download a script from NodeSource. This actually configures our system so that we can install Node.js 18.x using apt.
```bash
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
- Install Nodejs
```bash
sudo apt install -y nodejs
```
---
### Step 5: Install MongoDB
- Install gnupg and curl
```bash
sudo apt-get install -y gnupg curl
```
- Download MongoDB GPG key and save to keyring
```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
  sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
```
- Create MongoDB APT repository so that apt can easily fetch MongoDB Packages.
```bash
echo "deb [arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | \
sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
```
---
![mongodb apt](../3.MEAN_Stack/images/1a.PNG)
---
- Update your system again
```bash
sudo apt-get update
```
- Install MongoDB
```bash
sudo apt-get install -y mongodb-org
```
- Start MongoDB service
```bash
sudo systemctl start mongod
```
- Enable to start on boot
```bash
sudo systemctl enable mongod
```
- Check status on mongod
```bash
sudo systemctl status mongod
```
---
![mongodb status](../3.MEAN_Stack/images/1b.PNG)
---
