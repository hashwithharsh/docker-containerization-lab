# Issue: Service started before its dependency was ready

## What happened

A service could start while Redis or PostgreSQL was still initializing.

## Fix

Compose was configured with health-based dependency conditions where startup order mattered.

## Lesson

`depends_on` by itself is not the same as application readiness.
