# Grafana-and-Prometheus

## Grafana
### Overview:
Grafana is an open-source platform for monitoring and observability. It allows you to query, visualize, alert on, and understand your metrics, logs, and traces.

### Key Features:
Data Source Integration: Supports Prometheus, Elasticsearch, MySQL, and many more.
Dashboards: Create and share interactive dashboards.
Alerting: Set up alerts to notify you of potential issues.
Templating: Use variables to create dynamic and reusable dashboards.
Basic Workflow:
Install Grafana:
Download and install Grafana.
### Command:

```
wget https://dl.grafana.com/oss/release/grafana-7.5.5.linux-amd64.tar.gz
tar -zxvf grafana-7.5.5.linux-amd64.tar.gz
cd grafana-7.5.5
./bin/grafana-server

```

## Configure Data Source:

Add Prometheus as a data source.
Configuration: Navigate to Grafana UI > Configuration > Data Sources > Add Data Source.
Example:
Name: Prometheus
URL: http://localhost:9090

## Create Dashboards:
Build custom dashboards to visualize metrics.
Example: Create a panel to monitor CPU usage.
Query: rate(node_cpu_seconds_total[5m])
## Set Up Alerts:
Configure alert rules to notify you of issues.
Example: Alert on high CPU usage.
Configure alerting in panel settings.

## Share Dashboards:

Share dashboards with your team.
Configuration: Use the share option to export or link dashboards.
Tools and Best Practices:
## Pre-built Dashboards:
Use and customize pre-built dashboards from the Grafana community.
Example: Import Node Exporter Full dashboard (ID: 1860).

## Templating:
Use variables to create dynamic dashboards.
```
variable:
  name: node
  label: Node
  query: label_values(node_exporter_build_info, instance)
```
## Alerting:

Configure alert notifications via email, Slack, or other channels.
Example: Configure Slack integration
```
alerting:
  notification_channels:
    - name: slack
      type: slack
      settings:
        url: https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX


```

## Grafana Loki:

Use Loki for log aggregation and integrate it with Grafana for centralized logging.
Example: Configure Loki as a data source and use it in dashboards.


#Prometheus
###Overview:
Prometheus is an open-source systems monitoring and alerting toolkit originally built at SoundCloud. It collects and stores metrics as time series data, recording information with timestamps.

### Key Features:
Multi-dimensional Data Model: Uses key/value pairs for metrics.
Query Language (PromQL): Powerful and flexible query language.
Time Series Database: Stores time series data efficiently.
Service Discovery: Dynamically discovers targets for monitoring.
Alerting: Integrated alerting system with Prometheus Alertmanager.
## Basic Workflow:
## Install Prometheus:

Download and install Prometheus.
Command:
```
wget https://github.com/prometheus/prometheus/releases/download/v2.28.1/prometheus-2.28.1.linux-amd64.tar.gz
tar xvfz prometheus-*.tar.gz
cd prometheus-*

```
## Configuration:

Define a prometheus.yml configuration file.
Example
```
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']

```

## Run Prometheus:

Start the Prometheus server.
Command
```
./prometheus --config.file=prometheus.yml

```
## Collect Metrics:

Use exporters to collect metrics from various services.
Example: Node Exporter for system metrics.
```
wget https://github.com/prometheus/node_exporter/releases/download/v1.1.2/node_exporter-1.1.2.linux-amd64.tar.gz
tar xvfz node_exporter-*.tar.gz
./node_exporter

```
## Query Metrics:

Use PromQL to query metrics from the Prometheus UI.
Example: Query CPU usage
```
node_cpu_seconds_total
 
```

# Tools and Best Practices:
## Prometheus Exporters:

Use exporters to gather metrics from various services (e.g., Node Exporter, Blackbox Exporter).
Configuration: Define exporters in prometheus.yml.

##PromQL:

Learn Prometheus Query Language (PromQL) for advanced querying.
Example: Calculate CPU usage rate
```
rate(node_cpu_seconds_total[5m])

```
## Alerting:

Integrate with Alertmanager to handle alerts.

Configuration: Define alert rules in prometheus.yml.
```
alerting:
  alertmanagers:
    - static_configs:
        - targets: ['localhost:9093']

rule_files:
  - "alert.rules"

```
Example alert rule (alert.rules):
```
groups:
- name: example
  rules:
  - alert: HighCPUUsage
    expr: rate(node_cpu_seconds_total[5m]) > 0.8
    for: 2m
    labels:
      severity: critical
    annotations:
      summary: "High CPU usage detected"
      description: "CPU usage is above 80% for more than 2 minutes."

```

