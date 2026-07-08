# Kubernetes Observability Stack with Prometheus, Grafana & Alertmanager

## Project Overview

This project demonstrates the deployment of a **production-style Kubernetes observability platform** using the **Prometheus Stack (kube-prometheus-stack)**. The objective was to build a scalable monitoring solution capable of collecting, storing, visualizing, and analyzing Kubernetes and infrastructure metrics while gaining a deep understanding of cloud-native observability.

Beyond deploying the default monitoring stack, I designed and built **custom Grafana dashboards** to visualize application-specific metrics and traffic patterns, providing meaningful operational insights alongside the dashboards included with the Helm chart.

---

## Technologies Used

* Kubernetes
* Helm
* Prometheus
* Grafana
* Alertmanager
* kube-state-metrics
* node-exporter
* kubectl
* Linux
* Nginx
* Node.js
* ApacheBench (ab)
* curl

---

## Architecture

```text
                    Client Requests
                  (curl / ApacheBench)
                           │
                           ▼
                   Node.js Application
                           │
                           ▼
                     Kubernetes Cluster
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
        ▼                  ▼                  ▼
node-exporter     kube-state-metrics     Application Metrics
        │                  │                  │
        └──────────────────┼──────────────────┘
                           ▼
                     Prometheus Server
                           │
               Metrics Collection & Storage
                           │
            ┌──────────────┴──────────────┐
            │                             │
            ▼                             ▼
     Grafana Dashboards            Alertmanager
(Default + Custom Dashboards)      Alert Routing
```

---

# Project Objectives

* Deploy a complete Kubernetes monitoring platform.
* Understand the architecture of cloud-native observability.
* Monitor Kubernetes cluster health and workloads.
* Create custom Grafana dashboards.
* Generate traffic and validate metric collection.
* Practice production-style debugging and troubleshooting.

---

# Deployment Process

## Cluster Validation

Verified cluster health before deployment using:

* Nodes
* Pods
* Deployments
* Services
* Namespaces

---

## Helm Deployment

Installed the complete monitoring stack using Helm.

Components deployed:

* Prometheus
* Grafana
* Alertmanager
* node-exporter
* kube-state-metrics

Using Helm ensured:

* Consistent deployments
* Easy upgrades
* Simple rollback
* Production-standard package management

---

# Observability Components

## Prometheus

Responsibilities:

* Metric collection
* Time-series storage
* PromQL querying
* Service discovery

Collected metrics from:

* Kubernetes Nodes
* Pods
* Services
* Deployments
* Node Exporter
* kube-state-metrics

---

## Grafana

Configured Grafana as the visualization layer.

Implemented:

* Default dashboards provided by the Helm chart
* **Custom dashboards designed specifically for application monitoring**
* Real-time traffic visualization
* Infrastructure performance monitoring
* Resource utilization dashboards
* Kubernetes health dashboards

### Custom Dashboard Features

Created a custom Grafana dashboard to monitor:

* Application Requests per Second (RPS)
* Active Connections
* Response Times
* Request Rate
* CPU Utilization
* Memory Usage
* Pod Status
* Container Restarts
* Node Health
* Traffic Patterns during Load Testing

The custom dashboard complemented the default Kubernetes dashboards by providing a focused view of application performance and operational metrics.

---

## Alertmanager

Configured Alertmanager for:

* Alert routing
* Notification management
* Incident response workflow

---

## node-exporter

Collected infrastructure metrics including:

* CPU Utilization
* Memory Usage
* Disk Usage
* Filesystem Statistics
* Network Traffic

---

## kube-state-metrics

Collected Kubernetes object metrics including:

* Pod Status
* Deployments
* ReplicaSets
* StatefulSets
* DaemonSets
* Nodes
* Namespaces

---

# Kubernetes Concepts Explored

* Pod Networking
* Service Networking
* ClusterIP Services
* Internal DNS Resolution
* Kubernetes Service Discovery
* Helm Charts
* Helm Releases
* Labels & Selectors
* Kubernetes Resources
* Namespaces

---

# Validation & Troubleshooting

Used Kubernetes troubleshooting commands to validate deployments:

* kubectl logs
* kubectl describe
* kubectl get
* kubectl exec
* kubectl port-forward

Verified:

* Pod health
* Service communication
* DNS resolution
* Metrics collection
* Dashboard visualization
* Alert pipeline functionality

---

# Performance Testing

Generated synthetic traffic using:

* curl
* ApacheBench (ab)

Validated:

* Live metric ingestion
* Prometheus scraping
* Grafana dashboard updates
* Real-time traffic visualization
* Cluster performance under load

---

# Key Learning Outcomes

* Built a complete Kubernetes observability platform.
* Learned Prometheus architecture and metric collection.
* Understood Grafana dashboard design and visualization.
* Designed custom dashboards tailored to application monitoring.
* Explored Kubernetes networking and service discovery.
* Practiced Helm-based application deployment.
* Performed production-style troubleshooting using kubectl.
* Validated observability pipelines through live traffic simulation.
* Gained hands-on experience with cloud-native monitoring best practices.

---

# Future Enhancements

* Deploy using GitOps (Argo CD)
* Configure Prometheus Remote Write
* Integrate Loki for centralized log aggregation
* Add Tempo for distributed tracing
* Configure Slack and Email alerting
* Monitor custom application metrics
* Deploy the monitoring stack on Amazon EKS
* Automate deployment using GitLab CI/CD

---

# Skills Demonstrated

* Kubernetes
* Helm
* Prometheus
* Grafana
* Alertmanager
* Kubernetes Networking
* Service Discovery
* Monitoring & Observability
* Performance Testing
* Infrastructure Monitoring
* Linux Administration
* Cloud-Native Technologies
* DevOps
* Site Reliability Engineering (SRE)

---

# Conclusion

This project provided hands-on experience in designing and deploying a production-ready Kubernetes observability platform. By combining Prometheus, Grafana, Alertmanager, node-exporter, and kube-state-metrics with Helm-based deployment, I built a scalable monitoring solution capable of delivering real-time visibility into both infrastructure and application performance. Creating custom Grafana dashboards further enhanced observability by presenting meaningful business and operational metrics beyond the default dashboards, strengthening my understanding of monitoring architecture, Kubernetes internals, and production operations.
