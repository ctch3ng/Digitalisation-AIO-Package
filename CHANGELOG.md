# Changelog

All notable changes to this project will be documented in this file.

## [2.0.0] - 2026-01-15

### ⚠️ BREAKING CHANGES
- **OpenPLC Runtime upgraded from v3 to v4**
  - Runtime is now headless (no web interface)
  - Requires OpenPLC Editor v4 desktop application for control
  - Port changed from 8080 to 8443 (HTTPS)
  - Programs must be uploaded via Editor, not web browser

### Added
- OpenPLC Runtime v4 with REST API interface
- JWT-based authentication for enhanced security
- WebSocket debug interface for real-time monitoring
- Support for OpenPLC Editor v4 integration
- TLS/HTTPS on port 8443

### Changed
- OpenPLC Runtime port: 8080 → 8443
- Control method: Web UI → OpenPLC Editor desktop app
- Authentication: Web form → JWT tokens

### Removed
- OpenPLC Runtime web interface at :8080
- Direct browser-based program upload

---

## [1.0.0] - 2026-01-15

### Initial Release
- Node-RED for workflow automation
- PostgreSQL for time-series data
- Mosquitto MQTT broker
- Grafana for visualization
- OpenPLC Runtime v3 with web interface
- Pre-configured demo flows and dashboards
