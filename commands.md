# Docker Commands I Keep Handy

This is my small Docker reference for day-to-day DevOps work. I prefer checking the state first, then looking at logs or inspecting the container instead of guessing.

## Check containers

```bash
docker ps
docker ps -a
docker compose ps
```

Use `docker ps -a` when a container disappeared from the normal `docker ps` output.

## Logs

```bash
docker logs <container>
docker logs -f <container>
docker compose logs -f vote
docker compose logs --tail=100 db
```

## Enter a running container

```bash
docker exec -it <container> sh
docker compose exec vote sh
```

## Inspect a problem

```bash
docker inspect <container>
docker stats
docker top <container>
docker port <container>
```

## Images

```bash
docker images
docker image inspect <image>
docker history <image>
docker system df
```

## Build

```bash
docker build -t voting-vote:local ./vote
docker build --no-cache -t voting-vote:local ./vote
docker build --progress=plain -t voting-vote:local ./vote
```

Use `--no-cache` only when I have a reason to suspect a stale layer. Otherwise I want the cache to work.

## Compose

```bash
docker compose config
docker compose build
docker compose up -d
docker compose ps
docker compose logs -f
docker compose down
docker compose down -v
```

Be careful with `down -v` because it removes named volumes such as the PostgreSQL data volume.

## Networking

```bash
docker network ls
docker network inspect <network>
docker inspect <container> | grep -A 20 Networks
```

## Volumes

```bash
docker volume ls
docker volume inspect db-data
docker volume prune
```

## Cleanup

```bash
docker container prune
docker image prune
docker builder prune
docker system df
```

I check `docker system df` before deleting things when the machine is getting low on disk.

## Quick troubleshooting flow

```text
container stopped
  -> docker ps -a
  -> docker logs <container>
  -> docker inspect <container>
  -> check environment/network/volume
  -> reproduce after the fix
```

## Compose config check

```bash
docker compose config -q
```

I use this before starting a changed Compose file because it catches YAML and interpolation problems early.
