# Issue: Container exited immediately

## What happened

A container was present in `docker ps -a` but was not running.

## Checks

```bash
docker ps -a
docker logs <container>
docker inspect <container>
```

## Lesson

The exit status and logs are the first things I check before changing the image.
