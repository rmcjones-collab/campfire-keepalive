# Campfire keepalive

Pings the public status endpoint of the Virtual Campfire's Treeline Relay (`https://campfire-treeline.pplx.app/port/8097/api/status`) every five minutes so the hosted relay never idles. Contains no secrets; the `HEARTBEAT` file is updated once a day by the workflow so GitHub keeps the schedule enabled.
