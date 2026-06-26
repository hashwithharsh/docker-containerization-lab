# Issue: Redis was not ready

## Checks

```bash
docker compose ps
docker compose logs redis
docker inspect <redis-container>
```

## Lesson

I check the health status and Redis logs before restarting the whole stack.
