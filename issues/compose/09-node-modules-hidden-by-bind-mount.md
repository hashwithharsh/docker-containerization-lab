# Result dependencies hidden by bind mount

## What I was trying to do

I wanted the result service to use a bind mount in development so I could change the
Node.js source without rebuilding the image every time.

## What happened

The result container started, but the application could not find its Node.js packages.

The Dockerfile had already installed `node_modules` inside `/usr/local/app`, so at first
I was confused about why a package such as `express` was missing.

## What I checked

I checked the container logs and then looked at the Compose volume configuration.

The development service was mounting:

```text
./voting-app/result:/usr/local/app
```

This mount hides the `/usr/local/app` contents that were created in the image, including
the image's `node_modules` directory.

## Fix

I kept the source bind mount, but added a separate named volume for dependencies:

```yaml
volumes:
  - ./voting-app/result:/usr/local/app
  - result-node-modules:/usr/local/app/node_modules
```

I also added a development dependency stage to the result Dockerfile so the development
image has all packages needed for local development.

## What I learned

A bind mount can hide files that were already present in the image at the same path.
For Node.js development containers, keeping `node_modules` in a separate volume is a
simple way to avoid losing the container's installed dependencies.
