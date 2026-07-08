# Real-Time Application Monitoring with Prometheus & Grafana

## Project Overview

This project demonstrates how to build a complete monitoring and observability stack for a web application using **Prometheus** and **Grafana**. The goal was to collect real-time metrics, visualize application performance, and understand traffic patterns through meaningful dashboards.

Instead of focusing only on monitoring tools, this project emphasizes how metrics flow from an application to Prometheus and how Grafana transforms those metrics into actionable insights.

---

## Technologies Used

* Prometheus
* Grafana
* Node.js
* Nginx
* Nginx Prometheus Exporter
* ApacheBench (ab)
* Linux (Ubuntu)
* PM2

---

## Architecture

```text
                    Client Requests
                           │
                 curl / ApacheBench
                           │
                           ▼
                  Node.js Web Application
                           │
                    Reverse Proxy (Nginx)
                           │
          ┌────────────────┴────────────────┐
          │                                 │
          ▼                                 ▼
 Nginx Prometheus Exporter          Application Metrics
          │                                 │
          └────────────────┬────────────────┘
                           ▼
                     Prometheus Server
                           │
                           ▼
                    Grafana Dashboards
```

---

## Project Objectives

* Deploy a web application for monitoring.
* Configure Prometheus to collect infrastructure and application metrics.
* Integrate Nginx metrics using the Prometheus Exporter.
* Build Grafana dashboards for real-time visualization.
* Generate traffic using benchmarking tools.
* Observe how application metrics change under different traffic loads.
* Understand the complete observability workflow from metric collection to visualization.

---

## Features

### Prometheus

* Installed and configured Prometheus
* Configured scrape targets
* Collected application and Nginx metrics
* Verified real-time metric collection

### Grafana

* Connected Prometheus as a data source
* Built custom dashboards
* Visualized application performance
* Created live monitoring panels

### Application

* Deployed a simple Node.js application
* Configured Nginx as a reverse proxy
* Exposed Nginx metrics through Prometheus Exporter

### Traffic Simulation

Generated test traffic using:

* curl
* ApacheBench (ab)

This helped simulate user requests and observe metric changes in real time.

---

## Metrics Monitored

The dashboards displayed metrics such as:

* HTTP Requests per Second (RPS)
* Active Connections
* Total Requests
* Response Rate
* Nginx Metrics
* Application Availability
* Traffic Spikes
* Request Throughput

---

## Key Learning Outcomes

* Understood the complete Prometheus monitoring workflow.
* Learned how Prometheus scrapes metrics from exporters.
* Configured Grafana dashboards for real-time visualization.
* Analyzed application behavior during traffic spikes.
* Understood how monitoring data supports troubleshooting and performance optimization.
* Gained practical experience with observability in production-style environments.

---

## Future Enhancements

* Add Node Exporter for Linux system metrics
* Monitor CPU, Memory, Disk, and Network utilization
* Integrate Alertmanager for automated alerting
* Deploy the monitoring stack using Docker Compose
* Monitor Kubernetes workloads
* Add Loki for centralized log aggregation
* Create custom application metrics using Prometheus client libraries

---

## Skills Demonstrated

* Prometheus
* Grafana
* Monitoring & Observability
* Nginx
* Node.js
* Linux Administration
* Performance Monitoring
* ApacheBench
* PM2
* Infrastructure Monitoring
* DevOps Fundamentals

---

## Conclusion

This project strengthened my understanding of modern observability by implementing a complete monitoring pipeline from metric collection to visualization. By generating live traffic and monitoring it in Grafana, I gained practical experience in analyzing application performance, identifying traffic patterns, and understanding how monitoring supports reliable and scalable production systems.
