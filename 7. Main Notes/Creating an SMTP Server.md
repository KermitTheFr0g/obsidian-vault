---
type: note
tags:
  - computer-science
  - software-engineering
---
# NodeJS SMTP Server
Using `smtp-server` and `mailparser` to receive the mail through the SMTP Server.

## Hosting on AWS EC2
- Creating ssh key on instance
	- Adding SSH key to deploy keys on the smtp server GitHub repo
- Pulling down repo
- Installing pm2 `npm i -g pm2`
- Building node project `npm run build`
- Run using pm2 on port `2525` - `pm2 start dist/index.js --name smtp-server`
- Because we are running on port 2525 we need all traffic to be routed from 25 to 2525 we can do this using `iptables` - `sudo iptables -t nat -A PREROUTING -p tcp --dport 25 -j REDIRECT --to-port 2525`

## Adding to DNS Records
We need a static IP to add to our DNS records for this we can use an AWS Elastic IP.
- Add the IP an `A Record` as `mail`
- Add an `MX Record` pointing to `mail.{domain_name}`