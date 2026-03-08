# Pi-hole + dnscrypt-proxy (Custom Server)

Pi-hole for network-wide ad blocking with dnscrypt-proxy routing all DNS queries over DoH to a specific upstream server of your choosing.

**Links:** [Pi-hole](https://pi-hole.net) · [Pi-hole Docker](https://hub.docker.com/r/pihole/pihole) · [dnscrypt-proxy](https://github.com/DNSCrypt/dnscrypt-proxy) · [klutchell/dnscrypt-proxy](https://hub.docker.com/r/klutchell/dnscrypt-proxy)

---

## Quick Start

```bash
cp .env.example .env
# Edit .env with your values
# Edit the configs block in docker-compose.yml with your server name and stamp
docker compose up -d
```

## Choosing a Server

You have two options for picking an upstream DoH server:

- **Use an existing public server** — browse the [public servers list](https://dnscrypt.info/public-servers/) to find a server name and its stamp
- **Use your own DoH provider** — generate a stamp for any DoH URL using the [stamp calculator](https://dnscrypt.info/stamps/)

Update the `configs` block in `docker-compose.yml` with your chosen `server_names` value and the corresponding `stamp`.

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `TZ` | Timezone | `America/New_York` |
| `FTLCONF_webserver_api_password` | Pi-hole web UI password | — |
| `PIHOLE_WEB_PORT` | Host port for the web UI | `80` |
| `FTLCONF_dns_revServers` | Reverse DNS config for local network | — |
| `TEMPERATUREUNIT` | Dashboard temp unit (`f` or `c`) | `f` |

## Notes

- DNS port 53 is exposed on both TCP and UDP — make sure nothing else is using it on the host (e.g. `systemd-resolved`).
- dnscrypt-proxy runs on port 5053 internally and is not exposed to the host.
- `FTLCONF_dns_revServers` enables local hostname resolution. Format: `true,<CIDR>,<router>#53,<local domain>` — leave blank to disable.
- To find your Pi-hole version: `docker exec pihole pihole -v`
