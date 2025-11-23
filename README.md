# mws-interview
interview outpus

---

# **MWS Interview – Complete Hands-On DevOps + AWS + Docker Task Output**

This repository contains the **full implementation of the technical interview task** assigned by **MWS**, covering:

* Custom AWS networking setup
* EC2 provisioning
* SSM debugging
* CloudWatch & SNS
* EBS volume modification
* Docker container deployment
* Application testing
* Issue documentation
* Architecture diagrams

This README documents everything executed during the interview, including **flowcharts, commands, architecture, screenshots, and all issues faced**.

---

# **📌 Project Summary**

This task required me to:

### **✔ Build a complete AWS environment manually**

### **✔ Deploy an EC2 instance inside a private subnet**

### **✔ Access it using SSM (Session Manager)**

### **✔ Deploy a Dockerized application inside EC2**

### **✔ Set up monitoring, alerts, and storage modifications**

### **✔ Debug real-time failures (SSM not online, port issues, NAT, etc.)**

### **✔ Capture screenshots of all outputs**

### **✔ Document all issues and fixes**

This repository is a **complete, real-world DevOps + AWS hands-on demonstration** done during a live interview.

---

# **📁 Repository Structure**

```
mws-interview/
│
├── Dockerfile
├── index.html
├── Issues.txt
├── screenshots/
│   ├── vpc.png
│   ├── ec2.png
│   ├── docker-output.png
│   ├── alarm.png
│   └── ...
└── README.md (this file)
```

---

# **🏗️ AWS Infrastructure Built**

The following AWS resources were created manually as part of the interview:

## **1. VPC Setup**

### ✔ Custom VPC

* IPv4 CIDR
* IPv6 block

### ✔ Subnets

* **1 Public Subnet** (for NAT & IGW route)
* **1 Private Subnet** (for EC2 instance)

### ✔ Routing

* Internet Gateway attached
* NAT Gateway placed in public subnet
* Private subnet routed to NAT
* Public subnet routed to IGW

---

## **2. EC2 Setup**

### ✔ EC2 launched inside **private subnet**

* Not directly accessible via SSH
* Connected only through **SSM**

### ✔ IAM Role Attached

* `AmazonSSMManagedInstanceCore`

### ✔ Security Group Rules

* Allow **only port 8000 (UDP)**
* Deny all other inbound ports
* Allow outbound traffic

### ✔ EBS Volume Modification

* Increased volume size manually
* Validated successful resizing

---

## **3. Monitoring & Alerts**

### ✔ CloudWatch Metric Alarms

* CPU Utilization alarm configured
* EBS storage metric monitored

### ✔ SNS Notification Setup

* SNS topic created
* Email subscription
* Alarm → SNS → Email trigger configured

### ✔ Stress Testing (CPU & EBS)

Used stress command to trigger alarms.

---

## **4. Docker Deployment**

### ✔ Built a Docker image from `Dockerfile`

### ✔ Ran the container inside EC2

### ✔ Exposed application through port 8000

### ✔ Verified application output

### ✔ Included all screenshots as proof

---

# **🖥️ Docker Build & Run Commands**

### **Build Image**

```bash
docker build -t mws-app .
```

### **Run Container**

```bash
docker run -d -p 8000:8000 mws-app
```

### **Verify**

```bash
curl localhost:8000
```

---

# **📊 Architecture Diagram**

```
                         ┌──────────────────────────┐
                         │        AWS Cloud         │
                         └─────────────┬────────────┘
                                       │
                        ┌──────────────┴──────────────┐
                        │      Custom VPC (IPv4/IPv6)  │
                        └──────────────┬──────────────┘
                                       │
     ┌─────────────────────────────────┼─────────────────────────────────┐
     │                                 │                                 │
┌────▼────┐                       ┌────▼────┐                     ┌─────▼─────┐
│ Public  │                       │ Private │                     │ Internet  │
│ Subnet  │                       │ Subnet  │                     │  Gateway  │
└────┬────┘                       └────┬────┘                     └─────┬─────┘
     │ NAT Gateway                      │ EC2 Instance                  │
     │ (has Public IP)                  │ (No public IP)                │
     │                                   │ SSM Role Attached             │
     │                                   │ Docker App                    │
     │                                   │ CloudWatch Agent (metrics)    │
     │                                   ▼                               │
     │                          ┌────────────────┐                       │
     └─────────────────────────►│  SSM Session   │◄───────────────────────┘
                                └────────────────┘

```

---

# **🔄 Flowchart – End-to-End Workflow**

```
             ┌───────────────────────────────────┐
             │ Start Interview Task              │
             └───────────────┬───────────────────┘
                             │
                             ▼
               ┌────────────────────────┐
               │ Create Custom VPC      │
               └───────────┬────────────┘
                           │
                           ▼
         ┌────────────────────────────────────────┐
         │ Create Public + Private Subnets         │
         └────────────────┬────────────────────────┘
                          │
                          ▼
           ┌──────────────────────────────────┐
           │ Attach IGW & Create NAT Gateway  │
           └──────────────────┬───────────────┘
                              │
                              ▼
            ┌────────────────────────────────┐
            │ Launch EC2 in Private Subnet   │
            └─────────────────┬──────────────┘
                              │
                              ▼
          ┌─────────────────────────────────────┐
          │ Attach SSM Role & Connect via SSM   │
          └──────────────────┬──────────────────┘
                             │
                             ▼
           ┌──────────────────────────────────┐
           │ Deploy Dockerized Application    │
           └──────────────────┬───────────────┘
                              │
                              ▼
            ┌────────────────────────────────┐
            │ Configure CloudWatch Alarms    │
            │ + SNS Email Alerts             │
            └────────────────────┬───────────┘
                                 │
                                 ▼
               ┌───────────────────────────────────┐
               │ Execute Stress Test & Verify Logs │
               └───────────────────┬──────────────┘
                                   │
                                   ▼
                     ┌──────────────────────────┐
                     │ Document All Issues      │
                     └──────────────┬───────────┘
                                    │
                                    ▼
                         ┌────────────────────┐
                         │ Submit for Review  │
                         └────────────────────┘
```

---
# **📬 Contact**

**Kapilan R**
DevOps Engineer (Fresher with Real-Time Hands-On Experience)
GitHub: [https://github.com/kapilanramesh](https://github.com/kapilanramesh)
Email: kapilanramesh1@gmail.com

---

