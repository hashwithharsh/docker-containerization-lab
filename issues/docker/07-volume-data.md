# Issue: Database data disappeared during cleanup

## What happened

I used `docker compose down -v` while testing cleanup and removed the PostgreSQL named volume.

## Lesson

`docker compose down` and `docker compose down -v` are not equivalent. I now check volumes before using the `-v` option.
