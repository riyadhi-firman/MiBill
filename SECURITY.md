# SECURITY.md

## Rules

- never log passwords
- never log RADIUS secrets
- never log database credentials
- never log API tokens
- encrypt sensitive secrets
- use RBAC
- enforce tenant isolation
- parameterized SQL
- validate input
- rate limit APIs
- least privilege
- secure cookies/tokens
- audit critical operations
- rotate secrets
- firewall RADIUS ports
- restrict CoA/Disconnect
- never expose internal infrastructure unnecessarily

## RADIUS

Allow 1812/1813 only from authorized NAS sources.

Allow 3799 only from trusted sources.

## Production

Use:

```text
TLS
Secret management
Firewall
Backups
Audit
Monitoring
```
