# result frontend — Node
FROM node:18-slim AS deps
WORKDIR /usr/local/app
COPY voting-app/result/package*.json ./
RUN npm ci --omit=dev && npm cache clean --force

FROM node:18-slim AS dev-deps
WORKDIR /usr/local/app
COPY voting-app/result/package*.json ./
RUN npm ci && npm cache clean --force

FROM node:18-slim AS base
RUN apt-get update \
    && apt-get install -y --no-install-recommends curl tini \
    && rm -rf /var/lib/apt/lists/* \
    && useradd --create-home --uid 10001 appuser
WORKDIR /usr/local/app
COPY --from=deps /usr/local/app/node_modules ./node_modules
COPY voting-app/result/ .
RUN chown -R appuser:appuser /usr/local/app
USER appuser
ENV PORT=80
EXPOSE 80
ENTRYPOINT ["/usr/bin/tini", "--"]
CMD ["node", "server.js"]

FROM base AS dev
USER root
RUN npm install -g nodemon
COPY --from=dev-deps /usr/local/app/node_modules ./node_modules
RUN chown -R appuser:appuser /usr/local/app
USER appuser
