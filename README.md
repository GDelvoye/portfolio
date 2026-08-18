# Portfolio

Static portfolio homepage served directly from an Nginx container.

## Run Locally

```bash
docker compose up -d --build
```

The page is available at `http://localhost:8090/`.

## Stop

```bash
docker compose down
```

## Deployment

The service exposes internal port `80`. In production, place Caddy, Nginx, or another reverse proxy in front of the Docker-published port.
