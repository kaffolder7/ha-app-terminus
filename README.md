# Home Assistant Terminus Apps

This repository packages [Terminus](https://github.com/usetrmnl/terminus) as a Home Assistant app so TRMNL devices can use a local BYOS server.

## Apps

### Terminus

Runs Terminus `0.60.0` with its required PostgreSQL and Valkey services inside one Home Assistant app container. The app exposes only the Terminus web/API port and keeps all persistent state in Home Assistant app storage.

See [Terminus app documentation](terminus/DOCS.md) for installation, TRMNL device setup, backups, and optional Cloudflare Tunnel exposure.
