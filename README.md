# GLPI on Debian (Docker)

This repository provides a Docker-based setup to run GLPI on Debian using docker compose.

## Prerequisites

- Docker Engine (compatible with the `docker compose` plugin)
- Docker Compose v2 (the `docker compose` command)
- Basic familiarity with Docker and environment files

## Quick start

1. Copy the sample environment file and edit it:

```bash
cp glpi.env.sample .env
# Open .env in your editor and set the required values
```

2. Build the images:

```bash
docker compose build
```

3. Start containers in detached mode:

```bash
docker compose up -d
```

Containers will start and GLPI should become available on the configured host and port. (ie. localhost:9000).

## Using an existing GLPI installation

If you already have a configured GLPI instance and want to reuse its configuration:

- Replace the files under `glpi/config/` with the corresponding configuration files from your old installation.
- Replace the files under `glpi/files/` with the corresponding configuration files from your old installation.
- Replace the files under `glpi/marketplace/` with the corresponding configuration files from your old installation.
- Replace the files under `glpi/plugins/` with the corresponding configuration files from your old installation.
- Ensure file ownership and permissions are correct for the containers (for example, `chown` to match container user if needed).
- Verify environment variables in `.env` match your existing installation before starting the containers.

## Stopping and removing

To stop the containers:

```bash
docker compose down
```

To stop and remove volumes (data will be lost):

```bash
docker compose down -v
```

## Troubleshooting

- Check container logs:

```bash
docker compose logs -f
```

- If permission issues arise after copying config files from another system, adjust ownership and permissions to match the container requirements.

## License

This repository contains configuration and helper files for running GLPI with Docker. Refer to individual components for their respective licenses.
```
