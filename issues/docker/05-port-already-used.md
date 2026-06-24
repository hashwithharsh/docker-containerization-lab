# Issue: Host port already in use

## What happened

Compose could not publish an application port because another local process/container was already using it.

## Checks

```bash
docker ps
docker compose ps
ss -lntp
```

## Fix

I stopped the old container/process or selected a different local port.
