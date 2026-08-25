# MASTER BUILD PROMPT
# ISP FTTH OSS/BSS + NMS + FIELD SERVICE PLATFORM
# HYBRID LARAVEL + GO

## ROLE OF THE AI CODING AGENT

Act as the principal software architect, senior Laravel engineer,
senior Go network engineer, senior React engineer, database architect,
DevOps engineer, QA engineer and UI/UX engineer.

Your responsibility is to DESIGN, BUILD, TEST, DOCUMENT and FIX this
application.

Do not merely generate scaffolding.

Do not stop after creating migrations or UI mockups.

Implement functional modules end-to-end.

When real network equipment is unavailable, use proper adapter
interfaces and realistic mock/simulator implementations. Never fake
successful production operations.

Never expose credentials or secrets.

Prefer security, maintainability, observability and scalability.

============================================================
1. PRODUCT
============================================================

Build a production-grade ISP FTTH Operations Platform for:

PT Susu Teknologi Indonesia

The product is a unified:

OSS
BSS
CRM
Billing
Payment
RADIUS
MikroTik Management
ZTE OLT Management
FTTH Topology
NOC
Monitoring
Alarm
Incident Management
Ticketing
PSB
Technician Management
Work Order
Scheduling
Dispatch
Partner Portal
Customer Portal

The modules must operate as ONE integrated platform.

============================================================
2. TARGET SCALE
============================================================

Design for:

10,000+
50,000+
100,000+ customers

Potential network:

Hundreds of OLTs
Thousands of PONs
Hundreds of thousands of ONUs

Use:
- database indexes
- pagination
- caching
- Redis
- queues
- worker pools
- batching
- lazy loading
- event-driven processing
- concurrency control

Never load the complete ONU/topology dataset into the browser.

============================================================
3. CORE ARCHITECTURE
============================================================

Use HYBRID ARCHITECTURE.

Laravel handles BUSINESS / OSS / BSS.

Go handles NETWORK / NMS / high-concurrency collectors.

React handles the UI.

Recommended:

                    INTERNET
                       |
                     NGINX
                       |
              +--------+--------+
              |                 |
              v                 v
          LARAVEL              GO
          OSS/BSS          NETWORK ENGINE
              |                 |
              |                 +-- ZTE OLT
              |                 +-- MikroTik
              |                 +-- SNMP
              |                 +-- SSH
              |                 +-- ICMP
              |                 +-- RADIUS
              |                 +-- Polling
              |                 +-- Network Events
              |                 +-- Provisioning
              |
              +---------+-------+
                        |
                      Redis
                        |
                 Event / Queue
                        |
                    WebSocket
                        |
                      React

Go must NOT bypass Laravel business rules for customer/billing
operations.

Prefer:
Go -> internal API/event -> Laravel business service.

============================================================
4. TECHNOLOGY STACK
============================================================

FRONTEND:
- React
- TypeScript
- Inertia.js
- Tailwind CSS
- shadcn/ui
- Lucide React
- TanStack Table
- React Hook Form
- Zod
- Recharts
- React Flow
- FullCalendar
- MapLibre or Leaflet

LARAVEL:
- Laravel 12
- PHP 8.3+
- Sanctum
- Horizon
- Reverb
- Queue
- Scheduler
- Events
- Notifications
- Policies
- API Resources

GO:
- current stable Go version
- Chi or Fiber if useful
- goroutines
- worker pools
- context cancellation
- connection pooling
- retry/backoff
- circuit breakers
- structured logging
- graceful shutdown

DATABASE:
- PostgreSQL 16+
- PostGIS

INFRA:
- Redis
- Nginx
- Docker
- Docker Compose
- PHP-FPM

NETWORK:
- FreeRADIUS
- MikroTik RouterOS API/REST/SSH
- ZTE OLT SSH/SNMP
- SNMP
- ICMP
- TCP health checks

============================================================
5. REPOSITORY
============================================================

Use a monorepo:

isp-platform/

apps/
  api/                 Laravel
  web/                 React/Inertia
  network-engine/      Go

packages/
  shared-types/

database/
docs/
infra/
scripts/

docker-compose.yml
.env.example
README.md
MASTER_PROMPT.md
TASK.md
DESIGN.md
ERD.md
API.md
NETWORK.md
TOPOLOGY.md
NOC.md
TECHNICIAN.md
SCHEDULING.md
PROVISIONING.md
SECURITY.md

============================================================
6. DOMAIN OWNERSHIP
============================================================

LARAVEL:

Customer
CRM
Billing
Invoice
Payment
Subscription
Package
Partner
Commission
Ticket
PSB
Survey
Installation
Work Order
Technician
Scheduling
Dispatch
SLA
Notification
Reports
RBAC
Audit
Portals
Business topology metadata

GO:

ZTE OLT
PON
ONU
MikroTik
RADIUS collectors
SNMP
ICMP
SSH
Network discovery
Network polling
Network alarms
Optical telemetry
Network provisioning
Network commands
Network health
Network realtime events

============================================================
7. AUTHENTICATION / RBAC
============================================================

Roles:

SUPER_ADMIN
ADMIN
FINANCE
BILLING
NOC
NETWORK_ENGINEER
TECHNICIAN
DISPATCHER
SUPERVISOR
SALES
CUSTOMER_SERVICE
PARTNER
CUSTOMER

Support:
- login
- logout
- password reset
- 2FA
- device/session management
- logout all sessions

Use granular permissions.

Examples:

customer.view
customer.create
customer.update
customer.delete
billing.view
billing.create
billing.update
payment.view
payment.refund
olt.view
olt.create
olt.update
olt.delete
olt.sync
olt.command
onu.view
onu.provision
onu.deprovision
topology.view
topology.trace
topology.impact
workorder.view
workorder.create
workorder.assign
workorder.schedule
workorder.complete
technician.view
technician.schedule
technician.location

============================================================
8. MULTI TENANCY
============================================================

Support:
- company
- region
- area
- POP
- partner

Implement:
- tenant middleware
- tenant-scoped queries
- tenant policies
- tenant-aware jobs
- tenant-aware events
- tenant isolation tests

Never allow cross-tenant access.

============================================================
9. CRM / CUSTOMER
============================================================

Lifecycle:

LEAD
-> PROSPECT
-> SURVEY
-> APPROVED
-> INSTALLATION
-> ACTIVE

Statuses:

ACTIVE
SUSPENDED
ISOLATED
TERMINATED
BLACKLISTED

Customer fields:

customer_id
customer_number
name
email
phone
whatsapp
identity_number
address
village
district
city
province
postal_code
latitude
longitude
partner_id
sales_id
status
notes

Customer tabs:

Overview
Contact
Address
Subscription
Billing
Payment
Network
Topology
ONU
IP
RADIUS
Tickets
Incidents
Work Orders
Installation
Documents
Activity

Global search:
Customer ID
Name
Phone
WhatsApp
ONU Serial
ONU MAC
ODP
ODC
OLT
PON
IP
PPPoE Username
Invoice
Work Order

============================================================
10. PACKAGE / SERVICE
============================================================

Package:

name
code
description
download_speed
upload_speed
burst_limit
priority
price
installation_fee
recurring_fee
billing_cycle
tax
fup_limit
fup_speed
status

Service types:

STATIC
DHCP
PPPOE
HOTSPOT

============================================================
11. SUBSCRIPTION
============================================================

Support multiple subscriptions per customer.

Fields:

customer_id
package_id
service_type
username
encrypted_password
static_ip
ipv6_prefix
vlan
radius_profile
mikrotik_profile
activation_date
billing_date
due_date
status

Statuses:
PENDING
ACTIVE
SUSPENDED
TERMINATED

============================================================
12. BILLING
============================================================

Entities:

Invoice
InvoiceItem
Payment
CreditNote
Refund
Discount
Tax
BillingCycle

Invoice statuses:

DRAFT
PENDING
PARTIAL
PAID
OVERDUE
CANCELLED
REFUNDED

Financial records must be audited and must not be physically deleted.

============================================================
13. PAYMENT GATEWAY
============================================================

Use:

PaymentGatewayInterface

Initial adapters:
- Midtrans
- Xendit

Support:
- Virtual Account
- QRIS
- E-wallet
- Bank Transfer
- Card where supported

Flow:

Invoice
-> Payment
-> Gateway
-> Webhook
-> Verify signature
-> Idempotency
-> Payment transaction
-> Invoice PAID
-> Service activation
-> Provisioning
-> Notification

Webhook must be:
- signed
- verified
- idempotent
- retryable
- audited

============================================================
14. RADIUS
============================================================

Integrate FreeRADIUS.

Support:
- authentication
- authorization
- accounting

Services:
- PPPoE
- Hotspot

Use:
radcheck
radreply
radgroupcheck
radgroupreply
radacct

Track:
username
NAS
session_id
IP
start
stop
duration
upload
download

============================================================
15. MIKROTIK GO ENGINE
============================================================

Create:

MikrotikAdapter interface

Implement:
- RouterOS API
- REST
- SSH fallback

Functions:

TestConnection
GetIdentity
GetInterfaces
GetVlans
GetRoutes
GetARP
GetDHCPLeases
GetPPPoESessions
GetHotspotSessions
DisconnectPPPoE
DisconnectHotspot
CreateAddress
RemoveAddress
CreateQueue
UpdateQueue
DisableUser
EnableUser
BackupConfiguration

Credentials must be encrypted.

Never permit arbitrary frontend shell commands.

============================================================
16. ZTE GO ENGINE
============================================================

Create:

OltAdapter interface

Implement:
- ZteC300Adapter
- ZteC320Adapter
- ZteC600Adapter

Communication:
- SSH
- SNMP

Functions:

Connect
Disconnect
TestConnection
GetDeviceInfo
GetBoards
GetPonPorts
GetOnus
GetOnu
DiscoverOnus
AuthorizeOnu
DeleteOnu
GetOnuStatus
GetOpticalPower
GetOnuDistance
GetOnuTemperature
GetOnuMac
GetVlan
GetServicePorts
GetTcont
GetGemPorts
GetDbaProfiles
GetLineProfiles
GetServiceProfiles

Vendor-specific ZTE CLI belongs only in the Go adapter layer.

============================================================
17. GO NETWORK ENGINE
============================================================

Build:

apps/network-engine/

cmd/network-engine/main.go

internal/
  api/
  config/
  events/
  collector/
  worker/
  olt/zte/c300/
  olt/zte/c320/
  olt/zte/c600/
  mikrotik/
  radius/
  snmp/
  icmp/
  ssh/
  monitoring/
  alarms/
  provisioning/
  topology/
  health/
  metrics/

Use:
- bounded worker pools
- context cancellation
- timeouts
- connection reuse
- retry with exponential backoff
- circuit breaker
- per-device concurrency limits
- graceful shutdown

Never create unlimited goroutines.

============================================================
18. NETWORK COLLECTOR
============================================================

Monitor:
- OLT
- PON
- ONU
- MikroTik
- RADIUS
- Router
- Switch

Polling intervals must be configurable.

Suggested:
OLT: 30-60 sec
PON: 30-60 sec
ONU state: 30-60 sec
Optical: 1-5 min
MikroTik: 30-60 sec

Use jitter to avoid synchronized polling storms.

============================================================
19. NETWORK EVENTS
============================================================

Events:

OltOnline
OltOffline
OltAlarm
OltRecovered

PonOnline
PonOffline
PonDown
PonRecovered

OnuOnline
OnuOffline
OnuLos
OnuRecovered
OnuLowRx
OnuHighTemperature

RouterOnline
RouterOffline
PppoeConnected
PppoeDisconnected
HotspotLogin
HotspotLogout

RadiusSessionStarted
RadiusSessionStopped
RadiusAuthenticationFailed

Every event contains:

event_id
event_type
source
tenant_id
entity_type
entity_id
timestamp
severity
payload
correlation_id

============================================================
20. REALTIME
============================================================

The application MUST be realtime.

Architecture:

ZTE/MikroTik/SNMP
        |
        v
Go Collector
        |
        v
Network Event
        |
        v
Redis
        |
        +----> Laravel processing
        |
        +----> Realtime broadcast
                         |
                         v
                    WebSocket
                         |
                         v
                       React

Do not use browser polling for normal application events.

Use:
- Redis
- Laravel events
- Laravel broadcasting
- Reverb/WebSocket

If the architecture benefits from a Go realtime gateway, document and
implement it, but keep authorization and business rules centralized.

Channels:

company.{companyId}
region.{regionId}
pop.{popId}
olt.{oltId}
pon.{ponId}
customer.{customerId}
technician.{technicianId}
workorder.{workOrderId}
incident.{incidentId}
dispatcher.{regionId}
noc.{regionId}
admin.{companyId}

Authorize every private channel.

============================================================
21. REALTIME UI
============================================================

Update without browser refresh:

OLT status
PON status
ONU status
LOS
RX
Alarms
Incidents
Affected customer count
Technician status
Technician location
Work Order status
Payment status
Provisioning status

On WebSocket disconnect:
display "Realtime connection lost"

Automatically reconnect with exponential backoff.

After reconnect:
- resync current state
- reconcile missed events
- remove stale state

Never silently show stale data.

============================================================
22. EVENT LOG
============================================================

Store:

event_id
event_type
source
entity_type
entity_id
payload
created_at
processed_at
broadcasted_at
status

Statuses:
PENDING
PROCESSED
FAILED

Do not store secrets in payload.

============================================================
23. OLT / PON / ONU
============================================================

OLT:

code
name
vendor
model
serial_number
management_ip
snmp_port
ssh_port
username
encrypted_credentials
pop_id
region_id
latitude
longitude
status

OLT dashboard:
CPU
Memory
Temperature
Uptime
PON Count
ONU Count
Alarm Count

PON:

olt_id
slot
port
name
pon_type
capacity
status

PON metrics:
ONU Count
Online
Offline
LOS
Average RX
Average TX

ONU:

serial_number
mac_address
name
olt_id
pon_id
odc_id
odp_id
odp_port_id
customer_id
status
rx_power
tx_power
temperature
distance
last_seen

Statuses:
ONLINE
OFFLINE
LOS
UNKNOWN
DISABLED

Prevent duplicate active ONU assignment.

============================================================
24. FTTH TOPOLOGY
============================================================

Primary path:

POP
↓
OLT
↓
PON
↓
ODC
↓
FIBER CORE
↓
ODP
↓
ODP PORT
↓
DROP CABLE
↓
ONU
↓
CUSTOMER

Support:
POP
OLT
PON
ODC
ODP
ONU
Customer
Fiber
Fiber Core
Splitter
Splice Closure
Joint Box

============================================================
25. ODC / ODP
============================================================

ODC:

code
name
capacity
core_count
used_core
available_core
latitude
longitude
address
status
installation_date

ODP:

code
name
odc_id
capacity
used_ports
available_ports
latitude
longitude
address
status

ODP port:
port_number
status
onu_id
customer_id

Statuses:
AVAILABLE
RESERVED
USED
DAMAGED
BLOCKED

============================================================
26. FIBER / SPLITTER
============================================================

Fiber cable:
code
name
fiber_count
length
source
destination
route_geometry
status

Fiber core:
fiber_id
core_number
color
source
destination
status

Statuses:
CONNECTED
RESERVED
DAMAGED
AVAILABLE

Support:
splice
joint closure
splitter
route

Splitter ratios:
1:2
1:4
1:8
1:16
1:32
1:64

============================================================
27. TOPOLOGY ENGINE
============================================================

Use:

topology_nodes
- id
- type
- reference_id
- name
- latitude
- longitude
- status

topology_connections
- id
- source_node_id
- target_node_id
- connection_type
- fiber_core_id
- distance
- status
- valid_from
- valid_until

topology_connection_histories
- id
- connection_id
- old_source
- old_target
- changed_by
- reason
- changed_at

Preserve history.

Use React Flow for visualization.

Features:
- zoom
- pan
- search
- filter
- cluster
- trace
- impact
- node details
- edit
- maintenance
- incident

Lazy load topology.

============================================================
28. TRACE
============================================================

Customer -> OLT:

Customer
→ ONU
→ ODP
→ Fiber
→ ODC
→ PON
→ OLT
→ POP

OLT -> Customer:

OLT
→ PON
→ ODC
→ ODP
→ ONU
→ Customer

Trace from:
OLT
PON
ODC
ODP
ONU
Customer

============================================================
29. IMPACT ANALYSIS
============================================================

OLT down:
calculate PON, ODC, ODP, ONU, customer, service and revenue impact.

PON down:
calculate ODC, ODP, ONU and customers.

ODC down:
calculate ODP, ONU and customers.

ODP down:
calculate ONU and customers.

ONU down:
calculate customer.

============================================================
30. NOC / ALARM / INCIDENT
============================================================

NOC metrics:
OLT Online
OLT Offline
PON Down
ONU Online
ONU Offline
ONU LOS
Low RX
High Temperature
Critical Alarm
Open Incident
Open Ticket
Affected Customers

Alarm types:
OLT_DOWN
PON_DOWN
ONU_LOS
ONU_OFFLINE
LOW_RX
HIGH_RX
HIGH_TEMPERATURE
INTERFACE_DOWN
HIGH_CPU
HIGH_MEMORY
PACKET_LOSS

Severity:
INFO
WARNING
MAJOR
CRITICAL

Lifecycle:
OPEN
ACKNOWLEDGED
RESOLVED
CLOSED

Incident correlation example:

PON 1/1/3 DOWN

Create one root incident instead of hundreds of customer incidents.

Show:
12 ODP
2 ODC
148 ONU
143 Customers

Actions:
View Customers
Trace Topology
Create Work Order
Notify Customers
Create Maintenance

============================================================
31. TICKETING
============================================================

Categories:
Billing
Internet
Slow
LOS
ONU
Installation
Payment
Technical
Complaint
Other

Statuses:
OPEN
ASSIGNED
IN_PROGRESS
WAITING_CUSTOMER
WAITING_TECHNICIAN
RESOLVED
CLOSED

Priority:
LOW
NORMAL
HIGH
URGENT

Ticket must create a Work Order when field intervention is needed.

============================================================
32. PSB
============================================================

Workflow:

LEAD
→ SURVEY
→ APPROVED
→ SCHEDULED
→ TECHNICIAN
→ INSTALLATION
→ TEST
→ ACTIVATION
→ COMPLETED

Survey:
coverage
ODP
ODP port
distance
drop cable estimate
RX prediction
feasibility
GPS
photos
notes

Approved PSB automatically creates installation Work Order.

============================================================
33. TECHNICIAN
============================================================

Fields:

employee_number
name
phone
whatsapp
email
photo
team_id
region_id
area_id
status
skills
latitude
longitude
last_location_at

Statuses:
AVAILABLE
BUSY
ON_JOB
OFFLINE
LEAVE
SUSPENDED

Skills:
FTTH_INSTALLATION
FTTH_REPAIR
ONU
OLT
FIBER_SPLICE
ODP
ODC
NETWORK
MIKROTIK
CPE
SURVEY

============================================================
34. TECHNICIAN SCHEDULING
============================================================

Support:
- working hours
- breaks
- leave
- holiday
- overtime
- customer appointment

Create SchedulingService:

findAvailableTechnicians()
findAvailableSlots()
calculateTravelTime()
detectConflict()
calculateSLA()
suggestTechnician()
suggestSchedule()
optimizeRoute()

Consider:
skill
availability
workload
region
area
distance
travel time
job duration
priority
SLA
appointment

Rank:
Skill Match
Availability
Distance
Workload
SLA
Region
Priority

Do not allow overlapping jobs.

============================================================
35. WORK ORDER
============================================================

Fields:

work_order_number
job_type
title
description
customer_id
ticket_id
incident_id
psb_id
maintenance_id
topology_node_id
region_id
area_id
priority
status
assigned_team_id
assigned_technician_id
scheduled_start
scheduled_end
actual_start
actual_end
latitude
longitude
address
sla_deadline
notes

Statuses:

DRAFT
PENDING
SCHEDULED
ASSIGNED
EN_ROUTE
ARRIVED
IN_PROGRESS
WAITING
COMPLETED
CANCELLED
FAILED
RESCHEDULED

============================================================
36. DISPATCH
============================================================

Kanban:

UNASSIGNED
SCHEDULED
EN_ROUTE
ARRIVED
IN_PROGRESS
WAITING
COMPLETED

Card:
WO number
customer
job type
technician
priority
schedule
SLA
location

Drag and drop assignment.

============================================================
37. TECHNICIAN MOBILE
============================================================

Bottom navigation:

Home
Jobs
Map
Notifications
Profile

Job:
Customer
Address
Map
Call
WhatsApp
Navigate
Topology
Checklist
Photo
Measurement
Materials
Complete

Support offline:
job
checklist
photos
notes
measurements
signature

Sync when online with conflict resolution.

============================================================
38. WORK ORDER CHECKLIST
============================================================

PSB example:

[ ] Verify customer
[ ] Check ODP
[ ] Check ODP port
[ ] Install drop cable
[ ] Install ONU
[ ] Register ONU
[ ] Check RX
[ ] Check TX
[ ] Configure service
[ ] Internet test
[ ] Speed test
[ ] Customer confirmation
[ ] Photos

Items:
PENDING
COMPLETED
FAILED
SKIPPED

Skipped/failed requires reason.

============================================================
39. GPS / ROUTE / EVIDENCE
============================================================

Technician location:
latitude
longitude
accuracy
timestamp

Show:
current location
last location
job location
customer location

Field evidence:
before
during
after
ONU
ODP
cable
splicing

Metadata:
latitude
longitude
timestamp
technician_id
work_order_id

Route optimization:
distance
travel time
SLA
priority
appointment

============================================================
40. SLA
============================================================

Critical: 2 hours
High: 4 hours
Normal: 24 hours
Low: 72 hours

States:
SAFE
WARNING
BREACHED

Escalation:
warning
supervisor
breach

============================================================
41. MATERIAL / TOOL
============================================================

Materials:
ONU
Drop Cable
RJ45
Patch Cord
Adapter
Splitter
Fiber Closure
Splice Sleeve
Connector

Tools:
OTDR
Optical Power Meter
Fusion Splicer
VFL
Laptop
Crimping Tool

Inventory consumption must update stock.

============================================================
42. CUSTOMER PORTAL
============================================================

Show:
Internet status
Package
IP
Usage
Invoice
Payment
ONU
Ticket

Actions:
Pay Invoice
Download Invoice
Create Ticket
View Payment
View Usage

============================================================
43. PARTNER PORTAL
============================================================

Show:
Customers
Active Customers
PSB
Installation
Revenue
Commission
Outstanding

Actions:
Create Customer
Submit PSB
Track Installation
View Commission
View Invoice

Commission:
fixed
percentage
tiered

Statuses:
PENDING
APPROVED
PAID
CANCELLED

============================================================
44. NOTIFICATION
============================================================

Channels:
WhatsApp
Email
SMS
In-App
Push

Events:
Invoice Created
Invoice Reminder
Payment Received
Service Suspended
Service Activated
PSB Approved
Technician Assigned
Technician En Route
Installation Scheduled
Installation Completed
Maintenance
Incident
Incident Resolved
Work Order Rescheduled

Use provider adapters.

============================================================
45. IPAM / VLAN
============================================================

IPAM:
IPv4
IPv6
Public
Private
CGNAT
PPPoE
DHCP
Static
Hotspot

Statuses:
AVAILABLE
ALLOCATED
RESERVED
BLOCKED
QUARANTINE

Support:
Subnet
Prefix
Pool
Allocation
Release
History

VLAN:
ID
name
purpose
region
POP
OLT
service

Example:
165 STATIC
144 HOTSPOT
100 TR069

============================================================
46. PROVISIONING
============================================================

Laravel requests provisioning.

Go executes network steps.

Flow:

Create Customer
→ Create Subscription
→ Allocate IP
→ Create RADIUS
→ Configure MikroTik
→ Configure OLT
→ Authorize ONU
→ Assign ODP Port
→ Verify ONU
→ Verify RX
→ Verify RADIUS
→ Verify PPPoE
→ Activate

Every step:
PENDING
RUNNING
SUCCESS
FAILED
RETRY

Maintain provisioning transaction and logs.

If provisioning fails:
- show failed step
- retry
- rollback
- manual continuation

Never leave an unknown half-configured service silently.

============================================================
47. SERVICE SUSPENSION / REACTIVATION
============================================================

Overdue:

Invoice
→ Grace Period
→ Reminder
→ Suspension

Possible:
- RADIUS disable
- MikroTik disconnect
- service profile change
- address change where applicable

Payment:
→ verify
→ reactivate
→ reconnect
→ notify

============================================================
48. FUP
============================================================

Support:
- quota
- usage
- warning
- speed reduction
- reset

Example:
100 Mbps
2 TB
80% warning
90% warning
100% reduce to 20 Mbps

============================================================
49. REPORTING
============================================================

Reports:
Customer
Revenue
Invoice
Payment
Package
Partner
Commission
ONU
OLT
PON
ODC
ODP
Fiber
Usage
FUP
Incident
Ticket
Installation
Technician
Work Order
SLA

Export:
CSV
Excel
PDF

============================================================
50. DASHBOARDS
============================================================

ADMIN / MANAGEMENT:
Revenue
Customers
Active Services
Outstanding
Payment Today
OLT
ONU
Network Availability
Incidents
Tickets
Technician Operations

NOC:
OLT
PON
ONU
LOS
RX
Traffic
Alarms
Incidents
Impact

DISPATCHER:
Total Jobs
Unassigned
Scheduled
En Route
In Progress
SLA Risk
SLA Breached
Completed
Live Map
Dispatch Board

TECHNICIAN:
Today's Jobs
Completed
Pending
Next Job
Route
Map
SLA
Checklist
Notifications

PARTNER:
Customers
PSB
Installation
Revenue
Commission
Outstanding

CUSTOMER:
Internet
Package
Usage
Invoice
Payment
ONU
Ticket

============================================================
51. UI / UX
============================================================

Premium enterprise NOC/OSS style.

Do not use a generic admin template.

Support:
- light mode
- dark mode
- responsive desktop
- responsive mobile
- accessibility
- keyboard navigation
- meaningful status badges
- command-center dashboards
- interactive maps
- topology
- compact high-density tables

Technician UI must be much simpler than admin UI.

============================================================
52. DATABASE
============================================================

Create migrations for:

users
roles
permissions
companies
regions
areas
pops

customers
customer_contacts
customer_addresses

packages
subscriptions
subscription_histories

invoices
invoice_items
payments
payment_transactions
refunds
credit_notes

radius_accounts
radius_sessions

mikrotik_devices
mikrotik_profiles

olts
olt_ports
pons
onus

odcs
odc_ports
odps
odp_ports

fiber_cables
fiber_cores
fiber_splices
splitters

topology_nodes
topology_connections
topology_connection_histories

ip_pools
ip_subnets
ip_addresses

vlans

alarms
incidents
incident_customers

tickets
ticket_comments

psb_orders
surveys
installations

technicians
technician_teams
technician_skills
technician_availabilities
technician_leaves
technician_locations

job_types
work_orders
work_order_assignments
work_order_checklists
work_order_checklist_items
work_order_materials
work_order_tools
work_order_photos
work_order_measurements
work_order_comments
work_order_status_histories
work_order_locations
work_order_customer_signatures

customer_appointments
schedule_conflicts
technician_routes

technician_ratings
technician_performance_metrics

partners
partner_customers
partner_commissions

notifications
webhooks
audit_logs
event_logs
provisioning_jobs
provisioning_steps

============================================================
53. API
============================================================

Laravel:

/api/v1/customers
/api/v1/subscriptions
/api/v1/packages
/api/v1/invoices
/api/v1/payments
/api/v1/radius
/api/v1/mikrotik
/api/v1/olts
/api/v1/pons
/api/v1/onus
/api/v1/odcs
/api/v1/odps
/api/v1/fibers
/api/v1/splitters
/api/v1/topology
/api/v1/topology/trace
/api/v1/topology/impact
/api/v1/incidents
/api/v1/tickets
/api/v1/technicians
/api/v1/work-orders
/api/v1/scheduler
/api/v1/dispatch
/api/v1/partners
/api/v1/reports

Go internal:

/health
/ready
/metrics

/internal/network/olt/*
/internal/network/mikrotik/*
/internal/network/radius/*
/internal/network/provision/*
/internal/network/discovery/*

Internal network endpoints must not be publicly exposed.

Document all API contracts.

============================================================
54. GO OBSERVABILITY
============================================================

Expose:
- /health
- /ready
- /metrics

Metrics:
polling duration
polling success/failure
device count
active workers
queue depth
event count
event latency
OLT availability
ONU online/offline
SNMP errors
SSH errors
API errors

Use Prometheus-compatible metrics.

============================================================
55. QUEUES
============================================================

Laravel:
Redis + Horizon

Go:
bounded worker pools + Redis Streams/PubSub or another documented
event transport.

Jobs:
SyncOLT
SyncPON
SyncONU
PollSNMP
PollMikrotik
ProcessRadiusAccounting
GenerateInvoices
SendNotifications
ProcessPaymentWebhook
ProvisionCustomer
SuspendCustomer
ReactivateCustomer
CalculateUsage
DetectAlarm
CalculateTopologyImpact
ScheduleTechnician
OptimizeTechnicianRoute
SendSlaWarning

============================================================
56. NETWORK PROTECTION
============================================================

Per device:
- maximum concurrent SSH sessions
- maximum concurrent commands
- command timeout
- retry limit
- exponential backoff
- circuit breaker

Queue OLT commands.

Do not execute mass commands without authorization.

============================================================
57. SECURITY
============================================================

Implement:
CSRF
XSS protection
SQL injection protection
rate limiting
RBAC
2FA
credential encryption
webhook verification
API authentication
audit logs
secure headers
secret management

Never store plaintext:
OLT passwords
MikroTik passwords
RADIUS secrets
API tokens
payment secrets
SSH private keys

Never log secrets.

============================================================
58. AUDIT
============================================================

Audit:
login
logout
create
update
delete
payment
refund
provisioning
deprovisioning
ONU movement
ODP assignment
VLAN changes
IP allocation
network commands
work order assignment
schedule changes
technician location access

Store:
user
IP
user_agent
action
entity
before
after
timestamp

============================================================
59. PERFORMANCE / RESILIENCE
============================================================

Use:
- indexes
- composite indexes
- pagination
- server-side filtering
- caching
- Redis
- queues
- batching
- lazy loading
- virtualized tables
- connection pools
- worker pools

Avoid:
- N+1 queries
- unbounded goroutines
- full table scans
- huge WebSocket payloads
- full topology loads

If a device is unreachable:
- retry
- exponential backoff
- circuit breaker
- mark state UNKNOWN where appropriate
- never incorrectly show ONLINE

============================================================
60. BACKUP / DISASTER RECOVERY
============================================================

Support:
PostgreSQL backup
Redis persistence strategy
MikroTik backup
OLT configuration backup
application backup

Document:
backup schedule
retention
restore
RPO
RTO
disaster recovery

============================================================
61. DEVOPS
============================================================

Provide:
Dockerfile
docker-compose.yml
.env.example
Nginx
PHP-FPM
Laravel worker
Horizon
Scheduler
Reverb
PostgreSQL
Redis
Go network engine

Services:
nginx
web
api
network-engine
postgres
redis
horizon
scheduler
reverb

Add health checks and graceful shutdown.

============================================================
62. TESTING
============================================================

Create:
- Laravel unit tests
- Laravel feature tests
- API tests
- browser tests
- Go unit tests
- Go integration tests
- network adapter tests
- contract tests
- realtime tests
- load tests for critical services

Test:
authentication
RBAC
tenant isolation
customer
billing
payment
webhook
RADIUS
MikroTik
ZTE
ONU
topology
trace
impact
provisioning
incident
ticket
technician
scheduling
work order
PSB
partner
customer portal
realtime reconnect
event idempotency

Use simulated ZTE/MikroTik devices for integration testing.

============================================================
63. SEED DATA
============================================================

Company:
PT Susu Teknologi Indonesia

POP:
POP-PEJATEN

OLT:
OLT-C600-PEJATEN-01

PON:
1/1/1
1/1/2
1/1/3

ODC:
ODC-PEJATEN-01
ODC-PEJATEN-02

ODP:
ODP-PEJATEN-001
ODP-PEJATEN-002
ODP-PEJATEN-003

Packages:
20 Mbps
50 Mbps
100 Mbps
200 Mbps
500 Mbps

Services:
STATIC
DHCP
PPPOE
HOTSPOT

Seed at least:
100 customers
100 ONUs
10 technicians
3 teams
30 work orders
realistic topology
invoices
payments
tickets
alarms
incidents

============================================================
64. DOCUMENTATION
============================================================

Create:

README.md
ARCHITECTURE.md
DATABASE.md
ERD.md
API.md
DEPLOYMENT.md
SECURITY.md
NETWORK.md
ZTE-OLT.md
MIKROTIK.md
RADIUS.md
PAYMENT.md
PROVISIONING.md
TOPOLOGY.md
NOC.md
TECHNICIAN.md
SCHEDULING.md
WORK-ORDER.md
PARTNER.md
CUSTOMER-PORTAL.md
TASK.md
DESIGN.md

============================================================
65. TASK.MD
============================================================

Create a detailed backlog.

Statuses:
[ ] Not Started
[~] In Progress
[x] Completed

Every task:
ID
Priority
Description
Dependencies
Acceptance Criteria
Status

Phases:

P01 Foundation
P02 Authentication
P03 RBAC
P04 CRM
P05 Billing
P06 Payment
P07 RADIUS
P08 MikroTik
P09 Go Network Engine
P10 ZTE OLT
P11 PON/ONU
P12 IPAM
P13 VLAN
P14 ODC
P15 ODP
P16 Fiber
P17 Topology
P18 NOC
P19 Monitoring
P20 Alarm
P21 Incident
P22 Ticket
P23 PSB
P24 Technician
P25 Work Order
P26 Scheduling
P27 Dispatch
P28 Installation
P29 Partner
P30 Customer Portal
P31 Notification
P32 Realtime
P33 Reporting
P34 Security
P35 Testing
P36 Deployment

============================================================
66. DESIGN.MD
============================================================

Document:
design principles
color system
typography
spacing
layout
sidebar
topbar
cards
tables
forms
modal
drawer
toast
timeline
calendar
map
topology
charts
status badges
mobile
dark mode

Use premium enterprise OSS/NOC style.

============================================================
67. ERD
============================================================

Business:

Company
→ Region
→ Area
→ POP
→ OLT
→ PON
→ ODC
→ Fiber
→ ODP
→ ONU
→ Customer
→ Subscription
→ Invoice
→ Payment

Operations:

Customer
→ Ticket
→ Work Order
→ Technician
→ Schedule

Incident:

Alarm
→ Incident
→ Impact
→ Affected Customer
→ Work Order

============================================================
68. REALTIME BUSINESS FLOW
============================================================

Payment:

Customer pays
→ gateway webhook
→ Laravel verifies
→ invoice PAID
→ realtime event
→ React update
→ provisioning
→ Go network engine
→ RADIUS
→ MikroTik
→ OLT
→ ONU
→ verification
→ service active

============================================================
69. REALTIME NETWORK FLOW
============================================================

ONU LOS:

ZTE OLT
→ Go collector
→ state change
→ OnuLos event
→ Redis
→ Laravel processing
→ topology lookup
→ customer impact
→ alarm
→ WebSocket
→ NOC dashboard

No browser refresh.

============================================================
70. INCIDENT AUTOMATION
============================================================

PON 1/1/3 DOWN:

Go detects
→ Laravel creates alarm
→ topology impact
→ incident
→ affected customers
→ work order
→ technician recommendation
→ dispatcher approval
→ assignment
→ technician notification
→ repair
→ verify recovery
→ resolve incident
→ notify customers

============================================================
71. CUSTOMER TROUBLE FLOW
============================================================

Customer reports "Internet mati".

Immediately show:

Customer
Service
Package
IP
RADIUS
MikroTik
ONU
RX/TX
ODP
ODC
PON
OLT
Last Online
Last Offline
Recent Alarm

Diagnostic:
1. service
2. RADIUS
3. PPPoE session
4. MikroTik
5. ONU
6. optical
7. PON
8. OLT
9. topology impact

If field visit required:
create Work Order.

============================================================
72. PSB AUTOMATION
============================================================

PSB approved:

PSB
→ installation Work Order
→ required skill
→ available technicians
→ available slots
→ distance
→ SLA
→ recommendation
→ dispatcher approval
→ assignment
→ customer notification
→ technician notification

============================================================
73. WORK ORDER COMPLETION
============================================================

Do not allow completion when required fields are missing.

PSB example:
ONU serial required
ODP port required
RX required
Internet test required
Photo required
Customer confirmation required

After completion:
signature
evidence
timeline
inventory consumption
topology update
service activation if applicable
customer notification

============================================================
74. ACCEPTANCE CRITERIA
============================================================

The platform is accepted when:

Customer creation works.
Package creation works.
Subscription works.
Invoice generation works.
Payment works.
Payment webhook works.
Invoice becomes PAID.
RADIUS works.
MikroTik integration works.
ZTE OLT integration works.
ONU discovery works.
ONU provisioning works.
ONU assignment to ODP works.
Customer-to-ONU mapping works.
Topology visualization works.
Customer-to-OLT trace works.
OLT-to-customer trace works.
ODC trace works.
ODP trace works.
PON impact analysis works.
OLT impact analysis works.
ONU failure identifies customer.
PON failure identifies affected customers.
Incident creation works.
Work Order works.
Technician assignment works.
Schedule conflict detection works.
Technician receives job.
Technician starts job.
Technician uploads evidence.
Checklist works.
Customer signature works.
Work Order completion works.
Notifications work.
PSB creates Work Order.
Ticket creates Work Order.
Incident creates Work Order.
Technician recommendation works.
Schedule recommendation works.
SLA works.
NOC dashboard works.
Dispatcher dashboard works.
Technician dashboard works.
Management dashboard works.
Partner dashboard works.
Customer portal works.
Realtime works without refresh.
WebSocket reconnect works.
Network polling works.
Network events work.
Credential encryption works.
Sensitive actions are audited.
Payment webhook is idempotent.
Provisioning retry works.
Provisioning rollback works.
Topology history is preserved.
Backup/restore is documented.
Application can be deployed.

============================================================
75. DEVELOPMENT EXECUTION RULE
============================================================

Before coding:

1. Inspect repository.
2. Create architecture.
3. Create module map.
4. Create ERD.
5. Create TASK.md.
6. Create DESIGN.md.
7. Create API.md.
8. Create documentation skeleton.

Then implement phases in order.

After every phase:
- run tests
- run lint/static analysis
- build frontend
- build Go
- fix errors
- update TASK.md
- update documentation

Do not jump randomly between modules.

Do not build UI without backend contract.

Do not build backend without data model.

Do not build network integration without adapter interfaces.

Do not create fake successful responses.

Do not mark unfinished features as completed.

When a design decision is ambiguous, choose the most secure,
maintainable and scalable option and document the decision.

============================================================
76. FINAL PRINCIPLE
============================================================

Build an ISP OPERATING SYSTEM.

Not only:
billing
CRM
NMS
topology
technician calendar

Build:

UNIFIED ISP OPERATIONS PLATFORM

BUSINESS
+
BILLING
+
PAYMENT
+
RADIUS
+
MIKROTIK
+
ZTE OLT
+
ONU
+
FTTH TOPOLOGY
+
NOC
+
INCIDENT
+
TICKETING
+
TECHNICIAN
+
WORK ORDER
+
SCHEDULING
+
DISPATCH
+
PARTNER
+
CUSTOMER

All modules must share:
- customer identity
- topology
- network state
- event model
- permissions
- audit
- notifications
- operational history

============================================================
END OF MASTER BUILD PROMPT
============================================================
