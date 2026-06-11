# Containerized Multi-Service Voting App

This project uses Docker's Example Voting App as the application workload. The application source is kept from the upstream sample; my work is focused on the Docker side: image builds, Dockerfiles, Compose, networking, health checks, persistent storage, image size and troubleshooting.

## Application pieces

- `vote/` - Python voting frontend
- `result/` - Node.js result frontend
- `worker/` - .NET worker that moves votes from Redis to PostgreSQL
- `redis` - temporary vote queue
- `db` - PostgreSQL database
- `seed-data/` - optional test data generator

## Docker work in this repository

1. Compared the upstream Dockerfiles and Compose file.
2. Added project-managed Dockerfiles for vote, result and worker.
3. Used multi-stage builds where they give a clear benefit.
4. Kept dependency layers before source-code layers so builds can use cache.
5. Added `.dockerignore` files to reduce build context.
6. Added a production-style Compose file without source-code bind mounts.
7. Kept PostgreSQL data in a named volume.
8. Used separate front and back networks.
9. Added health checks and health-based startup conditions.
10. Added troubleshooting notes for common Docker/Compose failures.

## Run the sample development setup

```bash
docker compose up -d

docker compose ps
```

Open the vote app on port `8080` and the result app on port `8081`.

To seed sample votes:

```bash
docker compose --profile seed up -d
```

## Run the production-style Compose file

```bash
docker compose -f docker-compose.prod.yml build
docker compose -f docker-compose.prod.yml up -d
docker compose -f docker-compose.prod.yml ps
```

## Useful checks

```bash
docker compose config
docker compose logs --tail=100 vote
docker compose logs --tail=100 worker
docker compose logs --tail=100 db
docker stats
```

See [`commands.md`](commands.md) for the commands I use most often.

## Troubleshooting

Issues are separated into Docker and Compose notes under `issues/`. Each note records the problem, what I checked, the cause, the fix and what I learned.

## Upstream source

The application is based on Docker's Example Voting App sample:
https://github.com/dockersamples/example-voting-app

The application source and upstream license are retained. This repository is about my Docker learning and infrastructure work around that application.

## Before I start changing the stack

I first run `docker compose config -q`, then `docker compose ps` and the relevant service logs. This helps me separate Compose configuration problems from application problems.

## Application source layout

The original voting application files are kept together under `voting-app/`. Docker-specific files stay outside this folder so it is clear which files belong to the application and which files are part of my container work.
