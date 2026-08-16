---
type: note
tags:
  - computer-science
  - home-labbing
relations:
  - "[[Admin Homelab setup]]"
---
pi
phineas123

curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

sudo usermod -aG docker $USER

newgrp docker

docker run hello-world

sudo apt-get update
sudo apt-get install -y docker-compose-plugin

docker compose version

/home/pi/homelab/
├── homeassistant/
│   ├── docker-compose.yml
│   └── config/                
│
├── grafana/
│   ├── docker-compose.yml
│   └── data/                  
│
├── influxdb/
│   ├── docker-compose.yml
│   └── data/ 


Home assistant
```
services:
  homeassistant:
    container_name: homeassistant
    image: ghcr.io/home-assistant/home-assistant:stable
    volumes:
      - ./config:/config
      - /etc/localtime:/etc/localtime:ro
    environment:
      - TZ=Europe/London
    restart: unless-stopped
    network_mode: host
```

Grafana
```
services:
  grafana:
    container_name: grafana
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    volumes:
      - ./data:/var/lib/grafana
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    restart: unless-stopped
    networks:
      - monitoring

networks:
  monitoring:
    external: true
```

Influxdb
```
services:
  influxdb:
    container_name: influxdb
    image: influxdb:2.7
    ports:
      - "8086:8086"
    volumes:
      - ./data:/var/lib/influxdb2
    environment:
      - DOCKER_INFLUXDB_INIT_MODE=setup
      - DOCKER_INFLUXDB_INIT_USERNAME=admin
      - DOCKER_INFLUXDB_INIT_PASSWORD=adminadmin
      - DOCKER_INFLUXDB_INIT_ORG=home
      - DOCKER_INFLUXDB_INIT_BUCKET=homeassistant
    restart: unless-stopped
    networks:
      - monitoring

networks:
  monitoring:
    external: true
```


`docker network create monitoring`

https://www.hacs.xyz/docs/use/download/download/#to-download-hacs