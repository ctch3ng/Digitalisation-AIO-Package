# Digitalisation AIO Package

The **Digitalisation AIO (All-In-One) Package** is a comprehensive Docker-based stack that integrates tools for automation, data management, and visualisation. It is designed to facilitate efficient workflows, seamless communication, and insightful analysis.

## Components
- **Node-RED**: Automates workflows and orchestrates communication.
- **PostgreSQL**: Manages and stores time-series data.
- **Mosquitto**: Enables MQTT-based messaging between services.
- **Grafana**: Provides data visualisation and analytics.
- **OpenPLC Runtime**: For running PLC programs (Modbus TCP/IP Enabled) - OpenPLC Editor needed to be downloaded and installed separately [https://autonomylogic.com/](https://autonomylogic.com/).

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
1. `Windows` users: **Docker Desktop** with WSL2 (Ubuntu). Docker Desktop should be linked (integrated) to your WSL2 instance.
2. `Mac` users: **Docker Desktop** and Xcode installed.

### Setup Steps
1. Clone this repository, and update ownership.
```bash
git clone https://github.com/ctch3ng/Digitalisation-AIO-Package.git
```
🚨 For *Windows* users, run the following.
Rationale: On most Linux (Ubuntu included) systems, UID 1000 and GID 1000 typically refer to the first regular user account created and the primary group associated with the first non-system user account, respectively. You can use the command `id -u` and `id -g` to find your UID and GID.
```bash
sudo chown -R 1000:1000 Digitalisation-AIO-Package/
```
🚨 For *Mac* users, run the following instead.
Rationale: On MacOS systems, UID 501 and GID 501 typically refer to the first regular user account created and the primary group associated with the first non-system user account, respectively.
```bash
sudo chown -R 501:501 Digitalisation-AIO-Package/
```
🚨For both *Mac* and *Windows* users, run the following.

Rationale: In Node-Red, installing packages via the `Manage palette` could remove the customised DHT and Button emulators that come with this package. The following is to make a copy of them to the folder `Temp` such that we can re-apply them later when needed. 

```bash
sudo cp -r ~/Digitalisation-AIO-Package/nodered-data/node_modules/ ~/Digitalisation-AIO-Package/temp
```

2. Configure the `.env` file with your preferred credentials. (You can skip this if you just want to give it a test drive)
- Set your PostgreSQL password.
  - The default password is `05JD£AEBW2'f`.
- Define Grafana admin credentials.
  - The default username and password are `admin` and `0m{-}>7nP8)C`, respectively. 
3. Launch the stack:
```bash
cd Digitalisation-AIO-Package/
```
```bash
sudo docker compose up -d
```
🚨 If step 3 above ends up with permission issues, you may need to further run the following as well to provide adequate access rights.
```bash
sudo chmod -R 777 ~/Digitalisation-AIO-Package/
```
4. Access the services:
- Node-RED: [http://localhost:1880](http://localhost:1880)
- Grafana: [http://localhost:3000](http://localhost:3000)
- OpenPLC Runtime: [http://localhost:8080](http://localhost:8080)

# Node-RED Demo (Post-installation Steps)
Under `Manage palette`, search and install the following modules.
  - `node-red-contrib-postgresql`
  - `node-red-dashboard`
  - `node-red-contrib-modbus`
  - `node-red-contrib-lfo`
    
Under `Configuration nodes`, expand `digitalisation-aio-package-mosquitto-1`. Enter the following information under `Security`
- Username: `mqtt_user1`
- Password: `P71X95tQ!]tm`

Return to your Ubuntu or Terminal, and run the following to install the DHT and button emulators.
```bash
cd ~/Digitalisation-AIO-Package/
cp -r ~/Digitalisation-AIO-Package/temp/* ~/Digitalisation-AIO-Package/nodered-data/node_modules/
sudo docker compose stop
sudo docker compose start
```


# Grafana Dashboard Demo (Post-installation Steps)
 - Under `Data sources`, add PostgreSQL with the following information.
   - Host URL: `digitalisation-aio-package-postgres-1:5432`
   - Database name: `postgres`
   - Username: `postgres`
   - Password: `05JD£AEBW2'f`
   - TLS/SSL Mode: `disable`
   - TimescaleDB: `enable`
 - Import the `Dashboard Demo.json` from the `grafana-data/` directory into Grafana via Dashboards -> Import. 
 - Edit `Sensor 1` and `Sensor 2` panels. Select `grafana-postgresql-datasource` as the source.

Note: Docker containers can reach out to each other via their container names; by default, they are
 - NodeRed: `digitalisation-aio-package-nodered-1`
 - PostgreSQL: `digitalisation-aio-package-postgres-1`
 - Mosquitto: `digitalisation-aio-package-mosquitto-1`
 - Grafana: `digitalisation-aio-package-grafana-1`
 - OpenPLC Runtime: `digitalisation-aio-package-openplc-runtime-1`

# [Optional] Updating Mosquitto's credentials (Again, you can skip this if you just want to give it a test drive)
- Enter the Mosquitto container:
```bash
docker exec -it digitalisation-aio-mosquitto sh
```
  - (Use `docker ps` to confirm the container name. Here, the name in the example is `digitalisation-aio-mosquitto`)

- Navigate to the password file directory:
```bash
cd /mosquitto/config
```
- Update the password file (Here, the default username and password are `mqtt_user1` and `P71X95tQ!]tm`, respectively):
```bash
rm passwordfile
echo "mqtt_user1:P71X95tQ!]tm" > passwordfile
chmod 0700 passwordfile
```
- Hash the password file:
```bash
mosquitto_passwd -U passwordfile
```
- Exit the container:
```bash
exit
```
