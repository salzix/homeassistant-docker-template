# homeassitant-docker-template
Home Assistant and InfluxDB2 Docker-compose templates for Raspberry Pi OS. Contains both applications. HA has access to USB0 for ZigBee gate.

## Requirements
* Raspberry Pi OS or other Linux OS
* Docker Engine installed

## Configuration
You may need to adjust directory permissions.

You'll need to generate access token to allow connecting HA to InfluxDB2. This token is generated inside InfluxDB2, so run `docker compose up innfluxdb`. Choose your Organization Name (something simple and without spaces and special chars!) and follow https://docs.influxdata.com/influxdb/cloud/security/tokens/create-token/
Once you have token, close InfluxDB2 (Ctrl+C).

You'll need to paste your OrgName and token to several files:
* config/configuration.yaml - replace "ReplaceMeWithToken" and "ReplaceMeWithYourOrganizationName" with token and OrgName respectively.
* influxdb2-config/infulx-configs - replace "ReplaceMeWithToken" and "ReplaceMeWithYourOrganizationName" with token and OrgName respectively.
* .env - replace "ReplaceMeWithToken" with token.

## Running
`docker compose up -d` runs this stack.

GUI:
* RPi-IP:8123 - Home Assistant
* RPi-IP:8086 - InfluxDB2
