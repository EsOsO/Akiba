![Logo](https://github.com/EsOsO/akiba/blob/1425fb760c3c18d3905337ae477ff9356ccb3758/logo.png)

# Akiba: Modular Docker Compose for Homelab

**Akiba** provides a modular, secure, and extensible Docker Compose environment for self-hosting a wide range of services. It is designed for homelab users who want sane defaults, strong security, and easy extensibility—without vendor lock-in or cloud dependencies.

## Key Features
- **Modular architecture:** Each service is isolated in its own folder under `compose/` with dedicated configs and compose files.
- **Security first:** SSL termination via HAProxy, authentication with Authelia, and threat protection with Crowdsec.
- **Secrets management:** All secrets and environment variables are managed and injected using [Infisical](https://infisical.com/).
- **Easy data management:** Persistent data is mapped to `${DATA_DIR}`; large user files (media, photos, etc.) use `${MEDIA_DIR}`.
- **Simple workflows:** Use the provided Makefile for common operations like starting, stopping, and managing the stack.
- **Extensible:** Add new services by creating a new folder in `compose/` and updating the root compose file.

## Usage Pattern

1. Configure secrets and environment variables in Infisical.
2. Use the Makefile for common workflows:
   ```sh
   make up       # Start the stack with secrets injected
   make down     # Stop and remove containers
   make pull     # Pull latest images
   make restart  # Restart all services
   make config   # Show the full resolved compose config
   make clean    # Prune unused Docker resources
   ```
3. Access services via Traefik (reverse proxy) with authentication and security enforced.
4. Add or update services by editing the relevant `compose/` subfolder and root compose file.

## Included Services

### Base

- Authelia (auth)
- Traefik (reverse proxy)
- Crowdsec (security)
- Cetusguard (docker socket proxy)
- Portainer
- Homepage
- Dozzle

### Additional

- Paperless-ngx
- Nextcloud
- Jellyfin
- Immich
- NocoDB
- Vaultwarden
- Uptime Kuma

and more

> **More detailed documentation and service-specific guides are available in the [Wiki](https://github.com/EsOsO/akiba/wiki) and the `doc/` folder.**

---

> **Disclaimer:** Some content in this repository, including documentation and configuration, may be AI generated or AI assisted.
