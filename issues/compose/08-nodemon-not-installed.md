# Issue: Result container could not find nodemon

## What I was trying to do

I wanted the result service to restart automatically when I changed the Node.js source during local development.

## What happened

The result container started and exited because Compose was trying to run `nodemon`, but the image did not have the command available.

## What I checked

I checked the container logs first and then looked at the result Dockerfile and `package.json`. The package file did not list `nodemon` as an application dependency.

## What I found

The development Compose file was using `nodemon` while the Docker image was installing only production dependencies. There was also a source bind mount over the application directory, so simply installing a development dependency into the image's local `node_modules` would not be a good fit for this setup.

## Fix

I added a separate `dev` stage to the result Dockerfile and installed `nodemon` globally in that stage. The development Compose service now builds that target and uses `command` for the development process. The production build still uses the smaller runtime image without nodemon.

## How I checked it

I checked the generated Compose configuration and reviewed the image stages. On a machine with Docker available, I would verify it with:

```bash
docker compose config -q
docker compose build result
docker compose up result
docker compose logs result
```

## What I learned

Development tooling does not always belong in the production image. Keeping a separate development stage lets me use a tool such as nodemon locally without adding it to the production runtime.
