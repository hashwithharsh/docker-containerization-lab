# Issue: Application used the wrong environment value

## What I checked

```bash
docker compose config
docker inspect <container>
```

## Lesson

I verify the rendered Compose configuration before assuming the application itself is broken.
