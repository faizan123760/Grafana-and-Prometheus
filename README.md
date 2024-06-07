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
'''
wget https://dl.grafana.com/oss/release/grafana-7.5.5.linux-amd64.tar.gz
tar -zxvf grafana-7.5.5.linux-amd64.tar.gz
cd grafana-7.5.5
./bin/grafana-server

'''

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
'''
variable:
  name: node
  label: Node
  query: label_values(node_exporter_build_info, instance)

'''
