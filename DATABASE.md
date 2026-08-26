# DATABASE.md

## Database

PostgreSQL.

Use:

```text
pgx
sqlc
migrations
```

## Rules

- Every tenant-owned table has tenant_id.
- Use foreign keys.
- Add indexes for common lookup fields.
- Use unique constraints where required.
- Use timestamps.
- Audit important state transitions.
- Avoid N+1.
- Paginate large datasets.

## Critical indexes

```text
tenant_id
customer_id
subscription_id
username
acctsessionid
nasipaddress
starttime
stoptime
ip_address
serial_number
```

## RADIUS

Use standard FreeRADIUS tables:

```text
radcheck
radreply
radgroupcheck
radgroupreply
radusergroup
radacct
nas
```

Application tables:

```text
radius_accounts
radius_profiles
radius_nas
radius_servers
radius_attribute_mappings
radius_nas_capabilities
radius_coa_requests
radius_disconnect_requests
radius_sync_logs
radius_audit_logs
```

## Topology

Use:

```text
odcs
odps
topology_nodes
topology_links
topology_dependencies
```

Dependency:

```text
OLT → PON → ODC → ODP → ONU → Customer
```

## IPAM

Use:

```text
ip_pools
subnets
ip_allocations
ip_reservations
```

Go IPAM is the source of truth.
