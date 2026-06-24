# Issue: Build cache was not being reused

## What I was doing

I wanted a small source-code change to rebuild quickly.

## What happened

Docker rebuilt dependency installation too.

## What I checked

I looked at the Dockerfile order and noticed dependency files were being copied together with application code.

## Fix

I copied dependency files first and installed dependencies before copying the rest of the source.

## What I learned

Docker cache works layer by layer, so Dockerfile order matters.
