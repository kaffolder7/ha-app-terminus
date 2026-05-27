# Home Assistant App: Terminus

This repository packages [Terminus](https://github.com/usetrmnl/terminus) as a Home Assistant app so TRMNL devices can use a local BYOS server.

![Supports aarch64 Architecture][aarch64-shield] ![Supports amd64 Architecture][amd64-shield] ![Build Status][build-shield]

Runs Terminus `0.60.0` with its required PostgreSQL and Valkey services inside one Home Assistant app container. The app exposes only the Terminus web/API port and keeps all persistent state in Home Assistant app storage.

See [Terminus app documentation](terminus/DOCS.md) for installation, TRMNL device setup, backups, and optional Cloudflare Tunnel exposure.

## Installation

1. In Home Assistant, go to **Settings → Apps → App store**.
2. Open the App store menu (⋮) → **Repositories**.
3. Add this repository URL:

   `https://github.com/kaffolder7/ha-app-terminus`

Or add it directly:

[![Open your Home Assistant instance and show the app repository dialog pre-filled.][my-ha-badge]][my-ha-link]

4. Refresh the App Store so the new repository is loaded.
5. Find **TRMNL Terminus** and click **Install**.
6. Start the app.

---

[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[build-shield]: https://img.shields.io/github/actions/workflow/status/kaffolder7/ha-app-terminus/builder.yaml
[my-ha-badge]: https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg
[my-ha-link]: https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fkaffolder7%2Fha-app-terminus
