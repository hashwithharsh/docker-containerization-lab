# Compose notes

The main development Compose file is the upstream sample. `docker-compose.prod.yml` is the version I changed for this project so it builds the application images from the repository root and does not use source-code bind mounts.

Before starting a changed file, I check it with:

```bash
docker compose -f docker-compose.prod.yml config -q
```
