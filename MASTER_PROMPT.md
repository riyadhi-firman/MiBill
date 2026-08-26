# PT MITRA MEDIA DATA
# FINAL MASTER IMPLEMENTATION PROMPT
## ISP / FTTH Billing + OSS/BSS + Network Management Platform

## 1. MISSION

Build a production-ready ISP/FTTH management platform for:

**PT Mitra Media Data**

The platform combines:

- Customer Management
- Billing
- Payment Gateway
- Subscription
- Static IP
- DHCP
- PPPoE
- Hotspot
- FreeRADIUS
- MikroTik
- ZTE OLT
- IPAM
- FTTH topology
- OLT → PON → ODC → ODP → ONU → Customer dependency mapping
- FieldOps
- Technician scheduling
- NOC
- Ticketing
- Monitoring
- Mitra/Reseller
- Reports
- Finance
- Notifications
- Realtime
- Multi-tenant
- RBAC
- Audit
- Production operations

This is an implementation specification for an AI coding agent.

Do not create a mock-only application.

---

# 2. NON-NEGOTIABLE ARCHITECTURE

## DO NOT USE LARAVEL

The application must use a Go-first architecture.

### Frontend

```text
React
TypeScript
shadcn/ui
Tailwind CSS
TanStack Query
TanStack Table
React Hook Form
Zod
Recharts
```

### Backend

```text
Go
Fiber
REST API
WebSocket
Go Worker
Go Scheduler
```

### Database

```text
PostgreSQL
pgx
sqlc
versioned migrations
```

### Cache / Queue

```text
Redis
```

### Network

```text
MikroTik RouterOS API
SNMP
ICMP
```

### RADIUS

```text
FreeRADIUS 3.2.x
```

### ZTE OLT

Use exactly:

```text
Cepat-Kilat-Teknologi/snmp-olt-zte
Release v3.2.0
```

Reference:

```text
https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte/releases/tag/v3.2.0
```

Do not replace it with an unrelated implementation.

### Monitoring

```text
Prometheus
Grafana
```

### Deployment

```text
Docker
Nginx / reverse proxy
CI/CD
```

---

# 3. ARCHITECTURE PRINCIPLE

Use a **modular monolith first**.

Do not create many microservices unless there is a proven need.

```text
Go Application
│
├── auth
├── tenant
├── customer
├── subscription
├── package
├── billing
├── payment
├── commission
├── radius
├── mikrotik
├── olt
├── ipam
├── topology
├── fieldops
├── technician
├── ticket
├── noc
├── monitoring
├── notification
├── reporting
├── audit
└── realtime
```

Use:

```text
Handler
  ↓
Service
  ↓
Repository
  ↓
PostgreSQL
```

Network integrations:

```text
Service
  ↓
Adapter
  ↓
MikroTik / ZTE / FreeRADIUS
```

Do not put business logic inside HTTP handlers.

---

# 4. TARGET ARCHITECTURE

```text
                         INTERNET
                            │
                            ▼
                  React + shadcn/ui
                            │
                       REST/WebSocket
                            │
                            ▼
                    ┌──────────────┐
                    │  Go + Fiber  │
                    └──────┬───────┘
                           │
            ┌──────────────┼───────────────┐
            ▼              ▼               ▼
       PostgreSQL        Redis          Workers
            │                              │
            │              ┌───────────────┼───────────────┐
            │              ▼               ▼               ▼
            │         FreeRADIUS       MikroTik           ZTE
            │              │               │               │
            │              ▼               ▼               ▼
            │           PPPoE           RouterOS      C300/C320
            │           Hotspot
            │
            └────────────── Business / OSS / BSS
```

---

# 5. REPOSITORY STRUCTURE

Create:

```text
cmd/
  api/
  worker/
  scheduler/

internal/
  auth/
  tenant/
  customer/
  subscription/
  package/
  billing/
  payment/
  commission/
  radius/
  mikrotik/
  olt/
  ipam/
  topology/
  fieldops/
  technician/
  ticket/
  noc/
  monitoring/
  notification/
  reporting/
  audit/
  realtime/

pkg/
  logger/
  response/
  validator/
  crypto/
  pagination/
  events/
```

Frontend:

```text
src/
  app/
  components/
  features/
    dashboard/
    customers/
    billing/
    packages/
    services/
    radius/
    mikrotik/
    olt/
    topology/
    ipam/
    fieldops/
    noc/
    monitoring/
    mitra/
    reports/
    administration/
  hooks/
  lib/
  routes/
  types/
```

---

# 6. DATABASE MASTER DESIGN

Use PostgreSQL.

Use:

```text
pgx
sqlc
migrations
```

Core:

```text
tenants
users
roles
permissions
user_roles
role_permissions
audit_logs
```

Customer:

```text
customers
customer_contacts
customer_addresses
customer_notes
```

Products:

```text
products
packages
package_features
```

Services:

```text
services
subscriptions
subscription_events
```

Billing:

```text
invoices
invoice_items
payments
payment_transactions
payment_gateways
payment_webhooks
billing_cycles
```

Mitra:

```text
mitras
commission_rules
commission_ledgers
payouts
```

RADIUS:

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
radcheck
radreply
radgroupcheck
radgroupreply
radusergroup
radacct
nas
```

MikroTik:

```text
mikrotik_devices
mikrotik_interfaces
mikrotik_ip_pools
mikrotik_sessions
mikrotik_health
```

OLT:

```text
olts
olt_pons
onus
onu_profiles
olt_alarms
olt_optical_readings
```

IPAM:

```text
ip_pools
subnets
ip_allocations
ip_reservations
```

Topology:

```text
odcs
odps
topology_nodes
topology_links
topology_dependencies
```

FieldOps:

```text
technicians
technician_schedules
work_orders
work_order_items
work_order_events
```

NOC:

```text
tickets
ticket_comments
ticket_events
incidents
sla_policies
sla_events
```

Monitoring:

```text
monitoring_targets
monitoring_samples
alerts
alert_events
```

Notifications:

```text
notifications
notification_templates
notification_channels
```

Use foreign keys, indexes, unique constraints and appropriate retention.

Every tenant-owned table must have:

```text
tenant_id
```

---

# 7. AUTHENTICATION / RBAC

Implement:

- login
- logout
- refresh token/session
- password reset
- 2FA-ready architecture
- RBAC
- permission management
- tenant context
- audit

Roles:

```text
Super Admin
Administrator
Finance
Billing
NOC
Network Engineer
Technician
Mitra
Customer
Viewer
```

Granular permissions:

```text
customer.view
customer.create
customer.update
customer.suspend

billing.view
billing.invoice.create
billing.payment.verify

radius.view
radius.user.provision
radius.session.disconnect
radius.nas.manage

olt.view
olt.manage
onu.view
onu.manage

topology.view
topology.manage

fieldops.view
fieldops.manage
```

---

# 8. CUSTOMER MANAGEMENT

Customer fields:

```text
Customer ID
Name
Phone
Email
Address
Tenant
Mitra
Status
Created At
```

Statuses:

```text
LEAD
PENDING
ACTIVE
SUSPENDED
TERMINATED
```

Customer 360:

```text
Overview
Services
Subscriptions
Billing
RADIUS
IP
MikroTik
OLT/PON/ONU
Topology
Usage
Tickets
Work Orders
Invoices
Activity
```

---

# 9. INTERNET SERVICES

Support:

```text
STATIC
DHCP
PPPOE
HOTSPOT
```

Prepare:

```text
IPv4
IPv6
Dual Stack
```

Every service links:

```text
Customer
Subscription
Package
Network Profile
IP allocation
RADIUS account if applicable
NAS
OLT/ONU dependency if applicable
```

---

# 10. PACKAGES

Package fields:

```text
Name
Service Type
Download
Upload
Price
Billing Cycle
Burst
Priority
Session Timeout
Idle Timeout
Simultaneous Use
IPv4 Pool
IPv6 Pool
DNS
MikroTik Profile
RADIUS Profile
Status
```

Support packages from low speed to high speed.

Do not hard-code packages inside RADIUS.

---

# 11. SUBSCRIPTION LIFECYCLE

```text
PENDING
 ↓
ACTIVE
 ↓
GRACE_PERIOD
 ↓
SUSPENDED
 ↓
REACTIVATING
 ↓
ACTIVE
```

Or:

```text
TERMINATED
```

RADIUS/network suspension must be driven by business state.

Never suspend customers merely because a network component is temporarily
unavailable.

---

# 12. BILLING

Support:

- invoice
- invoice items
- recurring billing
- billing cycle
- due date
- overdue
- grace period
- suspension
- reactivation
- refund
- adjustment
- credit note
- finance reports

Invoice statuses:

```text
DRAFT
ISSUED
PENDING
PAID
PARTIALLY_PAID
OVERDUE
CANCELLED
REFUNDED
```

---

# 13. PAYMENT GATEWAY

Use an abstraction:

```go
type PaymentGateway interface {
    CreatePayment(...)
    VerifyPayment(...)
    HandleWebhook(...)
    RefundPayment(...)
}
```

Webhook:

```text
Gateway
 ↓
Go API
 ↓
Verify signature
 ↓
Verify transaction
 ↓
Payment
 ↓
Invoice
 ↓
Subscription
 ↓
RADIUS activation
 ↓
Optional CoA
 ↓
Notification
```

Webhook processing must be idempotent.

---

# 14. MITRA / RESELLER

Support:

```text
Mitra
Customers
Services
Commission Rules
Commission Ledger
Payouts
Reports
```

Dashboard:

```text
Customers
Active Services
Revenue
Commission
Pending Payment
Growth
```

---

# 15. FREERADIUS

FreeRADIUS MUST be standalone.

Target:

```text
FreeRADIUS 3.2.x
```

Recommended target:

```text
3.2.10
```

FreeRADIUS responsibilities:

```text
Authentication
Authorization
Accounting
RADIUS policy
NAS communication
CoA
Disconnect
```

Go responsibilities:

```text
Provisioning
Lifecycle management
RADIUS administration
Billing synchronization
Queue/retry
Business integration
```

Do not build a custom RADIUS server in Go.

---

# 16. RADIUS DATABASE

Standard:

```text
radcheck
radreply
radgroupcheck
radgroupreply
radusergroup
radacct
nas
```

Application:

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

Never log passwords or shared secrets.

---

# 17. RADIUS ACCOUNT

Fields:

```text
id
tenant_id
customer_id
subscription_id
username
authentication_type
service_type
profile_id
status
simultaneous_use
password_reference
last_auth_at
last_reject_at
created_at
updated_at
```

Service:

```text
PPPOE
HOTSPOT
```

Status:

```text
PENDING
ACTIVE
SUSPENDED
DISABLED
EXPIRED
TERMINATED
```

---

# 18. RADIUS PROFILE

Fields:

```text
name
service_type
download_speed
upload_speed
rate_limit
burst_limit
priority
session_timeout
idle_timeout
simultaneous_use
ipv4_pool
ipv6_pool
dns_servers
mikrotik_group
mikrotik_address_list
status
```

Create:

```text
RadiusPolicyBuilder
RadiusAttributeBuilder
RadiusService
RadiusSessionService
RadiusAccountingService
RadiusCoaService
```

---

# 19. PPPoE

Flow:

```text
Customer
 ↓
ONU
 ↓
OLT
 ↓
MikroTik
 ↓
FreeRADIUS
 ↓
Access-Accept/Reject
 ↓
Internet
```

Support applicable:

```text
PAP
CHAP
MS-CHAP
MS-CHAPv2
```

---

# 20. HOTSPOT

```text
Client
 ↓
MikroTik Hotspot
 ↓
FreeRADIUS
 ↓
Authentication
 ↓
Authorization
 ↓
Internet
```

---

# 21. RADIUS ATTRIBUTES

Support where applicable:

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

Use configurable attribute mappings.

---

# 22. IPAM

Go IPAM is the source of truth.

Support:

```text
IPv4
IPv6
Static
Dynamic Pool
DHCP
Dual Stack
```

Static:

```text
Framed-IP-Address
```

Dynamic:

```text
Framed-Pool
```

Never duplicate IP allocation logic in FreeRADIUS.

---

# 23. RADIUS ACCOUNTING

Enable:

```text
Accounting-Start
Accounting-Interim-Update
Accounting-Stop
```

Track:

```text
username
NAS
NAS IP
NAS port
acctsessionid
start
update
stop
session time
input octets
output octets
framed IP
terminate cause
service type
```

Default interim interval:

```text
5 minutes
```

Handle:
- missing stop
- NAS reboot
- duplicate start
- duplicate stop
- stale session
- packet loss

Create session reconciliation.

---

# 24. RADIUS SESSIONS

Dashboard:

```text
Active Sessions
Sessions Today
Auth Success
Auth Reject
Traffic
Average Duration
```

Actions:

```text
View
Disconnect
Customer
Subscription
```

---

# 25. BILLING → RADIUS AUTOMATION

Suspension:

```text
Invoice overdue
 ↓
Grace expired
 ↓
Subscription SUSPENDED
 ↓
Update RADIUS
 ↓
Optional Disconnect
```

Reactivation:

```text
Payment received
 ↓
Invoice PAID
 ↓
Subscription ACTIVE
 ↓
Update RADIUS
 ↓
Optional CoA
```

All operations:
- idempotent
- audited
- retried safely

---

# 26. CoA / DISCONNECT

Support:

```text
CoA
Disconnect-Request
```

Use for:

- speed changes
- package changes
- suspension
- reactivation
- policy changes
- manual disconnect

Track:

```text
request_id
NAS
username
attributes
result
response_code
latency
retry_count
```

Optional port:

```text
3799/udp
```

---

# 27. NAS

Support:

```text
MikroTik
BNG
Other RADIUS clients
```

Fields:

```text
name
shortname
ip_address
vendor
model
type
secret_encrypted
auth_port
acct_port
coa_port
status
description
```

Secrets:
- encrypted at rest
- never returned after creation
- never logged
- never committed
- rotation supported

---

# 28. MIKROTIK

Use RouterOS API.

Modules:

```text
Routers
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

Dashboard:

```text
Routers Online
PPPoE Sessions
Hotspot Users
Traffic
CPU
Memory
```

Use adapter interfaces and timeouts.

---

# 29. ZTE OLT

MUST use:

```text
Cepat-Kilat-Teknologi/snmp-olt-zte
v3.2.0
```

Supports intended capabilities such as:

```text
Multi-OLT
Per-tenant keys
Uplink auto-detect
C300
C320
```

Do not invent unsupported commands.

---

# 30. OLT FEATURES

```text
OLT Dashboard
OLT Devices
PON
ONU
ONU Profiles
VLAN
Optical Power
Alarms
Monitoring
```

Dashboard:

```text
OLT Online
PON Online
ONU Online
ONU Offline
LOS Alarms
Optical Power
```

ONU table:

```text
ONU ID
Serial
Customer
PON
Status
RX
TX
Temperature
Uptime
Actions
```

---

# 31. FTTH TOPOLOGY

Mandatory hierarchy:

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

Example:

```text
OLT-01
 ↓
PON 1/1/1
 ↓
ODC-PEJATEN-01
 ↓
ODP-PEJATEN-012
 ↓
ONU-ZTE-001
 ↓
Customer
```

Interactive topology:
- zoom
- pan
- search
- filter
- node detail
- dependency highlighting
- alarm
- status
- customer lookup

Selecting ONU must highlight the complete dependency chain.

---

# 32. FIELDOPS

Support:

```text
Work Orders
Installation
Maintenance
Troubleshooting
Technicians
Schedules
Calendar
Job Detail
```

Statuses:

```text
PENDING
ASSIGNED
EN_ROUTE
IN_PROGRESS
WAITING
COMPLETED
CANCELLED
```

Calendar:

```text
Day
Week
Month
```

Dashboard:

```text
Today's Jobs
Pending
In Progress
Completed
Overdue
Technicians Online
```

---

# 33. NOC / TICKETING

Support:

```text
Tickets
Incidents
Network Events
SLA
Escalation
```

Dashboard:

```text
Active Incidents
Critical Alerts
Network Availability
OLT Down
MikroTik Down
RADIUS Down
Open Tickets
SLA Breach
```

---

# 34. MONITORING

Sources:

```text
SNMP
ICMP
MikroTik API
ZTE integration
RADIUS health
```

Metrics via Prometheus.

Dashboards:

```text
Application
Billing
RADIUS
MikroTik
OLT
Network
Workers
```

---

# 35. REALTIME

Use:

```text
Go WebSocket
Redis events
```

Events:

```text
radius.authenticated
radius.rejected
radius.session.started
radius.session.updated
radius.session.stopped

olt.status.changed
onu.status.changed
onu.alarm
olt.alarm

mikrotik.status.changed
mikrotik.session.changed

subscription.suspended
subscription.reactivated

payment.received
invoice.overdue

technician.status.changed
ticket.updated
incident.created
incident.resolved
```

UI:

```text
● LIVE
```

Fallback:

```text
● REALTIME DISCONNECTED
```

---

# 36. NOTIFICATIONS

Channels:

```text
WhatsApp
Email
SMS
In-App
```

Events:

```text
Invoice Created
Payment Received
Invoice Overdue
Suspended
Reactivated
Technician Scheduled
Ticket Updated
Network Incident
Maintenance
```

Use background workers.

---

# 37. REPORTS

Reports:

```text
Customer
Billing
Payment
Traffic
RADIUS
OLT
Technician
Financial
Mitra
```

Support:

```text
Filters
Date Range
Compare
Export
Print
CSV
XLSX/PDF where required
```

Large reports must run asynchronously.

---

# 38. COMPLETE UI/UX

The provided UI reference image is the visual benchmark.

The entire platform must use one visual system:

```text
Dark
shadcn/ui
Tailwind
Premium Enterprise Billing
Dense but readable
Rounded cards
Subtle borders
Compact tables
Clean typography
Minimal shadows
Consistent spacing
Responsive
```

Brand:

```text
PT Mitra Media Data
```

Never use the old company name in the new UI.

---

# 39. GLOBAL APP SHELL

Every page:

```text
┌─────────────────────────────────────────────────────────────┐
│ Sidebar │ Search     Notifications  Theme  User             │
│         ├───────────────────────────────────────────────────┤
│         │ Breadcrumb                                        │
│         │ Page Title                   Actions / Filters    │
│         │                                                   │
│         │ KPI Cards                                         │
│         │ Charts / Main Content                             │
│         │ Tables                                             │
└─────────────────────────────────────────────────────────────┘
```

Desktop:
persistent sidebar.

Tablet:
collapsible sidebar.

Mobile:
drawer navigation.

---

# 40. SIDEBAR

```text
MAIN
  Dashboard
  Customers
  Billing
  Products & Packages
  Services

NETWORK
  RADIUS
  MikroTik
  OLT (ZTE)
  Network Topology
  IP Management

OPERATIONS
  FieldOps / Technician
  NOC / Tickets
  Monitoring
  Alerts

BUSINESS
  Mitra / Reseller
  Reports
  Finance

SYSTEM
  Administration
  Settings
```

---

# 41. TOPBAR

Include:

```text
Global Search
⌘K / Ctrl+K
Notifications
Realtime Indicator
Theme
Tenant Switcher
User Menu
```

---

# 42. SHARED UI COMPONENTS

Create:

```text
AppShell
Sidebar
Topbar
Breadcrumb
PageHeader
MetricCard
ChartCard
DataTable
FilterToolbar
SearchInput
StatusBadge
HealthBadge
RealtimeIndicator
EmptyState
ErrorState
LoadingSkeleton
ConfirmDialog
DetailSheet
EntityAvatar
ActivityTimeline
StatList
ProgressBar
NetworkStatus
```

All modules MUST reuse them.

---

# 43. MAIN DASHBOARD

KPIs:

```text
Active Customers
Online Services
Monthly Revenue
Overdue
PPPoE Sessions
ONU Online
Network Availability
Open Tickets
```

Charts:

```text
Revenue
Customer Growth
Network Sessions
Traffic
```

Panels:

```text
Recent Payments
Active Sessions
Network Health
Recent Tickets
OLT Alarms
Technician Jobs
```

---

# 44. BILLING UI

Pages:

```text
Dashboard
Invoices
Payments
Overdue
Payment Gateway
Recurring Billing
Finance Reports
```

KPI:

```text
Revenue
Paid
Unpaid
Overdue
MRR
Active Customers
```

---

# 45. CUSTOMER UI

Customer list:

```text
Customer ID
Name
Service
Package
IP
Billing
RADIUS
OLT/ONU
Status
Actions
```

Customer 360:

```text
Overview
Services
Billing
RADIUS
Network
Usage
Tickets
Invoices
Activity
```

---

# 46. RADIUS UI

```text
Dashboard
Users
Profiles
Sessions
Accounting
NAS
CoA / Disconnect
Authentication Logs
Health
Settings
```

KPIs:

```text
Active Sessions
Auth Success
Auth Reject
RADIUS Requests
NAS Online
Traffic
```

---

# 47. MIKROTIK UI

```text
Dashboard
Routers
BNG
PPPoE
Hotspot
DHCP
IP Pools
Interfaces
Queues
Health
```

---

# 48. OLT UI

```text
Dashboard
OLT Devices
PON
ONU
ONU Profiles
VLAN
Optical Power
Alarms
Monitoring
```

---

# 49. TOPOLOGY UI

Visualize:

```text
OLT → PON → ODC → ODP → ONU → Customer
```

Features:

```text
Zoom
Pan
Search
Filter
Dependency Highlight
Node Detail
Alarm
Status
Customer Lookup
```

---

# 50. IPAM UI

```text
Dashboard
IPv4 Pools
IPv6 Pools
Subnets
Allocations
Static IP
DHCP
Usage
```

Show:

```text
Total
Used
Available
Reserved
Utilization
```

---

# 51. FIELDOPS UI

```text
Dashboard
Work Orders
Installation
Maintenance
Troubleshooting
Technicians
Schedule
Calendar
Job Detail
```

---

# 52. NOC UI

```text
Active Incidents
Critical Alerts
Network Availability
OLT Down
MikroTik Down
RADIUS Down
Open Tickets
SLA Breach
```

---

# 53. MONITORING UI

```text
Network Overview
MikroTik
OLT
RADIUS
Bandwidth
Traffic
Availability
Alerts
```

Use live indicators and historical charts.

---

# 54. MITRA UI

```text
Dashboard
Customers
Services
Billing
Commission
Revenue
Reports
```

---

# 55. REPORTS / FINANCE UI

```text
Customer
Billing
Payment
Traffic
RADIUS
OLT
Technician
Financial
Mitra
```

Actions:

```text
Filter
Date Range
Compare
Export
Print
```

---

# 56. ADMINISTRATION UI

```text
Users
Roles
Permissions
Tenants
Audit Logs
API
Integrations
Payment Gateway
RADIUS
MikroTik
OLT
System Settings
```

---

# 57. DESIGN SYSTEM

Centralize tokens:

```text
background
foreground
card
card-foreground
muted
muted-foreground
border
primary
primary-foreground
success
warning
destructive
info
```

Shared status:

```text
ACTIVE = success
ONLINE = success
SUSPENDED = destructive
OFFLINE = destructive
WARNING = warning
PENDING = warning
INFO = info
```

Do not rely only on color for meaning.

---

# 58. LOADING / EMPTY / ERROR

Every page must have:

```text
LoadingSkeleton
EmptyState
ErrorState
Retry
```

Never expose raw stack traces to users.

---

# 59. FORMS

Use:

```text
shadcn/ui
React Hook Form
Zod
```

Sections:

```text
General
Service
Network
Billing
Advanced
```

Never expose:

```text
RADIUS shared secrets
database passwords
API tokens
SSH credentials
payment secrets
```

---

# 60. TABLES

Use:

```text
TanStack Table
shadcn/ui
```

Features:

```text
search
filter
sort
pagination
column visibility
bulk actions
row actions
```

---

# 61. RESPONSIVE / ACCESSIBILITY

Support:

```text
Desktop
Tablet
Mobile
```

Accessibility:

```text
Keyboard navigation
Focus states
Semantic HTML
ARIA
Accessible labels
Contrast
```

---

# 62. API STANDARD

Base:

```text
/api/v1
```

Examples:

```text
GET    /customers
POST   /customers
GET    /customers/:id
PATCH  /customers/:id

GET    /subscriptions
POST   /subscriptions

GET    /invoices
POST   /invoices

GET    /payments
POST   /payments/webhooks

GET    /radius/users
POST   /radius/users
PATCH  /radius/users/:id
POST   /radius/users/:id/suspend
POST   /radius/users/:id/activate
POST   /radius/users/:id/disconnect

GET    /radius/sessions
GET    /radius/nas
POST   /radius/nas

GET    /mikrotik/devices
GET    /mikrotik/sessions

GET    /olts
GET    /olts/:id/pons
GET    /onus

GET    /topology
GET    /topology/:id/dependencies

GET    /work-orders
POST   /work-orders

GET    /tickets
POST   /tickets
```

Response:

```json
{
  "data": {},
  "meta": {},
  "error": null
}
```

---

# 63. OBSERVABILITY

Structured logs:

```text
timestamp
request_id
tenant_id
customer_id
subscription_id
operation
result
latency
```

Prometheus:

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
payment_webhooks_total
```

---

# 64. SECURITY

Implement:

```text
RBAC
Tenant isolation
Validation
Parameterized SQL
Rate limiting
Secure authentication
Secret encryption
Audit logs
Secret rotation
Least privilege
Firewall restrictions
```

Never log credentials.

---

# 65. DEPLOYMENT

Docker services:

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

Provide:

```text
docker-compose.yml
.env.example
health checks
migrations
seeds
backup
restore
```

Never commit `.env`.

---

# 66. CI/CD

Pipeline:

```text
Lint
Test
Build
Security Scan
Migration Check
Docker Build
Deploy
Health Check
```

Go:

```bash
go test ./...
go vet ./...
```

Frontend:

```bash
pnpm test
pnpm build
```

---

# 67. TESTING

Unit:
- domain services
- repositories
- workers
- adapters

Integration:
- PostgreSQL
- Redis
- RADIUS
- MikroTik
- ZTE

E2E:
- customer
- subscription
- billing
- payment
- suspension
- reactivation
- PPPoE
- Hotspot
- session
- topology
- technician
- ticket

Security:
- tenant isolation
- RBAC
- secrets
- authentication
- authorization

Performance:
- concurrent authentication
- accounting load
- session queries
- dashboard queries
- network polling

---

# 68. TASK.MD

Create and maintain a detailed TASK.md.

Each task must contain:

```text
ID
Priority
Dependencies
Description
Files
Implementation
Testing
Acceptance Criteria
Status
```

Initial task groups:

```text
CORE
AUTH
CUSTOMER
BILLING
PAYMENT
MITRA
RADIUS
MIKROTIK
OLT
TOPOLOGY
IPAM
FIELDOPS
NOC
MONITORING
NOTIFICATION
REPORTS
UI
SECURITY
OPS
TESTING
DOCUMENTATION
```

Do not mark a task DONE without verification.

---

# 69. DOCUMENTATION FILES

Create:

```text
README.md
TASK.md
DESIGN.md
ARCHITECTURE.md
DATABASE.md
API.md
RADIUS.md
MIKROTIK.md
OLT-ZTE.md
TOPOLOGY.md
IPAM.md
BILLING.md
PAYMENT.md
FIELDOPS.md
NOC.md
MONITORING.md
SECURITY.md
DEPLOYMENT.md
TESTING.md
```

---

# 70. AI CODING AGENT EXECUTION

Before coding:

1. Inspect repository.
2. Inspect existing frontend.
3. Inspect existing backend.
4. Inspect database.
5. Inspect Redis.
6. Inspect integrations.
7. Inspect current authentication.
8. Inspect current billing.
9. Inspect MikroTik integration.
10. Inspect ZTE integration.
11. Read all project documentation.
12. Create architecture plan.
13. Create migrations.
14. Create TASK.md.
15. Implement in dependency order.

For every task:

```text
IMPLEMENT
 ↓
TEST
 ↓
LINT
 ↓
BUILD
 ↓
VERIFY
 ↓
DOCUMENT
 ↓
UPDATE TASK.md
```

Never claim completion without actual verification.

Do not rewrite working code unnecessarily.

---

# 71. IMPLEMENTATION ORDER

Use this order:

```text
1. Repository audit
2. Architecture
3. Go foundation
4. PostgreSQL
5. Redis
6. Auth/RBAC
7. Tenant
8. Customer
9. Products/Packages
10. Services/Subscriptions
11. Billing
12. Payment Gateway
13. IPAM
14. FreeRADIUS
15. MikroTik
16. ZTE OLT
17. Topology
18. FieldOps
19. NOC
20. Monitoring
21. Notifications
22. Reports
23. Realtime
24. Complete UI
25. Testing
26. Security
27. Docker
28. CI/CD
29. Backup/Restore
30. Production verification
```

Do not build all UI pages before their API/domain contracts are understood.

---

# 72. PRODUCTION ACCEPTANCE

The platform is complete only when:

### Core
- [ ] Go backend
- [ ] PostgreSQL
- [ ] Redis
- [ ] Authentication
- [ ] RBAC
- [ ] Multi-tenant

### Customer
- [ ] Customer
- [ ] Customer 360
- [ ] Services
- [ ] Subscriptions

### Billing
- [ ] Packages
- [ ] Invoices
- [ ] Payments
- [ ] Payment Gateway
- [ ] Webhooks
- [ ] Overdue
- [ ] Grace Period
- [ ] Suspension
- [ ] Reactivation
- [ ] Reports

### Network
- [ ] Static
- [ ] DHCP
- [ ] PPPoE
- [ ] Hotspot
- [ ] IPv4
- [ ] IPv6
- [ ] IPAM

### RADIUS
- [ ] FreeRADIUS 3.2.x
- [ ] SQL
- [ ] Accounts
- [ ] Profiles
- [ ] Authentication
- [ ] Authorization
- [ ] Accounting
- [ ] Sessions
- [ ] CoA
- [ ] Disconnect
- [ ] NAS
- [ ] HA
- [ ] Monitoring

### MikroTik
- [ ] Router management
- [ ] RouterOS API
- [ ] PPPoE
- [ ] Hotspot
- [ ] DHCP
- [ ] IP Pool
- [ ] Health

### ZTE
- [ ] snmp-olt-zte v3.2.0
- [ ] Multi-OLT
- [ ] C300
- [ ] C320
- [ ] PON
- [ ] ONU
- [ ] Profiles
- [ ] Optical
- [ ] Alarm
- [ ] Monitoring

### FTTH
- [ ] OLT
- [ ] PON
- [ ] ODC
- [ ] ODP
- [ ] ONU
- [ ] Customer
- [ ] Dependency mapping
- [ ] Interactive topology

### Operations
- [ ] FieldOps
- [ ] Technician
- [ ] Schedule
- [ ] Work Orders
- [ ] NOC
- [ ] Tickets
- [ ] Incidents
- [ ] SLA
- [ ] Monitoring
- [ ] Alerts

### UI/UX
- [ ] Dark shadcn/ui
- [ ] Shared AppShell
- [ ] Sidebar
- [ ] Topbar
- [ ] Dashboard
- [ ] Billing UI
- [ ] Customer UI
- [ ] RADIUS UI
- [ ] MikroTik UI
- [ ] OLT UI
- [ ] Topology UI
- [ ] IPAM UI
- [ ] FieldOps UI
- [ ] NOC UI
- [ ] Monitoring UI
- [ ] Mitra UI
- [ ] Reports UI
- [ ] Administration UI
- [ ] Responsive
- [ ] Accessibility
- [ ] Loading states
- [ ] Empty states
- [ ] Error states
- [ ] Realtime indicator

### Operations
- [ ] Docker
- [ ] CI/CD
- [ ] Backup
- [ ] Restore
- [ ] Monitoring
- [ ] Documentation
- [ ] Security review

---

# 73. ABSOLUTE RULES

1. Do NOT use Laravel.
2. Use Go as the primary backend.
3. Keep FreeRADIUS standalone.
4. Do NOT implement a custom RADIUS server.
5. Keep `snmp-olt-zte v3.2.0`.
6. Do not replace the ZTE library without explicit approval.
7. Do not expose secrets.
8. Do not bypass tenant isolation.
9. Do not put business logic in handlers.
10. Do not duplicate IPAM logic.
11. Do not duplicate RADIUS authentication.
12. Prefer modular monolith before microservices.
13. Maintain TASK.md.
14. Test every feature.
15. Document every production feature.
16. Keep UI consistent across every module.
17. Use the provided UI reference as the visual benchmark.
18. Never claim a feature is complete without verification.

END OF MASTER PROMPT
