# Pi-hole + dnscrypt-proxy (Default)

Pi-hole for network-wide ad blocking with dnscrypt-proxy as the upstream DNS resolver. All DNS queries are encrypted using DNS over HTTPS (DoH) via dnscrypt-proxy's default server list.

**Links:** [Pi-hole](https://pi-hole.net) · [Pi-hole Docker](https://hub.docker.com/r/pihole/pihole) · [dnscrypt-proxy](https://github.com/DNSCrypt/dnscrypt-proxy) · [klutchell/dnscrypt-proxy](https://hub.docker.com/r/klutchell/dnscrypt-proxy)

---

## Quick Start

```bash
cp .env.example .env
# Edit .env with your values
docker compose up -d
```

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
