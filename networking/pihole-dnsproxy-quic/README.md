# Pi-hole + dnsproxy (DNS over QUIC)

Pi-hole for network-wide ad blocking with AdGuard's dnsproxy routing all DNS queries over DNS over QUIC (DoQ) to AdGuard's unfiltered DNS servers.

**Links:** [Pi-hole](https://pi-hole.net) · [Pi-hole Docker](https://hub.docker.com/r/pihole/pihole) · [dnsproxy](https://github.com/AdguardTeam/dnsproxy) · [dnsproxy Docker](https://hub.docker.com/r/adguard/dnsproxy)

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
- dnsproxy listens on port 5053 internally and is not exposed to the host.
- `FTLCONF_dns_revServers` enables local hostname resolution. Format: `true,<CIDR>,<router>#53,<local domain>` — leave blank to disable.
- To enable Pi-hole's built-in DHCP server, uncomment `cap_add: NET_ADMIN` in the compose file.
- To find your Pi-hole version: `docker exec pihole pihole -v`
