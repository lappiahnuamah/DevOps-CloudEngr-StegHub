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
   - Custom Port (Port 3000) - For the Frontend
   - Custom Port (Port 5000) - For the Backend
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

### Step 3: Update the System
```bash
sudo apt update && sudo apt upgrade -y
```

---

- I am going to the market

```bash
pip install nodejs
```
---
```python
pip install flask
```
---
![This is a mean stack image](../4.MEAN_Stack/images/mean_stack.png)
