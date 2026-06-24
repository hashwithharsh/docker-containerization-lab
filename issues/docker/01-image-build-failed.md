# Issue: Docker image build failed

## What I was doing

I was rebuilding the vote image after changing its Dockerfile.

## What happened

The build stopped during the dependency installation step.

## What I checked

I checked the failing Dockerfile layer and rebuilt with:

```bash
docker build --progress=plain -t voting-vote:local ./vote
```

## What I learned

The normal build output can hide useful detail. `--progress=plain` makes the failing command easier to see.
