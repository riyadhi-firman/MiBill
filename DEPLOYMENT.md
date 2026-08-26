# DEPLOYMENT.md

## Containers

```text
frontend
api
worker
scheduler
postgres
redis
freeradius
prometheus
grafana
nginx
```

## Production

Use separate network segments where practical.

Example:

```text
Internet
 ↓
Nginx
 ↓
Frontend/API
 ↓
Private network
 ├── PostgreSQL
 ├── Redis
 ├── FreeRADIUS
 ├── Prometheus
 └── Grafana
```

## RADIUS HA

```text
MikroTik
 ├── FreeRADIUS-01
 └── FreeRADIUS-02
```

## Backup

Back up:

```text
PostgreSQL
FreeRADIUS configuration
application configuration
NAS registry
```

Never back up secrets into Git.

## Restore

Document tested restore procedure.

## Health

Verify:

```text
API
Database
Redis
RADIUS
MikroTik
OLT
Prometheus
Grafana
```
