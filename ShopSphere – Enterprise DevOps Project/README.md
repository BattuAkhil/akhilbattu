# 🚀 ShopSphere – Full Stack E-Commerce Application with DevOps

![AWS](https://img.shields.io/badge/AWS-EC2-orange)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![GitLab CI/CD](https://img.shields.io/badge/GitLab-CI%2FCD-FC6D26)
![Node.js](https://img.shields.io/badge/Node.js-22-green)
![React](https://img.shields.io/badge/React-Vite-61DAFB)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248)
![Prometheus](https://img.shields.io/badge/Prometheus-Monitoring-E6522C)
![Grafana](https://img.shields.io/badge/Grafana-Dashboard-F46800)

## 📖 Overview

ShopSphere is a containerized full-stack e-commerce application deployed on AWS using modern DevOps practices.

The project demonstrates an end-to-end CI/CD pipeline, automated deployments, containerization, reverse proxy configuration, cloud hosting, and infrastructure monitoring.

---

# 🏗️ Architecture

```
Developer
    │
    │ Git Push
    ▼
GitLab Repository
    │
    ▼
GitLab CI/CD Pipeline
    │
    │ SSH Deployment
    ▼
AWS EC2 (Ubuntu)
    │
    ▼
Docker Compose
    │
    ├───────────────┐
    ▼               ▼
Frontend         Backend
(React)         (Node.js)
    │               │
    └──────┬────────┘
           ▼
       Nginx Reverse Proxy
           │
           ▼
     MongoDB Atlas

Monitoring

Node Exporter
      │
      ▼
 Prometheus
      │
      ▼
 Grafana
```

---

# ✨ Features

- User Registration & Login
- JWT Authentication
- Product Listing
- Product Search
- Shopping Cart
- Checkout
- Order Management
- Responsive UI
- Dockerized Services
- Automated CI/CD Deployment
- Infrastructure Monitoring

---

# 🛠️ Tech Stack

## Frontend

- React
- Vite
- HTML
- CSS
- JavaScript

## Backend

- Node.js
- Express.js
- JWT Authentication

## Database

- MongoDB Atlas

## DevOps

- Git
- GitLab
- GitLab CI/CD
- Docker
- Docker Compose
- AWS EC2
- Nginx
- SSH
- Prometheus
- Grafana
- Node Exporter

---

# ⚙️ CI/CD Pipeline

Every push to the **main** branch automatically triggers:

```
Git Push
      │
      ▼
GitLab Pipeline
      │
      ▼
SSH into EC2
      │
      ▼
Git Pull
      │
      ▼
Docker Compose Build
      │
      ▼
Docker Compose Up
      │
      ▼
Application Updated
```

---

# 📊 Monitoring

The project includes a complete monitoring stack.

### Prometheus

- Server Metrics
- Node Exporter Metrics

### Grafana Dashboards

- CPU Usage
- Memory Usage
- Disk Usage
- Network Traffic
- System Health

---

# 📁 Project Structure

```
shopsphere/

├── backend/
│   ├── src/
│   ├── Dockerfile
│   └── package.json
│
├── frontend/
│   ├── src/
│   ├── Dockerfile
│   └── package.json
│
├── nginx/
│   └── nginx.conf
│
├── monitoring/
│   ├── docker-compose.yml
│   └── prometheus.yml
│
├── docker-compose.yml
├── .gitlab-ci.yml
└── README.md
```

---

# 🚀 Deployment

### Clone Repository

```bash
git clone https://github.com/BattuAkhil/shopsphere.git
cd shopsphere
```

### Start Application

```bash
docker compose up -d --build
```

### Stop Application

```bash
docker compose down
```

---

# 📸 Screenshots

Add screenshots here.

- Home Page
- Login
- Product Page
- Cart
- Orders
- Grafana Dashboard
- GitLab Pipeline
- Docker Containers

---

# 📈 Monitoring URLs

Prometheus

```
http://<EC2-IP>:9090
```

Grafana

```
http://<EC2-IP>:3000
```

---

# 🔄 CI/CD Workflow

- Push code to GitLab
- Pipeline starts automatically
- SSH into AWS EC2
- Pull latest code
- Rebuild Docker images
- Restart containers
- Deploy latest version

---

# 💡 Skills Demonstrated

- Linux Administration
- AWS EC2
- Docker
- Docker Compose
- GitLab CI/CD
- Git
- SSH Authentication
- Nginx Reverse Proxy
- MongoDB Atlas
- Monitoring & Observability
- DevOps Automation
- Troubleshooting Production Deployments

---

# 📌 Future Improvements

- HTTPS with Let's Encrypt
- Terraform Infrastructure as Code
- Kubernetes Deployment
- GitLab Container Registry
- Alertmanager
- Blue/Green Deployment
- Automated Testing
- Auto Scaling

---

# 👨‍💻 Author

**Akhil Battu**

- GitHub: https://github.com/BattuAkhil
- LinkedIn: https://www.linkedin.com/in/akhil-battu-66b8a1364/

---

⭐ If you found this project useful, consider giving it a star!
