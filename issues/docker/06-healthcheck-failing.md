# Issue: Container was running but health check failed

## What I checked

```bash
docker ps
docker inspect <container>
docker logs <container>
```

## Lesson

A running container does not automatically mean the application inside it is ready. The health check needs to test something meaningful.
