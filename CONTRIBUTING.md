# Contributing

Thanks for considering a contribution.

## Good first changes

- Add a small, production-shaped starter stack.
- Improve health checks or default service boundaries.
- Document environment variables and deployment notes.

## Local validation

```bash
docker compose -f node-postgres-redis/docker-compose.yml config
docker compose -f php-mariadb/docker-compose.yml config
docker compose -f python-worker/docker-compose.yml config
```

## Pull requests

- Keep examples generic and reusable.
- Prefer safe defaults, health checks, named volumes, and clear port boundaries.
- Do not include real `.env` files, passwords, API keys, database dumps, or VPS credentials.
