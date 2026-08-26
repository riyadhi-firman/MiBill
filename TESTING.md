# TESTING.md

## Unit

Test:

```text
services
repositories
domain state transitions
payment adapters
RADIUS builders
network adapters
workers
```

## Integration

Test:

```text
PostgreSQL
Redis
FreeRADIUS
MikroTik
ZTE
```

## E2E

Test:

```text
customer
service
subscription
invoice
payment
suspension
reactivation
PPPoE
Hotspot
RADIUS session
CoA
disconnect
OLT discovery
ONU mapping
topology
work order
ticket
```

## Security

Test:

```text
tenant isolation
RBAC
authentication
authorization
secret handling
```

## Performance

Test:

```text
concurrent authentication
accounting load
dashboard queries
session queries
network polling
WebSocket events
```

## Completion

A feature is not DONE until tests and verification pass.
