# Issue: One container could not reach another service

## Checks

```bash
docker network ls
docker network inspect <network>
docker exec -it <container> sh
```

## Lesson

I check whether both services share the expected Docker network before changing application configuration.
