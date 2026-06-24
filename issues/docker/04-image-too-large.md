# Issue: Image was larger than expected

## What I checked

```bash
docker images
docker history <image>
```

I found packages and build dependencies that did not need to be present in the final runtime image.

## Fix

I used a multi-stage build for the result and worker services and kept build dependencies in the builder stage.

## Lesson

The runtime image only needs what is required to run the application.
