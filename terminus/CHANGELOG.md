# Changelog

## 0.1.0

- Initial Home Assistant app packaging for Terminus `0.60.0`.
- Runs Terminus web, Sidekiq, PostgreSQL 18, and Valkey in one app container.
- Persists database, key-value data, uploads, and generated secrets under `/data`.
- Documents external Cloudflare Tunnel exposure.
