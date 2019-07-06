# deconz-home-assistant-example
Docker compose example of deCONZ and Home Assistant.
Change the mount point of the two volumes and make sure that your Conbee device is at `/dev/ttyUSB0`.
Up that sh1t..

```
version: "3"
services:
  deconz:
    image: marthoc/deconz
    container_name: deconz
    network_mode: host
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /home/kerwood/conbee/deconz_data:/root/.local/share/dresden-elektronik/deCONZ
    devices:
      - /dev/ttyUSB0
    environment:
      - DECONZ_WEB_PORT=80
      - DECONZ_WS_PORT=443
      - DEBUG_INFO=1
      - DEBUG_APS=0
      - DEBUG_ZCL=0
      - DEBUG_ZDP=0
      - DEBUG_OTAU=0

  homeassistant:
    container_name: home-assistant
    image: homeassistant/home-assistant
    restart: unless-stopped
    network_mode: host
    volumes:
      - /home/kerwood/conbee/HA_config:/config
      - /etc/localtime:/etc/localtime:ro
```
