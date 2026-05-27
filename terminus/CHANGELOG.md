# Changelog

## 0.1.3

- Use PostgreSQL's versioned binaries directly for readiness checks and database setup so the app does not rely on Debian `pg_wrapper` symlinks under confined Home Assistant startup.

## 0.1.2

- Allow service users to traverse `/data` so PostgreSQL, Valkey, and Terminus can reach their owned persistent directories without exposing root directory listings.

## 0.1.1

- Add a custom AppArmor profile and explicit protected app defaults.
- Enable Docker init, tmpfs-backed `/tmp`, and application startup ordering.
- Pin the upstream Terminus base image by digest.
- Harden option validation, secret permissions, and Valkey readiness checks.
- Make CI rebuild on AppArmor profile changes and explicitly keep Cosign signing enabled.

## 0.1.0

- Initial Home Assistant app packaging for Terminus `0.60.0`.
- Runs Terminus web, Sidekiq, PostgreSQL 18, and Valkey in one app container.
- Persists database, key-value data, uploads, and generated secrets under `/data`.
- Documents external Cloudflare Tunnel exposure.
