---
type: note
tags:
  - computer-science
  - home-labbing
relations: "[[Admin Homelab setup]]"
---
# Virgin Admin Panel
http://192.168.0.1
Password: RileyRacoon26
# Raspberry PI (Services)
Hostname: pi-services
Username: pi
Password: phineas123
### Containers
Project exfil everything
- Another section for monitoring
Plex
- Overseerr
- http://192.168.0.157:5055/users/1/requests?filter=all
- QBittorrent: admin:RileyRacoon26
- http://192.168.0.157:8080/
- Radarr: kermit:RileyRacoon26
- http://192.168.0.157:7878/
- Sonarr: kermit:RileyRacoon26
- http://192.168.0.157:8989/
- Prowlarr: kermit:RileyRacoon26
- http://192.168.0.157:9696/
- Plex
- http://192.168.0.157:32400/web/
- AudioBookShelf admin:RileyRacoon26
- http://192.168.0.157:13378/
Home Assistant
Minecraft Server
Glance
InfluxDB
Monitoring
- Grafana http://192.168.0.157:3000/ admin:RileyRacoon26
- Prometheus
# Raspberry PI (Storage)
Hostname: pi-storage
Username: pi
Password: phineas123

# CloudFlared
prometheus-tunnel
583436ff-6404-4b45-b365-cb3136ef5e16
overseerr.project-prometheus.online
plex.project-prometheus.online

```
tunnel: 583436ff-6404-4b45-b365-cb3136ef5e16
credentials-file: /home/pi/.cloudflared/583436ff-6404-4b45-b365-cb3136ef5e16.json

ingress:
  - hostname: overseerr.project-prometheus.online
    service: http://localhost:5055
    
  - service: http_status:404
```

Have a look into setting up something like this:
https://nginxproxymanager.com/