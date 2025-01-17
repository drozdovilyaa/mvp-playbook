# Prometheus and Grafana setup

This guide will help you set up a Prometheus and Grafana stack for basic monitoring. We will integrate it with Traefik to collect and visualize access logs.

## Start Prometheus and Grafana stack

You can use Portainer for a simplified installation process or alternatively manage the setup manually by copying the necessary files and running a command.

### Option 1: Using Portainer

1. Log in to Portainer.

2. Navigate to Stacks and click Add Stack.

3. Upload the `prometheus_grafana.yml` file from the `docker/prometheus_grafana` folder or paste its contents into the editor.

4. Update any required environment variables within Portainer (if needed).

5. Deploy the stack.

### Option 2: Manual Setup

1. Copy the necessary files from the `docker/prometheus_grafana` folder to your server.

2. Update the `.env` file in the `docker/prometheus_grafana` folder with your environment variables.  

3. Start the Prometheus and Grafana stack:

   ```bash  
   sudo docker compose -f ~/docker/prometheus_grafana/prometheus_grafana.yml up -d  
   ```  

4. Open the Grafana dashboard in your web browser to confirm it is accessible.

## Configure Grafana to Use Prometheus

1. Log in to Grafana.
2. Go to Configuration > Data Sources and click Add data source.
3. Select Prometheus.
4. Enter the Prometheus server URL (e.g., http://prometheus:9090).
5. Click Save & Test to verify the connection.

## Import a Dashboard for Traefik Metrics

1. In Grafana, go to Dashboards > Import.
2. Use a pre-built dashboard:
3. Visit Grafana Dashboards and search for "Traefik".
4. Enter the dashboard ID and click Load.
5. Select the Prometheus data source and import the dashboard.

## Verify and Customize

1. Explore the dashboard to view Traefik metrics such as:
2. Request counts
3. Response times
4. HTTP status codes
