# Issue: PostgreSQL was not ready

## Checks

```bash
docker compose ps db
docker compose logs db
docker inspect <db-container>
```

## Lesson

PostgreSQL initialization can take longer than the application startup, so health-based dependencies are useful.
