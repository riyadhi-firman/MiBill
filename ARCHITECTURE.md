# ARCHITECTURE.md — PT MITRA MEDIA DATA

## Backend

```text
Go
Fiber
REST
WebSocket
Workers
Scheduler
```

## Data

```text
PostgreSQL
pgx
sqlc
Redis
```

## Network

```text
FreeRADIUS
MikroTik RouterOS
ZTE C300/C320
SNMP
ICMP
```

## OLT

```text
snmp-olt-zte v3.2.0
```

## Frontend

```text
React
TypeScript
shadcn/ui
Tailwind
TanStack Query
TanStack Table
React Hook Form
Zod
Recharts
```

## Domain Flow

```text
Customer
 ↓
Service
 ↓
Subscription
 ↓
Billing
 ↓
RADIUS / MikroTik
 ↓
Network
```

## FTTH Flow

```text
OLT
 ↓
PON
 ↓
ODC
 ↓
ODP
 ↓
ONU
 ↓
Customer
```

## Realtime

```text
Network Worker
 ↓
Domain Event
 ↓
Redis
 ↓
WebSocket
 ↓
React
```

## Principle

Start as modular monolith.

Extract services only when operational evidence justifies it.
