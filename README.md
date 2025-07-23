# 🚀 Deploy React App on AWS EC2 + Nginx (Free Tier) 🌐

[![AWS](https://img.shields.io/badge/AWS-Free%20Tier-orange?logo=amazon-aws)](https://aws.amazon.com/free/)
[![React](https://img.shields.io/badge/Built%20with-React-61DAFB?logo=react)](https://reactjs.org/)
[![Nginx](https://img.shields.io/badge/Web%20Server-Nginx-009639?logo=nginx)](https://nginx.org/)
[![Ubuntu](https://img.shields.io/badge/OS-Ubuntu-E95420?logo=ubuntu)](https://ubuntu.com/)

---

## 📄 Overview

This guide helps you deploy a production-ready React app on an AWS EC2 instance (Free Tier), served by Nginx. Perfect for portfolios and practicing deployments of projects!

---

## 📋 Prerequisites

- AWS account with Free Tier eligibility
- React app (local or in a Git repo)
- SSH keys (`.pem` file from AWS)

---

## 🛠️ Step 1: Setting Up AWS EC2

1. **Log in to AWS Console**
2. Go to **EC2** → Launch Instance
3. Choose **Ubuntu Server 20.04 (Free Tier eligible)**
4. Select **t2.micro** 
5. Download your keypair (`your-key.pem`)
6. Update Security Group:
    - `SSH (22)` — your IP only
    - `HTTP (80)` — open to all
    - `HTTPS (443)` — open to all
7. Launch your instance

---

## 🔐 Step 2: Connect to EC2 via SSH
On Windows open powershell and add your EC2 public IP in command.
```bash 
ssh -i /path/to/your-key.pem ubuntu@<EC2-PUBLIC-IP>
```

---

## 📦 Step 3: Install Required Packages
```bash
sudo apt update
```

```bash
sudo apt install nginx nodejs npm git -y
```

[![Nginx](https://img.shields.io/badge/Web%20Server-Nginx-009639?logo=nginx)](https://nginx.org/)
[![Node.js](https://img.shields.io/badge/Runtime-Node.js-339933?logo=node.js)](https://nodejs.org/)
[![npm](https://img.shields.io/badge/Package%20Manager-npm-CB3837?logo=npm)](https://www.npmjs.com/)
[![Git](https://img.shields.io/badge/Version%20Control-Git-F05032?logo=git)](https://git-scm.com/)

Check your installs:
`node -v`
`npm -v`
`nginx -v` 
`git --version`

---

## 📁 Step 4: Transfer and Build Your React App

**Clone from GitHub**
```bash
git clone https://github.com/your-username/your-react-app.git
```

```bash
cd your-react-app
```
**Build the app:**
```
npm install
```
```bash
npm run build
```

---

## 🚚 Step 5: Deploy Build Files to Nginx Web Root

Nginx root folder for ubuntu has path /var/www/html/
In this folder we have to add our build of react project.

```bash
sudo rm -rf /var/www/html/*
```

```bash
sudo cp -r build/* /var/www/html/
```
---

## ⚙️ Step 6: Configure Nginx

Edit the default Nginx config:
```bash
sudo nano /etc/nginx/sites-available/default
```

Changes in the `server` block:
```
server {
listen 80;

root /var/www/html;
index index.html index.htm;

location / {
    try_files $uri /index.html;
  }
}
```
**Test and restart Nginx:**
```bash
sudo nginx -t
```
**Whenever we do changes in default config file of nginx we have to restart the service**
```bash
sudo systemctl restart nginx
```

Now visit public id address on EC2 to see your React app!

---

**Will this always be free?**  
EC2 Free Tier lasts 12 months. Afterward, you’ll be charged per usage. For always-free static hosting, consider [Netlify](https://netlify.com/), [Vercel](https://vercel.com/), or [Cloudflare Pages](https://pages.cloudflare.com/).

## 🎯 Quick Commands Table

| Step                 | Command/Action                                  |
|----------------------|-------------------------------------------------|
| EC2 Launch           | AWS Console, open ports 22/80/443               |
| SSH to EC2           | `ssh -i "your-key.pem" ubuntu@EC2-IP`           |
| Install software     | `sudo apt install nginx nodejs npm git`         |
| Build React app      | `npm install && npm run build`                  |
| Deploy build         | `sudo cp -r build/* /var/www/html/`             |
| Nginx config         | Edit `/etc/nginx/sites-available/default`       |
| Restart Nginx        | `sudo systemctl restart nginx`                  |
| Test app             | Visit your IP/domain in browser                 |

---

> ⭐ Deploy and showcase your React app on AWS like a professional!
🎉 Now you have a fully formatted, visually appealing README.md to include with your deployment project!

You can insert your project/repo links wherever you see <YOUR_DOMAIN_OR_EC2_PUBLIC_IP>, <EC2-IP>, etc.

Drop this file in your GitHub repository root.

Happy deploying!
