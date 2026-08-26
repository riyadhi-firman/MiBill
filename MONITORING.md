# MONITORING.md

## Sources

```text
SNMP
ICMP
MikroTik API
ZTE integration
FreeRADIUS health
PostgreSQL
Redis
Go API
Workers
```

## Metrics

```text
http_requests_total
http_request_duration
worker_jobs_total
worker_job_failures
radius_auth_requests_total
radius_auth_accept_total
radius_auth_reject_total
radius_active_sessions
radius_coa_success
radius_coa_failure
mikrotik_health
olt_health
onu_online
onu_offline
```

## Alerts

```text
RADIUS Down
Both RADIUS Down
OLT Down
MikroTik Down
High Auth Reject
High Latency
Database Down
Redis Down
Worker Failure
CoA Failure
```

Avoid alert storms.
