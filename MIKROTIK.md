# MIKROTIK.md

## Integration

Use RouterOS API through a Go adapter.

## Modules

```text
Devices
BNG
PPPoE
Hotspot
DHCP
IP Pools
Interfaces
Queues
Sessions
Health
```

## Requirements

- connection timeout
- command timeout
- retry
- backoff
- idempotency
- audit
- health state

## RADIUS

MikroTik acts as NAS for FreeRADIUS.

Authentication:

```text
1812/udp
```

Accounting:

```text
1813/udp
```

CoA/Disconnect:

```text
3799/udp
```

Use only from trusted network sources.
