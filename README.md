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

## Local Traffic Stats

Nginx access logs are persisted locally in `logs/access.log`. The `logs/` directory is ignored by Git.

To generate a local HTML report with GoAccess:

```bash
mkdir -p stats
docker run --rm \
  -v "$PWD/logs:/logs:ro" \
  -v "$PWD/stats:/stats" \
  allinurl/goaccess:latest \
  /logs/access.log --log-format=COMBINED -o /stats/report.html
```

Then open `stats/report.html` locally.

GoAccess is a lightweight log analyzer: it reads standard web server logs and turns them into visitor/page-view statistics without adding tracking JavaScript or cookies to the website.
