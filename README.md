# coolify-stack-starters

![Validate](https://github.com/vaguul/coolify-stack-starters/actions/workflows/validate.yml/badge.svg)
![MIT License](https://img.shields.io/badge/license-MIT-8fe3c7)

Small starter stacks for self-hosted apps on Docker or Coolify, maintained by Vaguul under the Zemiax personal software studio.

The goal is simple: start from a clean template instead of rebuilding the same PHP, Node, database, and worker setup every time.

Use this repository as a GitHub template when you want to copy the starters into a new project.

## Included starters

- `node-postgres-redis`
- `php-mariadb`
- `python-worker`

## Validate

```bash
docker compose -f node-postgres-redis/docker-compose.yml config
docker compose -f php-mariadb/docker-compose.yml config
docker compose -f python-worker/docker-compose.yml config
```

## Validation matrix

Use these checks after deploying a starter locally or through Coolify:

| Starter | Static validation command | Expected services | Public surface | Health behavior | Host requirements |
| --- | --- | --- | --- | --- | --- |
| `node-postgres-redis` | `docker compose -f node-postgres-redis/docker-compose.yml config` | `api`, `postgres`, `redis` | `api` on `${API_PORT:-3000}` | Postgres must answer `pg_isready`, Redis must answer `PING`, and `api` waits for both dependencies to become healthy. | Port `${API_PORT:-3000}` must be free if published on the host. Uses named volumes `postgres-data` and `redis-data`. |
| `php-mariadb` | `docker compose -f php-mariadb/docker-compose.yml config` | `app`, `mariadb` | `app` on `${APP_PORT:-8080}` | MariaDB must answer `mariadb-admin ping`, and `app` waits for the database to become healthy. | Port `${APP_PORT:-8080}` must be free if published on the host. Uses named volume `mariadb-data`. |
| `python-worker` | `docker compose -f python-worker/docker-compose.yml config` | `worker` | none by default | The worker container should stay running with `restart: unless-stopped`. No dependency healthcheck is required. | No inbound host port required. Confirm the worker has the environment variables it needs before enabling real jobs. |

For production deployments, expose only the application service that needs traffic. Databases, Redis, and background workers should stay private to the Docker network unless your provider requires a separate internal network configuration.

## Security notes

- Replace every sample password before deploying.
- Keep `.env` files out of Git.
- Bind only the ports that the application actually needs.

## Who this is for

- solo builders shipping internal tools
- small product teams on VPS + Docker
- people using Coolify and wanting cleaner starting points

## Author

Built and maintained by Vaguul for Zemiax.

## License

MIT
