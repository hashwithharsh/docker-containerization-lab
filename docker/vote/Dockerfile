# vote frontend image
FROM python:3.11-slim AS base
WORKDIR /usr/local/app
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1
COPY voting-app/vote/requirements.txt ./requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

FROM base AS final
RUN apt-get update \
    && apt-get install -y --no-install-recommends curl \
    && rm -rf /var/lib/apt/lists/* \
    && useradd --create-home --uid 10001 appuser
COPY voting-app/vote/ .
RUN chown -R appuser:appuser /usr/local/app
USER appuser
EXPOSE 80
CMD ["gunicorn", "app:app", "-b", "0.0.0.0:80", "--log-file", "-", "--access-logfile", "-", "--workers", "3", "--keep-alive", "0"]
