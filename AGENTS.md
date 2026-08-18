# Portfolio Home Notes

This repository contains the static portfolio homepage published as `GDelvoye/portfolio`.

## App

- The site is static HTML/CSS served by Nginx from a Docker container.
- Local URL on the Docker host: `http://localhost:8090/`.
- Local network URL from another machine: `http://192.168.1.17:8090/`.
- The Docker Compose service name and container name are both `portfolio-home`.

## Common Commands

Run or rebuild the site:

```bash
docker compose up -d --build
```

Check status:

```bash
docker compose ps
```

Stop the site:

```bash
docker compose down
```

## Traffic Logs

- Nginx writes access logs to `logs/access.log` through the Compose bind mount `./logs:/var/log/nginx`.
- Nginx writes error logs to `logs/error.log`.
- `logs/` is local runtime data and must stay ignored by Git.
- If the container is recreated, logs remain on disk because they are bind-mounted from the host.

## Local Stats With GoAccess

GoAccess is used as a local-only log analyzer. It reads Nginx access logs and generates an HTML report with visits, page views, referrers, user agents, and similar HTTP-log statistics. The site does not include analytics JavaScript or cookies.

Generate a local report:

```bash
mkdir -p stats
docker run --rm \
  -v "$PWD/logs:/logs:ro" \
  -v "$PWD/stats:/stats" \
  allinurl/goaccess:latest \
  /logs/access.log --log-format=COMBINED -o /stats/report.html
```

Open the generated file locally:

```bash
xdg-open stats/report.html
```

Notes:

- `stats/` is generated output and must stay ignored by Git.
- The report is local only; do not expose it publicly unless access control is added.
- If `logs/access.log` is empty or missing, visit the site once and rerun the command.

## GitHub

- Remote repository: `https://github.com/GDelvoye/portfolio`.
- Main branch: `main`.
- Keep commits small: separate content/design changes from deployment or analytics changes.
