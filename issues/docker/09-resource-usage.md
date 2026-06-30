# Issue: Container resource usage looked high

## Checks

```bash
docker stats
docker top <container>
docker logs --tail=100 <container>
```

## Lesson

`docker stats` gives a quick first look at CPU and memory usage before deeper investigation.

Also useful: docker compose ps && docker logs <service>
