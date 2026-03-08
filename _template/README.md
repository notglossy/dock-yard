# Service Name

Brief one-sentence description of what this service does.

**Links:** [Homepage](https://example.com) · [Docker Hub](https://hub.docker.com) · [Docs](https://docs.example.com)

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
| `PUID` | User ID for file permissions | `1000` |
| `PGID` | Group ID for file permissions | `1000` |
| `TZ` | Timezone | `America/New_York` |
| `CONFIG_PATH` | Path to store config files | `/opt/appdata` |
| `PORT` | Port exposed on the host | `8080` |

## Notes

- Any gotchas, post-install steps, or configuration tips go here.
- Link to relevant docs if setup is non-obvious.
