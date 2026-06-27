# Issue: Container was on the wrong network

## Checks

```bash
docker network ls
docker network inspect <network>
```

## Lesson

The service name works as the DNS name only when the containers share a Docker network.
