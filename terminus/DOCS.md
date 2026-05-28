# TRMNL Terminus App

This app runs [Terminus](https://github.com/usetrmnl/terminus), the self-hosted TRMNL BYOS server, inside Home Assistant.

## Configuration

| Option | Description |
| --- | --- |
| `api_uri` | Public URL that TRMNL devices use for this Terminus instance. For LAN-only use, set this to a reachable local URL such as `http://homeassistant.local:2300` or `http://192.168.1.10:2300`. For Cloudflare Tunnel use, set this to the public HTTPS hostname. |
| `log_level` | Minimum Terminus log severity to write. Defaults to `warning`; use `info` or `debug` when you need more detailed troubleshooting output. |
| `rack_attack_allowed_subnets` | Comma-separated subnets or IP addresses allowed through Terminus rate-limit protection. The default private network list works for typical LAN and local tunnel-origin traffic. |
| `certificate_urls` | Optional comma-separated custom CA certificate URLs. Use this only when Terminus needs to call HTTPS services signed by a private CA. |

The app generates `APP_SECRET`, PostgreSQL password, and Valkey password into `/data/secrets.env` on first start. They are intentionally not exposed as app options.

## Device Setup

1. Start the app.
2. Open the Web UI and finish Terminus setup.
3. In each TRMNL device captive Wi-Fi portal, set the custom host to the exact value configured in `api_uri`.

The device custom host and Terminus `api_uri` must match because Terminus uses that value when producing API URLs for devices.

## Storage And Backups

Persistent state is stored in Home Assistant app storage:

- PostgreSQL data: `/data/postgres`
- Valkey data: `/data/valkey`
- Terminus uploads: `/data/uploads`
- Generated secrets: `/data/secrets.env`

The app uses `backup: cold`, so stop the app before snapshotting its data. Restoring the app data restores Terminus accounts, devices, uploads, and generated credentials.

## Cloudflare Tunnel

Cloudflare Tunnel support is intentionally external to this app.

Recommended setup:

1. Run a separate `cloudflared` connector, such as a dedicated Home Assistant Cloudflare Tunnel app or another host on the same network.
2. Configure the tunnel public hostname to forward to `http://<HOME_ASSISTANT_LAN_IP>:2300`.
3. Set this app's `api_uri` to the public HTTPS URL, for example `https://terminus.example.com`.
4. Configure remote TRMNL devices with the same public HTTPS URL as their custom host.

Do not put an interactive Cloudflare Access login in front of TRMNL device API paths. TRMNL devices cannot complete a browser-based Access challenge. If you use Cloudflare Access for the web UI, leave the device API endpoints reachable by the devices.

## Ports

Only `2300/tcp` is exposed. PostgreSQL and Valkey listen only inside the app container.

## Updating

This app pins Terminus to `0.60.0` by image digest for reproducible builds. Future app releases should update the pinned upstream image tag and digest together, then smoke-test startup, migrations, `/up`, Web UI, and device API behavior against existing `/data`.
