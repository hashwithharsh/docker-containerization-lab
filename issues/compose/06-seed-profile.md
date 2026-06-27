# Issue: Seed service did not start

## What happened

The seed service is behind the `seed` Compose profile, so a normal `docker compose up` does not start it.

## Fix

```bash
docker compose --profile seed up -d
```

## Lesson

Compose profiles are useful for optional jobs that should not run every time.
