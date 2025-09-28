# Plex Monitoring Stack

A comprehensive Docker Compose setup for a Plex media server with monitoring and management capabilities.

## Services

- **Plex**: Media server with hardware transcoding support
- **Prometheus**: Metrics collection and storage
- **Grafana**: Visualization and dashboarding
- **Dozzle**: Docker container log viewer
- **Node Exporter**: System metrics exporter
- **DCGM Exporter**: NVIDIA GPU metrics exporter
- **SmartCTL Exporter**: Disk health metrics exporter
- **cAdvisor**: Container metrics exporter
- **Plex Prometheus Exporter**: Plex-specific metrics exporter

## Prerequisites

- Docker and Docker Compose
- NVIDIA GPU with Docker GPU support (for hardware transcoding)
- Environment variables configured (see Setup section)

## Setup

1. Clone this repository
2. Copy the environment file templates and configure them:

   ```bash
   # Create environment files for each service
   cp plex/.env.example plex/.env
   cp prometheus/.env.example prometheus/.env
   cp grafana/.env.example grafana/.env
   # ... configure other .env files as needed
   ```

3. (Optional) Update the root `.env` file if you want to define shared environment variables for the stack.

4. Start the services:

   ```bash
   docker compose up -d
   ```

## Access Points

- **Plex**: <http://localhost:32400/web>
- **Grafana**: <http://localhost:3000>
- **Prometheus**: <http://localhost:9090>
- **Dozzle**: <http://localhost:8080>

## Configuration Files

- `prometheus/config/prometheus.yml`: Prometheus configuration
- `prometheus-rules` volume (`/etc/prometheus/rules` inside the container): Prometheus alerting rules
- `grafana/provisioning/`: Grafana datasources and dashboards
- `dozzle/data/users.yaml`: Dozzle user authentication

## Dashboards

This repository includes pre-configured Grafana dashboards for monitoring your Plex monitoring stack. For the most up-to-date Plex monitoring dashboards and additional configuration options, visit the [prometheus-plex-exporter repository](https://github.com/timothystewart6/prometheus-plex-exporter).

## Data Persistence

Persistent data for the stack is stored in Docker named volumes. The following volumes are created automatically:

- `prometheus-data`: Prometheus time series data
- `prometheus-rules`: Prometheus alerting rules
- `grafana-data`: Grafana dashboards, users, and settings
- `dozzle-data`: Dozzle configuration and authentication data

You can manage these volumes with Docker commands such as `docker volume ls` and `docker volume inspect`.

## Notes

- GPU support is configured for NVIDIA cards
- Prometheus retains data for 30 days
- All services are configured with security best practices (no-new-privileges)
- Services are set to restart unless explicitly stopped
- This stack provides comprehensive monitoring for Plex server performance, resource usage, and streaming analytics

## Further reading

For a walk-through and explanation of the design and dashboards used by this stack, see the accompanying blog post:

- ["Monitor your Plex Server like a Pro"](https://technotim.live/posts/monitor-your-plex-server-like-a-pro/)
