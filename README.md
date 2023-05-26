# homeassistant-docker-template
[Home Assistant](https://www.home-assistant.io/) and [InfluxDB2](https://docs.influxdata.com/influxdb/v2.2/) Docker-compose templates for Raspberry Pi OS. Contains both applications. HA has access to USB0 for ZigBee gate.

## Requirements
* Raspberry Pi OS or other Linux OS, Windows. Other systems are untested, but should work if Docker runs there
* Docker Engine installed

## Configuration
### Before you begin
* You may need to adjust mounted directory permissions to allow writes from HA and InfluxDB2 containers.
* containers run on `network_mode: host` by default, to avoid hassle with IP=127.0.0.1 address. If you want to run on localhost, you'll need to comment `network_mode: host` line in both service sections of `compose.yml` file, and uncomment sections exposing ports.

### Token for HA->InfluxDB2 access
You'll need to generate access token to allow connecting HA to InfluxDB2. This token is generated inside InfluxDB2 GUI on first run.
* run `docker compose up influxdb` and go to http:/127.0.0.1:8086 (or your RPi IP) in web browser.
* Create admin account, choose your Organization Name (something simple and without spaces and special chars!) and Bucket Name (for example: HA). Copy OrgName and token from next screen to some text editor.
* Once you have token, close InfluxDB2 container (Ctrl+C in console with running docker)

You'll need to paste your OrgName and token to files:
* config/configuration.yaml - replace "ReplaceMeWithToken" and "ReplaceMeWithYourOrganizationName" with token and OrgName respectively.
* influxdb2-config/influx-configs - replace "ReplaceMeWithToken" and "ReplaceMeWithYourOrganizationName" with token and OrgName respectively.

## Running
`docker compose up -d` runs this stack. It is configured to automatically start after host restart.

## GUI:
* your-RPi-IP:8123 - Home Assistant
* your-RPi-IP:8086 - InfluxDB2
