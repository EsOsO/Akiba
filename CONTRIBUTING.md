# Contributing to Akiba

Thank you for your interest in contributing to Akiba! This project aims to provide a modular, secure, and extensible Docker Compose environment for homelab users. Your contributions help make it better for everyone.

## How to Contribute

### 1. Issues & Feature Requests
- Search existing issues before opening a new one.
- Provide clear, descriptive titles and as much context as possible.
- For feature requests, explain the use case and benefits.

### 2. Pull Requests
- Fork the repository and create a new branch for your change.
- Follow the existing directory and compose file structure.
- Use environment variables for secrets and paths (do not hardcode sensitive values).
- Reference secrets via Infisical-managed environment variables.
- For new services, add a subfolder in `compose/` with a `compose.yaml` and any needed config files.
- Update the root `compose.yaml` or `compose.prod.yaml` if your service should be included by default.
- Add or update documentation in the `doc/` folder or the Wiki as appropriate.
- Use [conventional commits](https://www.conventionalcommits.org/) for commit messages (e.g., `feat: add new service`, `fix: correct volume path`).
- Run `make config` to validate your compose files before submitting.

### 3. Code Review & Merging
- All PRs are reviewed for security, maintainability, and adherence to project conventions.
- Automated checks (validation, changelog, etc.) must pass before merging.

## Best Practices
- Keep user data and configuration separate (use `${DATA_DIR}` and `${MEDIA_DIR}` as appropriate).
- Prefer modular, DRY patterns (use `extends` in compose files where possible).
- Document any new service or workflow.
- Test your changes locally before submitting.

## Community
- Be respectful and constructive in all communications.
- Suggestions and feedback are always welcome!

---
For more details, see the [Wiki](https://github.com/EsOsO/akiba/wiki) and other docs in the `doc/` folder.
