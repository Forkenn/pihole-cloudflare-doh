# pihole-cloudflare-doh
Docker Compose configuration to run Pi-hole with Cloudflared as DNS resolver via DNS-over-HTTPS (DoH). The solution provides privacy, DNS filtering and anti-tracking protection. It is based on the [official Docker Compose file](https://github.com/pi-hole/docker-pi-hole) for Pi-hole.

# Composition
* pihole: official main container for DNS filtering
* cloudflared: official proxy implementing DNS-over-HTTPS

# Requirements
* Docker
* Docker Compose
* Open ports: 53 (DNS), 80/443 (optional, for Pi-hole web interface)

# Installation and startup
1. Clone repo:
```shell script
git clone https://github.com/Forkenn/pihole-cloudflare-doh.git
cd pihole-cloudflare-doh
```
2. Edit the .env.example file by putting your password in there with *vi, vim or nano* and rename it to .env:
```shell script
cp .env.example .env
```
3. Run the Compose:
```shell script
docker-compose up -d    # or 'docker compose up -d' in some systems
```
4. Configure the system configuration to use local DNS at 127.0.0.1 or at the address of the device where the Pi-hole is installed on the local network.

Additionally, you can change some container configurations in docker-dompose.yml. For example, you can configure Pi-hole as DHCP or/and NTP.

# Configuration
Configuration of the Pi-hole Docker service (such as DHCP, NTP, etc.) is described in the [official repo](https://github.com/pi-hole/docker-pi-hole). Cloudflared configuration is described in the [official docs](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks) and on the [Pi-hole documentation page](https://docs.pi-hole.net/guides/dns/cloudflared).

# Project structure
    .
    ├── docker-compose.yml
    ├── etc-pihole/
    │   └── ...
    ├── etc-dnsmasq.d/
    │   └── ...
    ├── .env
    └── README.md

# Security
Use a strong password in the .env file and a firewall to restrict outside access to DNS if you don't need it.

There is a known problem with iptables/ufw controlled ports, solved through [iptables configuration](https://docs.docker.com/engine/network/packet-filtering-firewalls/), the [ufw-docker](https://github.com/chaifeng/ufw-docker) utility or its analogs.

# Notes
If something doesn't work:
* Make sure your router/device uses Pi-hole as the primary DNS
* Make sure you create an **.env** in the root of the project file with the password to access the Pi-hole web interface
* Cloudflared may require you to configure certificates or API tokens for some features (depending on **your** configuration and usage case, not applicable to the default configuration)

# Useful links
* [Pi-hole docs](https://docs.pi-hole.net)
* [Pi-hole Docker Compose Repo](https://github.com/pi-hole/docker-pi-hole)
* [Cloudflared docs](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks)
* [Cloudflared Docker Image](https://hub.docker.com/r/cloudflare/cloudflared)
* [Docker Compose docs](https://docs.docker.com/compose)

# Feedback
Please report issues on the [GitHub project](https://github.com/Forkenn/pihole-cloudflare-doh) when you suspect something.