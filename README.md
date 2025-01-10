# Digitalisation AIO Package

The **Digitalisation AIO (All-In-One) Package** is a comprehensive Docker-based stack that integrates tools for automation, data management, and visualisation. It is designed to facilitate efficient workflows, seamless communication, and insightful analysis.

## Components
- **Node-RED**: Automates workflows and orchestrates communication.
- **PostgreSQL**: Manages and stores timeseries data.
- **Mosquitto**: Enables MQTT-based messaging between services.
- **Grafana**: Provides data visualisation and analytics.

---

## Key Features
- Pre-configured Mosquitto broker with secure authentication.
- Node-RED flows demonstrating:
  - MQTT communication.
  - PostgreSQL integration for database creation and data management.
- Ready-to-use Grafana dashboard template for visualising time-series data.

---

## Quick Start

### Prerequisites
1. **Docker Desktop** with WSL2 (Ubuntu).
2. Docker Desktop should be linked to your WSL2 instance.

### Setup Steps
1. Clone this repository.
2. Configure the `.env` file with your preferred credentials.
- Set your PostgreSQL password.
- Define Grafana admin credentials.
3. Launch the stack:
```
docker-compose up -d
```
4. Access the services:
- Node-RED: [http://localhost:1880](http://localhost:1880)
- Grafana: [http://localhost:3000](http://localhost:3000)
