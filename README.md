# PT Mitra Media Data — ISP / FTTH Management Platform

Production-oriented ISP/FTTH Billing + OSS/BSS + Network Management platform.

## Stack

```text
React + TypeScript
shadcn/ui
Tailwind CSS
Go + Fiber
PostgreSQL
pgx + sqlc
Redis
FreeRADIUS 3.2.x
MikroTik RouterOS API
ZTE C300/C320
snmp-olt-zte v3.2.0
Prometheus
Grafana
Docker
```

## Core Features

- Customer
- Billing
- Payment Gateway
- Subscription
- Static
- DHCP
- PPPoE
- Hotspot
- FreeRADIUS
- MikroTik
- ZTE OLT
- IPAM
- OLT/PON/ODC/ODP/ONU topology
- FieldOps
- Technician Schedule
- NOC
- Ticketing
- Monitoring
- Mitra
- Reports
- Realtime
- Multi-tenant
- RBAC

## Important

Laravel is NOT used.

FreeRADIUS remains standalone.

ZTE integration must use:

```text
Cepat-Kilat-Teknologi/snmp-olt-zte v3.2.0
```

See `MASTER_PROMPT.md` for the complete implementation specification.

## AI Agent

Recommended execution:

```text
Read MASTER_PROMPT.md
Read ARCHITECTURE.md
Read DATABASE.md
Read DESIGN.md
Read API.md
Read TASK.md
Then implement tasks by dependency order.
```
