# AWS Three-Tier Architecture using Terraform

## Project Overview

This project demonstrates the deployment of a production-style **three-tier architecture on AWS** using **Terraform** as the Infrastructure as Code (IaC) tool. The objective was to automate infrastructure provisioning while following AWS best practices for networking, security, scalability, and maintainability.

The infrastructure was designed to be fully reproducible, modular, and suitable as a foundation for real-world cloud-native applications.

---

## Technologies Used

* **Terraform**
* **Amazon VPC**
* **Amazon EC2**
* **Application Load Balancer (ALB)**
* **Amazon RDS (Multi-AZ)**
* **Amazon S3**
* **AWS IAM**
* **Security Groups**
* **NAT Gateway**
* **Internet Gateway**
* **Amazon CloudWatch**

---

## Architecture

```text
                 Internet
                     │
                     ▼
          Internet Gateway (IGW)
                     │
                     ▼
        Application Load Balancer
               (Public Subnets)
                     │
                     ▼
          EC2 Application Servers
             (Private Subnets)
                     │
                     ▼
          Amazon RDS (Multi-AZ)
             (Private Subnets)

Additional Components
---------------------
• NAT Gateway for secure outbound internet access
• Amazon S3 for static assets and logs
• CloudWatch for monitoring
• IAM Roles and Security Groups for secure access
```

---

## Key Features

* Automated infrastructure provisioning using Terraform
* Custom VPC with public and private subnets across multiple Availability Zones
* Internet Gateway for public internet access
* NAT Gateway enabling outbound connectivity for private resources
* Application Load Balancer distributing incoming traffic
* EC2 application servers deployed in private subnets
* Amazon RDS Multi-AZ deployment for high availability
* Amazon S3 for object storage and application logs
* IAM roles implementing least-privilege access
* Security Groups restricting network access between application layers
* CloudWatch monitoring for infrastructure visibility

---

## Security Design

* Database is deployed in private subnets with no public endpoint.
* Application servers are accessible only through the Application Load Balancer.
* Security Groups restrict communication to only required ports.
* IAM roles are used instead of long-lived credentials where possible.
* Private instances access the internet securely through the NAT Gateway.

---

## Learning Outcomes

Through this project, I gained practical experience in:

* Designing AWS networking using VPCs, route tables, Internet Gateways, and NAT Gateways
* Building secure multi-tier cloud architectures
* Infrastructure provisioning using Terraform modules
* Managing infrastructure state for repeatable deployments
* Implementing AWS security best practices
* Understanding high availability and fault tolerance concepts
* Monitoring infrastructure using Amazon CloudWatch
* Structuring Infrastructure as Code for maintainability and scalability

---

## Future Enhancements

Planned improvements include:

* Containerizing the application using Docker
* Migrating compute workloads to Amazon ECS (Fargate) or Kubernetes (EKS)
* Implementing CI/CD pipelines using GitLab CI/CD
* Introducing Auto Scaling Groups
* Adding AWS WAF for enhanced security
* Centralizing logs using CloudWatch Logs
* Implementing cost optimization strategies
* Integrating Prometheus and Grafana for advanced monitoring
* Configuring Route 53 and HTTPS with AWS Certificate Manager

---

## Skills Demonstrated

* AWS Cloud Architecture
* Infrastructure as Code (Terraform)
* VPC Design and Networking
* EC2 Administration
* Load Balancing
* Database Deployment (Amazon RDS)
* Security Groups and IAM
* High Availability Design
* Linux Administration
* Cloud Monitoring
* Cloud Security
* DevOps Fundamentals

---

## Conclusion

This project strengthened my understanding of cloud architecture, Infrastructure as Code, and production-ready AWS deployments. It demonstrates how automated provisioning, secure networking, and modular infrastructure design can simplify deployment, improve consistency, and provide a scalable foundation for modern cloud applications.
