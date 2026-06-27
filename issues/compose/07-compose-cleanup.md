# Issue: Cleanup removed more than expected

## What I checked

```bash
docker compose ps
docker volume ls
docker network ls
```

## Lesson

I now inspect the resources first and only use volume removal when I really want a fresh database.
