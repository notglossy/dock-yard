# PostgreSQL + Auto Backup

PostgreSQL with automatic scheduled backups via `postgres-backup-local`. Backups are written to an NFS mount by default, with configurable retention for daily, weekly, and monthly snapshots.

**Links:** [PostgreSQL Docker](https://hub.docker.com/_/postgres) · [postgres-backup-local](https://github.com/prodrigestivill/docker-postgres-backup-local)

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
| `POSTGRES_DB` | Database name | — |
| `POSTGRES_USER` | Database user | — |
| `POSTGRES_PASSWORD` | Database password | — |
| `BACKUP_SCHEDULE` | Cron schedule for backups | `@daily` |
| `BACKUP_KEEP_DAYS` | Number of daily backups to retain | `7` |
| `BACKUP_KEEP_WEEKS` | Number of weekly backups to retain | `4` |
| `BACKUP_KEEP_MONTHS` | Number of monthly backups to retain | `6` |
| `NFS_HOST` | NFS server hostname or IP | — |
| `NFS_PATH` | NFS export path for backup storage | — |

## Notes

- Backups are stored at `/backups` inside the container, mapped to an NFS volume on the host. To use local storage instead, remove the `driver`, `driver_opts` block from the `postgres-backups` volume in `docker-compose.yml` and leave it as a plain named volume.
- `BACKUP_SCHEDULE` accepts cron expressions or shorthands like `@daily`, `@hourly`, `@weekly`.
- The backup service waits for PostgreSQL to pass its healthcheck before starting.
