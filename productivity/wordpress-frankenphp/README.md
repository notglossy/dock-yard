# WordPress + FrankenPHP

WordPress running on FrankenPHP with MariaDB, connected via Unix socket for maximum performance. Optionally exposed via a Cloudflare Tunnel — no open ports required.

**Links:** [WordPress](https://wordpress.org) · [FrankenPHP](https://frankenphp.dev) · [frankenpress image](https://github.com/notglossy/frankenpress) · [MariaDB Docker](https://hub.docker.com/_/mariadb) · [cloudflared](https://hub.docker.com/r/cloudflare/cloudflared)

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
| `SITE_URL` | Full public URL of your site | `https://example.com` |
| `SERVER_NAME` | FrankenPHP server name directive | `example.com, :80` |
| `WP_ENVIRONMENT_TYPE` | WordPress environment type | `production` |
| `MARIADB_DATABASE` | Database name | `wordpress` |
| `MARIADB_USER` | Database user | `wordpress` |
| `MARIADB_PASSWORD` | Database password | — |
| `MARIADB_ROOT_PASSWORD` | MariaDB root password | — |
| `WORDPRESS_AUTH_KEY` | WordPress secret key (optional) | — |
| `WORDPRESS_SECURE_AUTH_KEY` | WordPress secret key (optional) | — |
| `WORDPRESS_LOGGED_IN_KEY` | WordPress secret key (optional) | — |
| `WORDPRESS_NONCE_KEY` | WordPress secret key (optional) | — |
| `WORDPRESS_AUTH_SALT` | WordPress salt (optional) | — |
| `WORDPRESS_SECURE_AUTH_SALT` | WordPress salt (optional) | — |
| `WORDPRESS_LOGGED_IN_SALT` | WordPress salt (optional) | — |
| `WORDPRESS_NONCE_SALT` | WordPress salt (optional) | — |
| `CLOUDFLARE_TUNNEL_TOKEN` | Cloudflare Tunnel token (optional) | — |

## Notes

- WordPress and MariaDB communicate over a Unix socket (shared volume) rather than TCP — faster than a network connection between containers.
- MariaDB is on an isolated internal network and has no external access.
- **Secret keys/salts** are optional but recommended for production — generate them at [api.wordpress.org/secret-key/1.1/salt](https://api.wordpress.org/secret-key/1.1/salt/). Uncomment the relevant lines in `docker-compose.yml` to use them.
- **Memory limits** in the `deploy` blocks are set conservatively — adjust them to match your host.
- **Cloudflare Tunnel** is optional. Uncomment the `tunnel` service in `docker-compose.yml` and set `CLOUDFLARE_TUNNEL_TOKEN` to expose your site without opening firewall ports. Create a tunnel at [one.dash.cloudflare.com](https://one.dash.cloudflare.com/) → Networks → Tunnels.
