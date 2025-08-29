# Copilot Instructions for Akiba

## Project Overview
- This repository provides a modular Docker Compose stack for self-hosting a wide range of services, with a focus on security, backup, monitoring, and usability.
- The stack is designed for homelab users who want sane defaults and easy extensibility.

## Architecture & Structure
- All service definitions are under `compose/`, each in its own subdirectory (e.g., `compose/traefik/`, `compose/authelia/`).
- Each service or group has its own `compose.yaml` and related config files.
- Root-level `compose.yaml` and `compose.prod.yaml` aggregate or override service definitions for different environments.
- SSL termination is handled by HAProxy, which sits in front of Traefik. Traefik is used only to reverse proxy all user-facing Docker services, with Authelia for authentication and Crowdsec for security.
- Cetusguard proxies the Docker socket for enhanced security.

## Key Patterns & Conventions
- Secrets management and environment variables are handled through [Infisical](https://infisical.com/). Infisical is used to inject variables prior to executing `docker compose up`. Do not hardcode secrets; reference them via Infisical-managed environment variables.
- Compose files use environment variables for secrets, paths, and domain names. Avoid hardcoding sensitive values.
- Service configuration is kept in subfolders (e.g., `config/`, `rules/`, `initdb.d/`) within each service directory.
- Compose files may use `extends` for modularity and DRY principles.
- All persistent data should be mapped to `${DATA_DIR}` or similar variables.
- For large, user-provided files (such as photos or media), use a separate `${MEDIA_DIR}` variable to keep user data organized and distinct from configuration or service data.
- Use the provided `Makefile` for common workflows (if present).

## Developer Workflows
- To start the stack: `docker compose up -d` (use `compose.yaml` or `compose.prod.yaml` as needed).
- To update services: Use Renovate (see `renovate.json`) or update images in compose files.
- For logs: Use Dozzle or check container logs via Docker CLI.
- For monitoring: Use the monitoring tools currently configured in the stack (see `compose/` for available options).
- For backups: Use the `backup/` and `restic/` services and configs.

## Integration & Communication
- All services are routed through Traefik, which handles SSL, routing, and authentication via Authelia.
- Crowdsec integrates with Traefik for security enforcement.
- Inter-service communication is managed via Docker networks defined in compose files.

## Examples
- To add a new service, create a new subfolder in `compose/`, add a `compose.yaml`, and update the root compose file if needed.
- To override a config, place your file in the appropriate `config/` subfolder and map it in the compose file.

## References
- See `README.md` for a list of included services and project goals.
- See `compose/` for all service definitions and configurations.
- See `Makefile` for automation (if present).

---
When writing or editing code/configuration:
- Follow the existing directory and compose file structure.
- Use environment variables for all secrets and paths.
- Prefer modular, DRY patterns (use `extends` where possible).
- Document any new service or workflow in the README or relevant config folder.
- Use conventional commit messages for all changes.
