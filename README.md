# Campfire keepalive

Keeps the Virtual Campfire's Treeline Relay awake and checks that it is healthy. It uses the public status endpoint (`https://campfire-treeline.pplx.app/port/8097/api/status`) and contains no secrets.

## Primary: external monitor (UptimeRobot)

GitHub runs scheduled workflows on a best-effort basis and has skipped most five-minute runs, so the five-minute ping comes from an external monitor:

| Setting | Value |
|---|---|
| Service | UptimeRobot (Free plan), in Rory's UptimeRobot dashboard → Monitoring |
| Monitor name | `campfire relay status (keepalive)` |
| Type | Keyword |
| URL | `GET https://campfire-treeline.pplx.app/port/8097/api/status` |
| Keyword | `"paused": false`. The monitor alerts if the keyword is missing. |
| Interval / timeout | 300 s / 30 s |
| Alerts | Email to the owner when the keyword is missing or the response isn't 2xx/3xx |

Settings live in the UptimeRobot dashboard, not in this repo. If you change them there, update this table.

## Backup: GitHub workflow

`.github/workflows/ping.yml` pings the same endpoint on a five-minute cron. GitHub may delay or drop these runs. Once a day the workflow updates `HEARTBEAT`, so GitHub keeps the schedule enabled.
