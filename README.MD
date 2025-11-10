# 🚀 Python Application - Fully Automated CI/CD Pipeline using Jenkins & AWS EC2

This project showcases a **fully automated CI/CD pipeline** for deploying a **Python application** onto a deployment server using **Jenkins**, **GitHub**, and **AWS EC2 Instances**.  
It enables seamless, automated deployment every time new code is pushed to the repository.

---

## 🏗️ Project Architecture

**Workflow:**  
GitHub Repository → Jenkins Server (Build & Deploy) → EC2 Deployment Server (Run App using PM2)

- **EC2 Instance 1:** Jenkins CI/CD Server  
- **EC2 Instance 2:** Application Deployment & Execution Server

![](/img/Arc.png)

---

## ⚙️ CI/CD Pipeline Overview

1. **Developer commits code** to GitHub.  
2. **GitHub Webhook** triggers Jenkins automatically.  
3. **Jenkins** fetches the latest code, installs dependencies, and deploys it to the target EC2 instance.  
4. **PM2** ensures the Python application is running continuously.  

---

## ✅ Prerequisites

### 🖥️ Common Setup (Both EC2 Instances)
| Software | Purpose |
|-----------|----------|
| **Python3 / pip** | Run the Python application |
| **Git** | Clone and manage code |
| **OpenSSH** | Enable secure SSH communication |

### 🧰 Additional Setup (Jenkins Server)
| Software | Purpose |
|-----------|----------|
| **Jenkins** | CI/CD automation server |
| **SSH Agent Plugin** | Securely deploy code to the target EC2 instance |

### 🖥️ Additional Setup (Deployment Server)
| Software | Purpose |
|-----------|----------|
| **PM2** | Process manager for running Python apps continuously |
| **python3-venv** | Create isolated Python environments |

---

## 🗂️ Project Repository Structure

```bash
python-app-CICD/
│── app.py
│── requirements.txt
│── Dockerfile
│── README.md
│── Jenkinsfile
└── test/
```

---

## 🔧 Configure Deployment Server (EC2)

1. Launch a new **Ubuntu EC2 instance** (for deployment).  
2. Connect via SSH:  
   ```bash
   ssh -i your-key.pem ubuntu@<EC2-IP>
   ```
3. Install required tools:  
   ```bash
   sudo apt update
   sudo apt install -y python3 python3-venv python3-pip npm git
   sudo npm install -g pm2
   ```
4. Create a directory for your app:  
   ```bash
   mkdir -p /home/ubuntu/pythonapp
   ```

![](/img/Screenshot%20(114).png)

---

## ⚙️ Jenkins Pipeline Setup

1. **Login to Jenkins Server.**
2. Go to **Manage Jenkins → Credentials → Add Credentials**
   - Type: **SSH Username with Private Key**
   - ID: **node-key**
   - Username: **ubuntu**
   - Private Key: *(Paste your PEM key)*


3. Create a **New Pipeline Job** → *Pipeline script from SCM*

![](/img/Screenshot%20(116).png)

4. Set repository details:  
   - **Repository URL:** `https://github.com/rutikakale/python-app.git`  
   - **Branch:** `main`  
5. Save and click **Build Now**.

![](/img/Screenshot%20(122).png)

---

## 🧪 Jenkinsfile Example

Below is the Jenkinsfile used for automating the deployment:

![](/img/Screenshot%20(123).png)

---

## 🔔 GitHub Webhook Setup

To trigger Jenkins automatically on each push:

1. Go to your **GitHub Repository → Settings → Webhooks → Add Webhook**  
2. Enter the following details:  
   - **Payload URL:** `http://<JENKINS-IP>:8080/github-webhook/`  
   - **Content Type:** `application/json`  
   - **Trigger:** *Just push events*  

![](/img/Screenshot%20(117).png)

---

## 🎯 Final Output

After every **Git push**, Jenkins automatically:  
✅ Builds the Python app  
✅ Deploys it to the EC2 Deployment Server  
✅ Restarts the app using **PM2**  

![](/img/Screenshot%20(124).png)


---

## 🏁 Conclusion

This project delivers a **robust, automated CI/CD pipeline** for a Python application using **Jenkins** and **AWS EC2**.  
Each code push to GitHub triggers an end-to-end build and deployment process — ensuring **continuous delivery** with minimal manual effort.  

⭐ *If you found this project useful, give it a star on GitHub!*  
