# FreeRADIUS Implementation Prompt — PT Mitra Media Data

## Objective

Implement a production-grade **FreeRADIUS 3.2.x** subsystem for the PT Mitra Media Data ISP & FTTH Management Platform.

**FreeRADIUS MUST run as a standalone service.** Do not embed it in Laravel and do not rewrite RADIUS in Go.

### Architecture

```text
React + shadcn/ui
        |
     Laravel
      OSS/BSS
        |
   RadiusService
        |
 PostgreSQL + Redis
        |
 FreeRADIUS 3.2.x
        |
   +----+----+
   |         |
MikroTik  MikroTik
 PPPoE     Hotspot
```

## Responsibilities

### Laravel
- Customer
- Subscription
- Package
- Billing
- Invoice
- Payment
- Service status
- Suspension/reactivation
- RADIUS management UI
- RADIUS provisioning orchestration
- Audit

### FreeRADIUS
- Authentication
- Authorization
- Accounting
- Session handling
- RADIUS policy
- NAS communication
- CoA / Disconnect where supported

### Go
- Network engine
- ZTE
- MikroTik automation
- SNMP
- ICMP
- Polling

**Do not build a custom RADIUS server in Go.**

---

# 1. Version

Use the FreeRADIUS **3.2.x stable branch**.

Recommended target:

```text
FreeRADIUS 3.2.10
```

Verify and document the exact installed version before production.

Do not silently upgrade major versions.

---

# 2. Database

Use PostgreSQL with the FreeRADIUS SQL module.

Standard tables:

```text
radcheck
radreply
radgroupcheck
radgroupreply
radusergroup
radacct
nas
```

Application-owned tables:

```text
radius_accounts
radius_profiles
radius_nas
radius_servers
radius_sync_logs
radius_audit_logs
radius_events
```

Do not unnecessarily modify FreeRADIUS core tables.

---

# 3. Radius Account

Create `radius_accounts`:

```text
id
tenant_id
customer_id
subscription_id
username
authentication_type
profile_id
service_type
status
simultaneous_use
password_reference
created_at
updated_at
```

Service types:

```text
PPPOE
HOTSPOT
```

Statuses:

```text
ACTIVE
SUSPENDED
DISABLED
EXPIRED
PENDING
```

Never log plaintext passwords.

---

# 4. Radius Profile

Create `radius_profiles`:

```text
id
tenant_id
name
description
service_type
download_speed
upload_speed
rate_limit
session_timeout
idle_timeout
simultaneous_use
ipv4_pool
ipv6_pool
dns_servers
mikrotik_profile
status
created_at
updated_at
```

Centralize MikroTik attribute generation in a policy/attribute builder.

---

# 5. Laravel Service Layer

Create:

```php
interface RadiusServiceInterface
{
    provisionUser(...);
    updateUser(...);
    suspendUser(...);
    activateUser(...);
    disableUser(...);
    deleteUser(...);
    assignProfile(...);
    disconnectSession(...);
    coa(...);
    getSessions(...);
    getAccounting(...);
    getHealth(...);
}
```

Implement:

```text
RadiusService
```

Do not scatter direct RADIUS-table SQL across controllers.

Laravel remains the business source of truth.

---

# 6. PPPoE

Support MikroTik PPPoE:

```text
Customer
  |
ONT / OLT
  |
MikroTik
  |
RADIUS Access-Request
  |
FreeRADIUS
  |
Authentication + Authorization
  |
Access-Accept / Access-Reject
  |
MikroTik
  |
Internet
```

Support applicable:

- PAP
- CHAP
- MS-CHAP/MS-CHAPv2

Do not store plaintext credentials unnecessarily.

---

# 7. Hotspot

Support MikroTik Hotspot:

```text
Client
  |
MikroTik Hotspot
  |
FreeRADIUS
  |
Authentication
  |
Authorization
  |
Access-Accept
  |
Internet
```

Hotspot accounts must use the same customer/subscription model.

---

# 8. Authorization

Evaluate:

```text
Tenant
Customer
Subscription
Service
Status
Profile
IP allocation
Session policy
```

Rules:

```text
ACTIVE    -> Access-Accept
SUSPENDED -> Access-Reject
DISABLED  -> Access-Reject
EXPIRED   -> Access-Reject
PENDING   -> Access-Reject
```

Grace-period rules belong to Laravel.

Do not bury billing business logic inside complex FreeRADIUS SQL.

---

# 9. Billing Integration

Expected lifecycle:

```text
Invoice PAID
    |
Subscription ACTIVE
    |
RADIUS ACTIVE
    |
Customer Login Allowed
```

Overdue:

```text
Invoice OVERDUE
    |
Grace Period
    |
Still ACTIVE
```

After grace period:

```text
Subscription SUSPENDED
    |
RADIUS authorization blocked
    |
Optional Disconnect / CoA
```

Payment received:

```text
Payment
   |
Invoice PAID
   |
Subscription ACTIVE
   |
RADIUS ACTIVE
   |
Optional CoA / Reconnect
```

Audit every change.

---

# 10. Automatic Suspension

Create Laravel scheduled job:

```text
radius:sync-status
```

It must:

1. Find subscriptions requiring suspension.
2. Update subscription.
3. Update RADIUS authorization.
4. Disconnect active sessions if enabled.
5. Record audit.
6. Notify customer if configured.

Business state must remain controlled by Laravel.

---

# 11. Accounting

Enable:

```text
Accounting-Start
Accounting-Interim-Update
Accounting-Stop
```

Track:

```text
username
customer
subscription
NAS
NAS IP
NAS port
session ID
start time
stop time
session time
input octets
output octets
framed IP
terminate cause
```

Make interim interval configurable. A reasonable initial value is 5 minutes.

---

# 12. Active Sessions

Create:

```text
/radius/sessions
```

KPIs:

```text
Online Sessions
Sessions Today
Authentication Success
Authentication Failed
Upload
Download
```

Table:

```text
Username
Customer
NAS
IP
Start
Duration
Upload
Download
Status
Actions
```

Actions:

```text
View
Disconnect
Customer
Subscription
```

Use server-side pagination.

---

# 13. Authentication Logs

Create:

```text
/radius/logs
```

Show:

```text
Timestamp
Username
NAS
Source IP
Service
Result
Reason
Latency
```

Results:

```text
ACCEPT
REJECT
ERROR
```

Never display passwords or secrets.

---

# 14. NAS Management

Create `radius_nas`:

```text
id
tenant_id
name
shortname
ip_address
secret_encrypted
type
vendor
status
description
created_at
updated_at
```

Support:

- MikroTik
- BNG
- Other RADIUS clients

Actions:

```text
Add
Edit
Disable
Test
Rotate Secret
```

Encrypt secrets at rest and never reveal the complete secret after creation.

---

# 15. MikroTik Attributes

Support applicable attributes:

```text
Mikrotik-Rate-Limit
Mikrotik-Group
Mikrotik-Address-List
Mikrotik-Delegated-IPv6-Pool
Framed-IP-Address
Framed-IP-Netmask
Framed-Pool
Session-Timeout
Idle-Timeout
Simultaneous-Use
```

Do not hard-code attributes in controllers.

Use a centralized policy/attribute builder.

---

# 16. IPAM Integration

Laravel IPAM remains the source of truth:

```text
Subscription
    |
IPAM
    |
IP Allocation
    |
RadiusService
    |
FreeRADIUS
    |
Framed-IP-Address / Framed-Pool
    |
MikroTik
```

Support:

- Static IP
- Dynamic Pool
- IPv4
- IPv6

Do not create a competing IP allocation engine in FreeRADIUS.

---

# 17. Rate Limit

Example:

```text
Internet 100 Mbps
```

May generate:

```text
Mikrotik-Rate-Limit
```

Conceptual:

```text
100M/100M
```

The exact attribute format must follow the deployed MikroTik RADIUS dictionary.

Centralize rate-limit generation.

---

# 18. Simultaneous Use

Support:

```text
1
2
Unlimited
```

Use `Simultaneous-Use`.

Only enforce it when accounting state is sufficiently reliable.

---

# 19. CoA / Disconnect

Support where the NAS allows it:

```text
Change of Authorization
Disconnect-Request
```

Use for:

- Suspension
- Reactivation
- Package change
- Rate-limit change
- IP change
- Forced reconnect

Flow:

```text
Laravel
   |
RadiusService
   |
CoA / Disconnect
   |
MikroTik
   |
Active Session
```

Optional port:

```text
3799/udp
```

Only expose it to authorized NAS/network sources.

---

# 20. Package Change

Flow:

```text
Old Package
   |
New Package
   |
Subscription Updated
   |
RADIUS Profile Updated
   |
Optional CoA
   |
MikroTik Applies New Policy
```

Audit:

```text
Customer
Old Package
New Package
Operator
Timestamp
Reason
```

---

# 21. Multi-Tenant

Every application-owned RADIUS resource must include:

```text
tenant_id
```

Apply isolation to:

```text
Users
Profiles
NAS
Sessions
Accounting
Logs
Policies
```

Tenant A must never access Tenant B data.

---

# 22. High Availability

Production target:

```text
                  MikroTik
                 /                        v          v
        FreeRADIUS-01   FreeRADIUS-02
                \          /
                 \        /
                  PostgreSQL
```

Configure NAS with both RADIUS servers.

Monitor:

```text
RADIUS-01
RADIUS-02
Latency
Auth/s
Reject/s
Error/s
Accounting/s
```

---

# 23. Health

Validate configuration:

```bash
freeradius -XC
```

Service:

```bash
systemctl status freeradius
```

Ports:

```text
1812/udp
1813/udp
```

Optional:

```text
3799/udp
```

Never expose RADIUS ports to the public Internet unnecessarily.

---

# 24. Performance

Design for:

```text
10,000+
50,000+
100,000+
```

subscriber accounts.

Avoid:

- N+1 queries
- full-table scans
- unbounded accounting queries
- blocking network calls
- excessive database writes

Use:

- PostgreSQL indexes
- prepared statements
- connection pooling
- pagination
- aggregated accounting queries
- controlled caching

---

# 25. Monitoring

Integrate with Prometheus/Grafana.

Metrics:

```text
authentication_requests
authentication_success
authentication_rejects
authentication_errors
accounting_requests
active_sessions
session_duration
nas_availability
radius_response_latency
postgresql_latency
```

Alerts:

```text
RADIUS DOWN
High Authentication Failure
High Reject Rate
Database Unavailable
NAS Unavailable
High Latency
Accounting Failure
```

Prevent alert storms.

---

# 26. Security

Implement:

- encrypted NAS secrets
- least-privilege database user
- firewall
- tenant isolation
- audit logging
- no secret logging
- secure configuration
- restricted RADIUS ports
- secure CoA
- password protection
- configuration validation

Never log:

```text
Password
RADIUS Secret
API Token
DB Password
SSH Credential
```

---

# 27. UI

Use the existing PT Mitra Media Data shadcn/ui design system.

Do NOT create a separate RADIUS theme.

Pages:

```text
RADIUS
├── Dashboard
├── Users
├── Profiles
├── Sessions
├── Accounting
├── NAS
├── Logs
├── Health
└── Settings
```

Use shared:

- PageHeader
- MetricCard
- StatusBadge
- DataTable
- FilterToolbar
- DetailSheet
- Dialog
- Card
- Tabs
- Command
- Recharts

---

# 28. RADIUS Dashboard

Header:

```text
RADIUS
Authentication & Accounting
```

KPIs:

```text
Active Sessions
Auth Success
Auth Failed
NAS Online
Traffic
Average Session Duration
```

Charts:

```text
Authentication Trend
Active Sessions
Traffic
Failure Rate
```

Tables:

```text
Recent Authentication
Active Sessions
NAS Health
```

---

# 29. Customer 360

Customer detail must show:

```text
Billing Status
Subscription Status
RADIUS Status
Current Session
IP
NAS
Profile
Package
Usage
```

Example:

```text
Customer:
Ahmad Fauzi

Billing:
PAID

Subscription:
ACTIVE

Service:
PPPoE

RADIUS:
ONLINE

Profile:
100 Mbps

IP:
103.xxx.xxx.xxx

NAS:
MikroTik-PEJATEN-01

Session:
2h 31m
```

---

# 30. Realtime

Architecture:

```text
MikroTik
   |
RADIUS
   |
Accounting / Events
   |
Laravel
   |
Redis
   |
Laravel Reverb
   |
React
```

Realtime updates:

- Authentication
- Session start
- Session stop
- Online status
- Payment status
- Subscription status
- Suspension
- Reactivation
- NAS health

Show:

```text
● LIVE
```

---

# 31. Documentation

Create:

```text
docs/radius/
├── README.md
├── ARCHITECTURE.md
├── INSTALLATION.md
├── CONFIGURATION.md
├── MIKROTIK.md
├── PPPOE.md
├── HOTSPOT.md
├── ACCOUNTING.md
├── COA.md
├── HA.md
├── SECURITY.md
└── TROUBLESHOOTING.md
```

Document installation, configuration, PostgreSQL, MikroTik, PPPoE,
Hotspot, accounting, CoA, security, HA, backup, restore and
troubleshooting.

---

# 32. TASK.MD

Create:

```text
RADIUS-001 Install FreeRADIUS
RADIUS-002 Configure PostgreSQL
RADIUS-003 Configure SQL module
RADIUS-004 Configure NAS
RADIUS-005 Authentication
RADIUS-006 Authorization
RADIUS-007 PPPoE
RADIUS-008 Hotspot
RADIUS-009 Accounting
RADIUS-010 Profiles
RADIUS-011 Subscription status
RADIUS-012 Automatic suspension
RADIUS-013 Reactivation
RADIUS-014 Sessions
RADIUS-015 CoA
RADIUS-016 Disconnect
RADIUS-017 NAS management
RADIUS-018 Dashboard
RADIUS-019 Logs
RADIUS-020 Monitoring
RADIUS-021 HA
RADIUS-022 Security
RADIUS-023 Tests
RADIUS-024 Documentation
RADIUS-025 Production deployment
```

Each task must contain:

```text
ID
Priority
Description
Dependencies
Implementation
Acceptance Criteria
Status
```

---

# 33. Testing

Test:

### Authentication
- valid user
- invalid password
- unknown user
- suspended user
- disabled user
- expired subscription

### Authorization
- package
- rate limit
- IP
- session timeout
- simultaneous use

### Accounting
- start
- interim
- stop

### Billing
- paid
- overdue
- grace period
- suspended
- reactivated

### Security
- tenant isolation
- NAS secret
- unauthorized request

### CoA
- package change
- suspension
- reactivation
- disconnect

Lab test:

```bash
freeradius -XC
radtest USERNAME PASSWORD 127.0.0.1 0 testing123
```

Never commit real credentials.

---

# 34. Acceptance Criteria

Complete only when:

- [ ] FreeRADIUS 3.2.x installed
- [ ] Exact installed version documented
- [ ] PostgreSQL integration works
- [ ] SQL module works
- [ ] MikroTik NAS works
- [ ] PPPoE authentication works
- [ ] Hotspot authentication works
- [ ] Accounting works
- [ ] Active sessions work
- [ ] Profiles work
- [ ] Rate limit works
- [ ] Static IP works
- [ ] Dynamic pool works
- [ ] Subscription status controls authorization
- [ ] Automatic suspension works
- [ ] Automatic reactivation works
- [ ] CoA works where supported
- [ ] Disconnect works where supported
- [ ] Multi-tenant isolation works
- [ ] NAS management works
- [ ] RADIUS dashboard works
- [ ] RADIUS logs work
- [ ] Health monitoring works
- [ ] Prometheus metrics work
- [ ] HA is documented
- [ ] Security controls are implemented
- [ ] Automated tests pass
- [ ] Documentation is complete
- [ ] Production deployment is documented

---

# 35. Final Architecture Rule

```text
Laravel
=
Business / OSS / BSS

FreeRADIUS
=
Authentication / Authorization / Accounting

Go
=
Network Engine

PostgreSQL
=
Data

Redis
=
Cache / Queue / Realtime

React + shadcn/ui
=
User Interface
```

Final relationship:

```text
                         React
                           |
                           v
                       Laravel
                    OSS / Billing
                           |
                    RadiusService
                           |
              +------------+------------+
              |                         |
              v                         v
         PostgreSQL                   Redis
              |
              v
       FreeRADIUS 3.2.x
              |
       +------+------+
       |             |
       v             v
    MikroTik      MikroTik
     PPPoE        Hotspot
       |
       v
    Customer
```

The implementation must keep business logic in Laravel, RADIUS
authentication/accounting in FreeRADIUS, and network automation in Go.

END OF FREERADIUS IMPLEMENTATION PROMPT
