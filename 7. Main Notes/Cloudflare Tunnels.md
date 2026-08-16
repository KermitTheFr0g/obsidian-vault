---
type: note
tags:
  - computer-science
  - home-labbing
---
# Setup Cloudflare tunnel
Install cloudflared
https://pkg.cloudflare.com/index.html

verify with
```
cloudflared --version
```

login to your cloudflare account
```
cloudflared login
```

This should then create a new `.pem` file
```
~/.cloudflared/cert.pem
```

To get the current tunnels you might be running multiple
```
cloudflared tunnel list
```

Now we need to create a new tunnel
```
cloudflared tunnel create raspi-tunnel
```

Then create a new DNS for every service that you want to expose
ha -> homeassistant
glance -> glance
```

```

Create the tunnel config yml
```
sudo mkdir /etc/cloudflared
sudo nano /etc/cloudflared.config.yml
```
We need to follow the same ID that we got from creating the tunnel:
```
tunnel: a1b2c3d4-xxxx-xxxx-xxxx-abcdef123456
credentials-file: /home/pi/.cloudflared/a1b2c3d4-xxxx-xxxx-xxxx-abcdef123456.json

ingress:
  - hostname: raspi.example.com
    service: http://localhost:80
    
  - service: http_status:404
```
Each of the ingress hostnames is going to resolve one of the services on 

Multiple services would look like this:
```
ingress:
  - hostname: ha.whateverlinks.com
    service: http://localhost:8123

  - hostname: graphs.whateverlinks.com
    service: http://localhost:3000

  - hostname: glance.whateverlinks.com
    service: http://localhost:8280

  - service: http_status:404
```

Let's now test to make sure that we can connect to the running services
```
sudo cloudflared tunnel run raspi-tunnel
```
If this is successful and we can connect to the subdomain we have setup let's make sure this service is always live. 

```
sudo nano /etc/systemd/system/cloudflared.service
```

```
[Unit]
Description=Cloudflare Tunnel
After=network.target

[Service]
Type=simple
User=pi
ExecStart=/usr/local/bin/cloudflared tunnel run raspi-tunnel
Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
```

```
sudo systemctl daemon-reload
```

```
sudo systemctl enable cloudflared
```

```
sudo systemctl start cloudflared
```

```
sudo systemctl status cloudflared
```

To check the logs we can use:
```
journalctl -u cloudflared -f
```

### Multiple domains
I still need to try this out for myself but I have read online that you're able to use a single tunnel to multiple domains. As long as the domain is on your Cloudflare account it can be added to the tunnel and the domain added to the ingress file.