# 🚢 dock-yard

My personal collection of Docker Compose stacks for self-hosted services. Built for my own homelab, but structured to be easy for anyone to pick up and deploy.

---

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) with the [Compose plugin](https://docs.docker.com/compose/install/)
- Basic familiarity with `.env` files

Each stack has its own `.env.example`. Copy it to `.env`, fill in your values, then run `docker compose up -d`.

## Using with Komodo

These stacks work with [Komodo](https://komo.do) out of the box. When deploying a stack from this repo, skip the `.env` file — instead, paste the contents of `.env.example` into the **Environment** field in the Komodo stack configuration and fill in your values there. Komodo injects them at deploy time.

---

## Stacks

### Networking

> **Note:** Cloudflare deprecated `cloudflared` as a local DoH DNS proxy. The Pi-hole stacks below use dedicated DNS proxies as drop-in replacements.

| Stack | Description |
|-------|-------------|
| [pihole-dnscrypt-default](networking/pihole-dnscrypt-default/) | Pi-hole + dnscrypt-proxy with default server list (DoH) |
| [pihole-dnscrypt-custom](networking/pihole-dnscrypt-custom/) | Pi-hole + dnscrypt-proxy with a custom upstream server (DoH) |
| [pihole-dnsproxy-quic](networking/pihole-dnsproxy-quic/) | Pi-hole + AdGuard dnsproxy with DNS over QUIC |

### Databases
| Stack | Description |
|-------|-------------|
| [postgres-auto-backup](databases/postgres-auto-backup/) | PostgreSQL with scheduled backups to NFS (configurable retention) |

### Productivity
| Stack | Description |
|-------|-------------|
| [wordpress-frankenphp](productivity/wordpress-frankenphp/) | WordPress on FrankenPHP + MariaDB, with optional Cloudflare Tunnel |
