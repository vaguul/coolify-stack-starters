# coolify-stack-starters

![Validate](https://github.com/vaguul/coolify-stack-starters/actions/workflows/validate.yml/badge.svg)
![MIT License](https://img.shields.io/badge/license-MIT-8fe3c7)

Small starter stacks for self-hosted apps on Docker or Coolify, maintained by Vaguul under the Zemiax personal software studio.

The goal is simple: start from a clean template instead of rebuilding the same PHP, Node, database, and worker setup every time.

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

## Healthcheck expectations

Use these checks after deploying a starter locally or through Coolify:

| Starter | Public surface | Internal services | Healthy when |
| --- | --- | --- | --- |
| `node-postgres-redis` | `api` on `${API_PORT:-3000}` | `postgres`, `redis` | Postgres answers `pg_isready`, Redis answers `PING`, and the API starts after both dependencies are healthy. |
| `php-mariadb` | `app` on `${APP_PORT:-8080}` | `mariadb` | MariaDB answers `mariadb-admin ping` and the app starts after the database is healthy. |
| `python-worker` | none by default | `worker` | The worker container stays running with `restart: unless-stopped` and does not require an inbound public port. |

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
