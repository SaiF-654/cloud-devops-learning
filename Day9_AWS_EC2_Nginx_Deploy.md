# Day 9 - AWS EC2, Nginx & Deploying a Web Application

## Summary
Today I created an AWS account, launched an Ubuntu EC2 instance, connected via SSH, installed Nginx, deployed a simple web app, and opened port 80 in the security group for public access.

---

## Steps Covered

### 1. Create AWS Account
- Signed up for AWS and verified identity.
- Added billing method using **NayaPay debit card**.

---

### 2. Launch Ubuntu EC2 Instance
- Created a key pair (`mise_key.pem`).
- Created a security group with:
  - SSH (22) → My IP
  - HTTP (80) → 0.0.0.0/0
- Launched **Ubuntu Server 22.04 LTS** (t2.micro).

---

### 3. Connect to Server
```bash
ssh -i ~/keys/mise_key.pem ubuntu@<PUBLIC_IP>
```
- Alternative: EC2 Instance Connect (browser-based).

---

### 4. Update & Install Nginx
```bash
sudo apt-get update
sudo apt-get install -y nginx
systemctl status nginx
```
- Visit `http://<PUBLIC_IP>` → Default Nginx page is live.

---

### 5. Deploy a Simple Web App
**Option A — Copy local files (SCP):**
```bash
scp -i ~/keys/mise_key.pem ./index.html ubuntu@<PUBLIC_IP>:/home/ubuntu/
sudo mv /home/ubuntu/index.html /var/www/html/index.html
sudo chown www-data:www-data /var/www/html/index.html
```

**Option B — Clone from GitHub:**
```bash
sudo apt-get install -y git
sudo git clone https://github.com/your-username/your-web-repo.git /var/www/html
sudo chown -R www-data:www-data /var/www/html
```

---

### 6. Open Port 80 (Security Group)
- Added inbound rule for **HTTP (80)** from `0.0.0.0/0`.
- Verified accessibility by visiting the public IP in browser.

---

## Commands Practiced
```bash
sudo apt-get update
sudo apt-get install nginx
systemctl status nginx
ssh -i ~/keys/mise_key.pem ubuntu@<PUBLIC_IP>
scp -i ~/keys/mise_key.pem ./index.html ubuntu@<PUBLIC_IP>:/home/ubuntu/
```

---

## Key Takeaways
- AWS setup requires billing verification.  
- SSH keys are crucial for secure EC2 access.  
- Nginx is a lightweight, fast web server to serve applications.  
- Security groups control inbound/outbound traffic — opening port 80 allows public access.  
