# MASTER PROMPT — ISP FTTH OPERATIONS PLATFORM

## 1. PROJECT

Build a production-grade ISP FTTH Billing, CRM, Network Management, Provisioning, FTTH Topology, NOC, Field Operations, Technician Scheduling, Partner Portal and Customer Portal platform.

Demo/company seed:
**PT Susu Teknologi Indonesia**

This is NOT a simple billing CRUD. Build a unified ISP operational platform connecting:

Customer + Billing + Payment + RADIUS + MikroTik + ZTE OLT + ONU + ODP + ODC + Fiber + Topology + NOC + Incident + Ticket + Technician + Work Order + Scheduling + PSB + Partner + Customer Portal.

---

# 2. TECHNOLOGY STACK

## Backend
- Laravel 12
- PHP 8.3+
- Laravel Sanctum
- Laravel Horizon
- Laravel Reverb
- Laravel Queue
- Laravel Scheduler
- Laravel Events
- Laravel Notifications

## Frontend
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

## Database
- PostgreSQL 16+
- PostGIS for geographic/network data

## Infrastructure
- Redis
- Nginx
- Docker
- Docker Compose
- PHP-FPM

## Network
- FreeRADIUS
- MikroTik RouterOS API/REST/SSH
- ZTE OLT SSH
- ZTE OLT SNMP

## Maps
- MapLibre or Leaflet
- Create a map-provider adapter so the provider can be changed later.

---

# 3. ARCHITECTURE

Use a modular monolith architecture.

Controllers must be thin. Business logic must live in domain/application services.

Suggested:

app/
- Domain/
  - Customer/
  - CRM/
  - Billing/
  - Payment/
  - Subscription/
  - Radius/
  - Mikrotik/
  - Olt/
  - Onu/
  - Ftth/
  - Topology/
  - Fiber/
  - Odc/
  - Odp/
  - Splitter/
  - Ipam/
  - Vlan/
  - Noc/
  - Monitoring/
  - Alarm/
  - Incident/
  - Ticket/
  - Technician/
  - WorkOrder/
  - Scheduling/
  - Installation/
  - Partner/
  - Commission/
  - Notification/
  - Report/
  - Audit/
- Application/
- Infrastructure/
- Shared/

Use:
- Services
- Actions
- DTOs
- Enums
- Value Objects
- Events
- Listeners
- Jobs
- Policies
- Form Requests
- API Resources
- Adapters
- Interfaces

---

# 4. MULTI TENANCY

Support:

Company
Region
Area
POP
Partner

Major business records must have tenant_id where appropriate.

Implement:
- Tenant middleware
- Tenant-aware queries
- Tenant-aware policies
- Tenant-aware jobs
- Tenant isolation tests

A user must never access another tenant's data.

---

# 5. AUTHENTICATION AND RBAC

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

Implement granular permissions such as:

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

Support:
- Password login
- Password reset
- 2FA
- Session/device management
- Logout all sessions

---

# 6. CRM / CUSTOMER

Customer lifecycle:

LEAD
→ PROSPECT
→ SURVEY
→ APPROVED
→ INSTALLATION
→ ACTIVE

Statuses:
ACTIVE
SUSPENDED
ISOLATED
TERMINATED
BLACKLISTED

Customer fields:
- customer_id
- customer_number
- name
- email
- phone
- whatsapp
- identity_number
- address
- village
- district
- city
- province
- postal_code
- latitude
- longitude
- partner_id
- sales_id
- status
- notes

Customer detail tabs:
- Overview
- Contact
- Address
- Subscription
- Billing
- Payment
- Network
- Topology
- ONU
- IP
- RADIUS
- Tickets
- Incidents
- Work Orders
- Installation
- Documents
- Activity

Global search must support:
- Customer ID
- Name
- Phone
- WhatsApp
- ONU serial
- ONU MAC
- ODP
- ODC
- OLT
- PON
- IP
- PPPoE username
- Invoice
- Work Order

---

# 7. PACKAGE

Package fields:
- name
- code
- description
- download_speed
- upload_speed
- burst_limit
- priority
- price
- installation_fee
- recurring_fee
- billing_cycle
- tax
- fup_limit
- fup_speed
- status

Service types:
- STATIC
- DHCP
- PPPOE
- HOTSPOT

---

# 8. SUBSCRIPTION

Support multiple subscriptions per customer.

Fields:
- customer_id
- package_id
- service_type
- username
- encrypted_password
- static_ip
- ipv6_prefix
- vlan
- radius_profile
- mikrotik_profile
- activation_date
- billing_date
- due_date
- status

Statuses:
PENDING
ACTIVE
SUSPENDED
TERMINATED

---

# 9. BILLING

Entities:
- Invoice
- InvoiceItem
- Payment
- CreditNote
- Refund
- Discount
- Tax
- BillingCycle

Invoice statuses:
DRAFT
PENDING
PARTIAL
PAID
OVERDUE
CANCELLED
REFUNDED

Financial records must never be physically deleted.

Automated billing:
Generate invoice → notify → payment → verify → mark paid → activate/provision service.

---

# 10. PAYMENT GATEWAY

Use adapter architecture.

Interface:
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

Webhook:
- Verify signature
- Idempotency
- Audit
- Retry
- Error logging without secrets

Flow:

Invoice
→ Payment
→ Gateway
→ Webhook
→ Verify
→ Idempotency check
→ Payment transaction
→ Invoice PAID
→ Provision/activate
→ Notification

---

# 11. RADIUS

Integrate FreeRADIUS.

Support:
- Authentication
- Authorization
- Accounting

Support service:
- PPPoE
- Hotspot

RADIUS tables:
- radcheck
- radreply
- radgroupcheck
- radgroupreply
- radacct

Track:
- username
- NAS
- session_id
- IP
- start
- stop
- duration
- upload
- download

Customer service status must synchronize with RADIUS status.

---

# 12. MIKROTIK

Create:

MikrotikAdapterInterface

Adapters:
- RouterOS API
- RouterOS REST
- SSH fallback

Device:
- hostname
- identity
- management_ip
- api_port
- ssh_port
- username
- encrypted_credentials
- version
- model
- location
- status

Functions:
- testConnection
- getIdentity
- getInterfaces
- getVlans
- getRoutes
- getARP
- getDHCPLeases
- getPPPoESessions
- getHotspotSessions
- disconnectPPPoE
- disconnectHotspot
- createAddress
- removeAddress
- createQueue
- updateQueue
- disableUser
- enableUser
- backupConfiguration

Never execute arbitrary frontend commands. Use approved command services and audit sensitive operations.

---

# 13. ZTE OLT

Create:

OltAdapterInterface

Implement:
- ZteC300Adapter
- ZteC320Adapter
- ZteC600Adapter

Communication:
- SSH
- SNMP

Methods:
- connect
- disconnect
- testConnection
- getDeviceInfo
- getBoards
- getPonPorts
- getOnus
- getOnu
- discoverOnus
- authorizeOnu
- deleteOnu
- getOnuStatus
- getOpticalPower
- getOnuDistance
- getOnuTemperature
- getOnuMac
- getVlan
- getServicePorts
- getTcont
- getGemPorts
- getDbaProfiles
- getLineProfiles
- getServiceProfiles

Vendor-specific ZTE CLI commands must exist only in adapter/infrastructure classes, never in controllers.

---

# 14. OLT / PON / ONU MANAGEMENT

OLT:
- code
- name
- vendor
- model
- serial_number
- management_ip
- SNMP
- SSH
- credentials encrypted
- POP
- region
- coordinates
- status

OLT dashboard:
- CPU
- Memory
- Temperature
- Uptime
- PON count
- ONU count
- Alarm count

PON:
- olt_id
- slot
- port
- name
- pon_type
- capacity
- status

PON metrics:
- ONU count
- Online
- Offline
- LOS
- Average RX
- Average TX

ONU:
- serial_number
- mac_address
- name
- olt_id
- pon_id
- odc_id
- odp_id
- odp_port_id
- customer_id
- status
- rx_power
- tx_power
- temperature
- distance
- last_seen

ONU statuses:
ONLINE
OFFLINE
LOS
UNKNOWN
DISABLED

Prevent duplicate active ONU assignments.

---

# 15. FTTH TOPOLOGY ENGINE

Topology is a core domain, not just a visualization.

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

Support nodes:
- POP
- OLT
- PON
- ODC
- ODP
- ONU
- Customer
- Fiber
- Fiber Core
- Splitter
- Splice Closure
- Joint Box

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

Topology history must be preserved.

---

# 16. ODC

Fields:
- code
- name
- capacity
- core_count
- used_core
- available_core
- latitude
- longitude
- address
- status
- installation_date

Support:
- Input
- Output
- Fiber Core
- Splitter
- Splice

---

# 17. ODP

Fields:
- code
- name
- odc_id
- capacity
- used_ports
- available_ports
- latitude
- longitude
- address
- status

ODP ports:
- port_number
- status
- onu_id
- customer_id

Statuses:
AVAILABLE
RESERVED
USED
DAMAGED
BLOCKED

Prevent duplicate active ODP port assignments.

---

# 18. FIBER MANAGEMENT

Support:
- Fiber Cable
- Fiber Core
- Splice
- Splitter
- Joint Closure
- Route

Fiber cable:
- code
- name
- fiber_count
- length
- source
- destination
- route_geometry
- status

Fiber core:
- fiber_id
- core_number
- color
- source
- destination
- status

Statuses:
CONNECTED
RESERVED
DAMAGED
AVAILABLE

---

# 19. SPLITTER

Support:
1:2
1:4
1:8
1:16
1:32
1:64

Fields:
- type
- input
- output
- location
- odc_id
- odp_id
- status

---

# 20. TOPOLOGY VISUALIZATION

Use React Flow.

Node types:
- POP
- OLT
- PON
- ODC
- ODP
- ONU
- CUSTOMER
- FIBER

Features:
- Zoom
- Pan
- Search
- Filter
- Cluster
- Trace
- Impact Analysis
- Node detail
- Edit
- Maintenance
- Incident

Do not load the entire network graph initially. Use lazy loading.

---

# 21. TRACE PATH

Customer → OLT:

Customer
→ ONU
→ ODP
→ Fiber
→ ODC
→ PON
→ OLT
→ POP

OLT → Customer:

OLT
→ PON
→ ODC
→ ODP
→ ONU
→ Customer

Allow tracing from:
- OLT
- PON
- ODC
- ODP
- ONU
- Customer

---

# 22. IMPACT ANALYSIS

If OLT down:
calculate affected PON, ODC, ODP, ONU, customers, services and estimated revenue.

If PON down:
calculate affected ODC, ODP, ONU and customers.

If ODC down:
calculate affected ODP, ONU and customers.

If ODP down:
calculate affected ONU and customers.

If ONU down:
calculate affected customer.

Display:
- Affected network elements
- Affected services
- Affected customers
- Affected packages
- Estimated revenue impact

---

# 23. NOC

Create real-time NOC command center.

Metrics:
- OLT Online
- OLT Offline
- PON Down
- ONU Online
- ONU Offline
- ONU LOS
- Low RX
- High Temperature
- Customer Offline
- Critical Alarms
- Open Incidents
- Open Tickets

Charts:
- ONU status
- OLT availability
- Alarm trend
- Traffic
- SLA
- Incident trend

Use Laravel Reverb for realtime events.

---

# 24. MONITORING

Use:
- SNMP
- ICMP
- SSH
- API

Monitor:
- OLT
- MikroTik
- Router
- Switch

Metrics:
- CPU
- Memory
- Temperature
- Interface traffic
- Packet loss
- Latency
- Uptime
- ONU status
- RX/TX

---

# 25. ALARM MANAGEMENT

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

---

# 26. INCIDENT MANAGEMENT

Implement alarm correlation.

Example:

PON 1/1/3 DOWN

Do not create hundreds of individual incidents.

Create:
INC-2026-000001

Root cause:
PON 1/1/3

Affected:
- 2 ODC
- 12 ODP
- 148 ONU
- 143 customers

Actions:
- View Customers
- Trace Topology
- Create Work Order
- Notify Customers
- Create Maintenance

---

# 27. TICKETING

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

A ticket that requires field work must be able to create a Work Order.

---

# 28. PSB

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
- Coverage
- ODP
- ODP Port
- Distance
- Drop Cable Estimate
- RX prediction
- Feasibility
- GPS
- Photos
- Notes

When PSB is approved, automatically generate an installation Work Order.

---

# 29. TECHNICIAN MANAGEMENT

Technician:
- employee_number
- name
- phone
- whatsapp
- email
- photo
- team_id
- region_id
- area_id
- status
- skills
- latitude
- longitude
- last_location_at

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

---

# 30. TECHNICIAN TEAM

Support:
- Team
- Team Leader
- Region
- Area
- Skills
- Status

Example:
TEAM-PEJATEN-01
TEAM-PEJATEN-02
TEAM-SERANG-01

---

# 31. TECHNICIAN AVAILABILITY

Support:
- Working hours
- Break
- Leave
- Holiday
- Overtime

Example:
Monday 08:00–17:00
Break 12:00–13:00

Scheduler must prevent invalid booking.

---

# 32. JOB TYPES

Configurable job types:

PSB_INSTALLATION
SURVEY
ONU_REPLACEMENT
ONU_RELOCATION
LOS_REPAIR
SLOW_CONNECTION
CPE_REPLACEMENT
ODP_REPAIR
ODC_REPAIR
FIBER_REPAIR
SPLICING
MAINTENANCE
PREVENTIVE_MAINTENANCE
CUSTOMER_VISIT
TICKET
INCIDENT
DISMANTLING

Each job type:
- name
- code
- default_duration
- required_skill
- priority
- checklist
- sla_minutes
- required_tools
- required_materials

---

# 33. WORK ORDER

Fields:
- work_order_number
- job_type
- title
- description
- customer_id
- ticket_id
- incident_id
- psb_id
- maintenance_id
- topology_node_id
- region_id
- area_id
- priority
- status
- assigned_team_id
- assigned_technician_id
- scheduled_start
- scheduled_end
- actual_start
- actual_end
- latitude
- longitude
- address
- sla_deadline
- notes

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

---

# 34. TECHNICIAN SCHEDULING

Create SchedulingService.

The scheduler must consider:
- Technician availability
- Skill match
- Current workload
- Region
- Area
- Distance
- Travel time
- Job duration
- Priority
- SLA
- Customer appointment
- Existing schedule

Do not allow overlapping jobs unless explicitly overridden by authorized role.

Methods:
findAvailableTechnicians()
findAvailableSlots()
calculateTravelTime()
detectConflict()
calculateSLA()
suggestTechnician()
suggestSchedule()
optimizeRoute()

Ranking:
Skill Match
+ Availability
+ Distance
+ Workload
+ SLA
+ Region
+ Priority

Example:
Budi — 94
Andi — 87
Dedi — 72

---

# 35. CALENDAR SCHEDULER

Use FullCalendar or equivalent.

Views:
- Day
- Week
- Month
- Timeline
- Technician
- Team
- Region
- Area

Features:
- Drag and drop
- Resize
- Assign
- Reassign
- Reschedule
- Duplicate
- Cancel

Before save:
- Check availability
- Check skill
- Check conflict
- Check SLA
- Check travel time

---

# 36. DISPATCH BOARD

Kanban columns:

UNASSIGNED
SCHEDULED
EN_ROUTE
ARRIVED
IN_PROGRESS
WAITING
COMPLETED

Cards:
- WO Number
- Customer
- Job Type
- Technician
- Priority
- Schedule
- SLA
- Location

Support drag-and-drop.

---

# 37. TECHNICIAN DAILY DASHBOARD

Show:
- Today's jobs
- Completed
- Pending
- In Progress
- Next job
- Schedule
- Map
- Route
- Customer
- Address
- Phone
- Job type
- Priority
- SLA
- Checklist

Mobile-first.

Example:

Good Morning, Budi
AVAILABLE

8 Jobs
5 Completed
2 Pending
1 Active

Next:
10:30 ONU Replacement
CUS-000123

Buttons:
NAVIGATE
CALL
WHATSAPP
VIEW TOPOLOGY

---

# 38. DISPATCHER DASHBOARD

Metrics:
- Total Jobs
- Unassigned
- Scheduled
- In Progress
- SLA Risk
- SLA Breached
- Completed
- Failed

Technician availability:
AVAILABLE
BUSY
ON JOB
OFFLINE

Map:
- Technician
- Customer
- ODP
- ODC
- Incident
- Work Order

---

# 39. MANAGEMENT OPERATIONS DASHBOARD

Metrics:
- Jobs Today
- Completion Rate
- SLA Compliance
- Technician Utilization
- Average Resolution
- First Time Fix
- Repeat Visit
- Customer Rating
- Cost Per Job

Charts:
- Jobs Trend
- Jobs by Region
- Jobs by Technician
- Jobs by Job Type
- SLA Trend
- Completion Trend

---

# 40. WORK ORDER CHECKLIST

Checklist must be configurable per job type.

Example PSB Installation:

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

Each item:
PENDING
COMPLETED
FAILED
SKIPPED

Skipped/failed requires reason.

---

# 41. FIELD EVIDENCE

Technician can upload:
- Before photo
- During photo
- After photo
- ONU photo
- ODP photo
- Cable photo
- Splicing photo

Store metadata:
- latitude
- longitude
- timestamp
- technician_id
- work_order_id

---

# 42. GPS TRACKING

Technician mobile app can send:
- latitude
- longitude
- accuracy
- timestamp

Show:
- Current location
- Last location
- Job location
- Customer location

Only authorized roles can see technician locations.

---

# 43. ROUTE PLANNING

Optimize daily route considering:
- Distance
- Travel time
- SLA
- Priority
- Appointment

Example:

Technician
→ Customer A
→ Customer B
→ ODP
→ Customer C

Map provider must use adapter architecture.

---

# 44. CUSTOMER APPOINTMENT

Customer can select available slots.

Statuses:
REQUESTED
CONFIRMED
RESCHEDULED
CANCELLED
COMPLETED
NO_SHOW

Appointment is linked to Work Order.

---

# 45. SLA

Examples:

Critical: 2 hours
High: 4 hours
Normal: 24 hours
Low: 72 hours

States:
SAFE
WARNING
BREACHED

Automatic escalation:
- Warning
- Supervisor escalation
- SLA breached notification

---

# 46. MATERIAL MANAGEMENT

Work order can reserve and consume:
- ONU
- Drop Cable
- RJ45
- Patch Cord
- Adapter
- Splitter
- Fiber Closure
- Splice Sleeve
- Connector

Consumption updates inventory.

---

# 47. TOOL MANAGEMENT

Tools:
- OTDR
- Optical Power Meter
- Fusion Splicer
- VFL
- Laptop
- Crimping Tool

Statuses:
AVAILABLE
MISSING
DAMAGED

---

# 48. DIGITAL SIGNATURE

Customer signs after job completion.

Store:
- signature
- timestamp
- latitude
- longitude
- work_order_id

Generate completion report.

---

# 49. MOBILE TECHNICIAN APP

Bottom navigation:
Home
Jobs
Map
Notifications
Profile

Job screen:
- Customer
- Address
- Map
- Call
- WhatsApp
- Navigate
- Topology
- Checklist
- Photo
- Measurement
- Material
- Complete

---

# 50. OFFLINE MODE

Technician must be able to work with poor connectivity.

Offline:
- Job details
- Checklist
- Photos
- Notes
- Measurements

Sync when online.

Implement conflict resolution.

---

# 51. CUSTOMER PORTAL

Dashboard:
- Internet status
- Package
- IP
- Usage
- Invoice
- Payment
- ONU
- Ticket

Actions:
- Pay invoice
- Download invoice
- Create ticket
- View payment
- View usage

---

# 52. PARTNER PORTAL

Dashboard:
- Customers
- Active customers
- New PSB
- Installation
- Revenue
- Commission
- Outstanding invoice

Actions:
- Create customer
- Submit PSB
- Track installation
- View commission
- View invoices

Strict access isolation.

---

# 53. COMMISSION

Support:
- Percentage
- Fixed
- Tiered

Example:
1–50 = 5%
51–100 = 7%
100+ = 10%

Statuses:
PENDING
APPROVED
PAID
CANCELLED

---

# 54. NOTIFICATIONS

Channels:
- WhatsApp
- Email
- SMS
- In-App
- Push

Events:
- Invoice Created
- Invoice Reminder
- Payment Received
- Service Suspended
- Service Activated
- PSB Approved
- Technician Assigned
- Technician En Route
- Installation Scheduled
- Installation Completed
- Maintenance
- Incident
- Incident Resolved
- Work Order Rescheduled

Use provider adapters.

---

# 55. WHATSAPP

Create:

WhatsAppProviderInterface

Support future:
- Meta WhatsApp Cloud API
- Third-party provider

Templates:
- Invoice
- Payment
- Maintenance
- Incident
- PSB
- Technician Appointment
- Technician En Route
- Job Completed

---

# 56. IPAM

Support:
- IPv4
- IPv6
- Public
- Private
- CGNAT
- PPPoE
- DHCP
- Static
- Hotspot

Statuses:
AVAILABLE
ALLOCATED
RESERVED
BLOCKED
QUARANTINE

Support:
- Subnet
- Prefix
- Pool
- Allocation
- Release
- History

---

# 57. VLAN

Manage:
- VLAN ID
- Name
- Purpose
- Region
- POP
- OLT
- Service

Example:
VLAN 165 = STATIC
VLAN 144 = HOTSPOT
VLAN 100 = TR069

---

# 58. PROVISIONING

Customer activation:

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

Each step:
PENDING
RUNNING
SUCCESS
FAILED
RETRY

---

# 59. PROVISIONING ROLLBACK

If provisioning fails:
- Show failed step
- Retry
- Rollback
- Continue manually

Maintain provisioning logs.

---

# 60. SERVICE SUSPENSION

Overdue flow:

Invoice
→ Grace Period
→ Reminder
→ Suspension

Possible:
- RADIUS disable
- MikroTik disconnect
- Address removal
- Profile change

Payment flow:
Payment
→ Verify
→ Reactivate
→ Reconnect
→ Notify

---

# 61. FUP

Support:
- Monthly quota
- Usage
- Warning
- Speed reduction
- Reset

Example:
100 Mbps / 2 TB
80% warning
90% warning
100% reduce to 20 Mbps

---

# 62. REPORTING

Reports:
- Customer
- Revenue
- Invoice
- Payment
- Package
- Partner
- Commission
- ONU
- OLT
- PON
- ODC
- ODP
- Fiber
- Usage
- FUP
- Incident
- Ticket
- Installation
- Technician
- Work Order
- SLA

Export:
- CSV
- Excel
- PDF

---

# 63. DASHBOARD STRUCTURE

Create separate dashboards.

## ADMIN / MANAGEMENT
- Revenue
- Customers
- Active Services
- Outstanding Invoice
- Payment Today
- OLT
- ONU
- Network Availability
- Incidents
- Tickets
- Technician Operations

## NOC
- OLT
- PON
- ONU
- LOS
- RX
- Traffic
- Alarms
- Incidents
- Impacted Customers

## DISPATCHER
- Total Jobs
- Unassigned
- Scheduled
- En Route
- In Progress
- SLA Risk
- SLA Breached
- Completed
- Live Map
- Dispatch Board

## TECHNICIAN
- Today's Jobs
- Completed
- Pending
- Next Job
- Route
- Map
- SLA
- Checklist
- Notifications

## PARTNER
- Customers
- PSB
- Installation
- Revenue
- Commission
- Outstanding Invoice

## CUSTOMER
- Internet
- Package
- Usage
- Invoice
- Payment
- ONU
- Ticket

---

# 64. ADMIN DASHBOARD DESIGN

Premium enterprise SaaS.

Sidebar:

Dashboard

CRM
- Customers
- Leads
- Activities

Billing
- Invoices
- Payments
- Packages
- Subscriptions
- FUP

Network
- Dashboard
- OLT
- PON
- ONU
- MikroTik
- RADIUS
- IPAM
- VLAN
- Inventory

FTTH
- Topology
- ODC
- ODP
- Fiber
- Splitter
- Routes

NOC
- Live Monitor
- Alarms
- Incidents
- Impact

Operations
- PSB
- Survey
- Installation
- Work Orders
- Scheduling
- Dispatch
- Technician
- Maintenance
- Tickets

Partners
- Partners
- Customers
- Commission

Reports

Settings

Support:
- Light mode
- Dark mode
- Responsive layout

---

# 65. DISPATCH DASHBOARD DESIGN

Top KPIs:
- Total Jobs
- Unassigned
- SLA Risk
- SLA Breached
- Completed

Main area:

LEFT:
Dispatch Board

UNASSIGNED
SCHEDULED
EN_ROUTE
ARRIVED
IN_PROGRESS
WAITING
COMPLETED

RIGHT:
Live Map

Bottom:
- Technician utilization
- SLA chart
- Jobs by region

---

# 66. TECHNICIAN DASHBOARD DESIGN

Mobile-first.

Header:
Good Morning, Budi
AVAILABLE

KPIs:
8 Jobs
5 Completed
2 Pending
1 Active

Next job:
10:30
ONU Replacement
CUS-000123
ODP-PEJATEN-001
Port 08

Actions:
NAVIGATE
CALL
WHATSAPP
VIEW TOPOLOGY

Topology:
CUSTOMER
↓
ONU
↓
ODP
↓
ODC
↓
PON
↓
OLT

Checklist:
☑ Check ONU
☑ Check ODP
☐ Check RX
☐ Internet Test
☐ Upload Photo

Bottom:
Home
Jobs
Map
Notifications
Profile

---

# 67. CUSTOMER TOPOLOGY DRAWER

Example:

CUS-000123
Package: 100 Mbps
Service: PPPoE
IP: 10.x.x.x
ONU: ZTEG12345678
RX: -23.4 dBm
ODP: ODP-PEJATEN-001
Port: 08
ODC: ODC-PEJATEN-01
PON: 1/1/1
OLT: OLT-C600-PEJATEN-01
POP: POP-PEJATEN

Actions:
- Trace
- Open OLT
- Open ONU
- Open ODP
- Create Ticket
- Create Work Order

---

# 68. INCIDENT IMPACT DRAWER

Example:

PON 1/1/3 DOWN

Affected:
2 ODC
12 ODP
148 ONU
143 Customers
143 Services

Show estimated revenue impact.

Actions:
- View Customers
- Trace Topology
- Create Work Order
- Notify Customers

---

# 69. AUTOMATIC INCIDENT → WORK ORDER

If a network incident requires field intervention:

Incident
→ Topology Impact
→ Determine root node
→ Determine location
→ Determine required skill
→ Find nearest qualified technician
→ Check availability
→ Calculate SLA
→ Suggest technician
→ Suggest schedule
→ Dispatcher confirms
→ Assign Work Order
→ Notify technician

---

# 70. TICKET → WORK ORDER

When customer ticket requires field visit:

Create Work Order.

Show technician:
- Customer
- ONU
- RX
- TX
- OLT
- PON
- ODP
- ODC
- Last online
- Last offline
- Recent alarm
- Recent RADIUS session
- IP
- Package

---

# 71. WORK ORDER TIMELINE

Timeline:
- Created
- Assigned
- Scheduled
- Accepted
- En Route
- Arrived
- Started
- Checklist
- Provisioning
- Testing
- Completed

All changes must be audited.

---

# 72. DATABASE TABLES

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

---

# 73. API

Create REST API under /api/v1.

Core:
- /customers
- /subscriptions
- /packages
- /invoices
- /payments

Network:
- /radius
- /mikrotik
- /olts
- /pons
- /onus
- /odcs
- /odps
- /fibers
- /splitters

Topology:
- /topology
- /topology/trace
- /topology/impact

NOC:
- /alarms
- /incidents
- /tickets

Field:
- /technicians
- /work-orders
- /scheduler
- /dispatch

Portal:
- /partners
- /reports

Use:
- REST
- JSON
- API Resources
- Validation
- Rate limiting
- Authentication

---

# 74. REALTIME

Use Laravel Reverb.

Events:
- ONU Online
- ONU Offline
- LOS
- OLT Down
- PON Down
- Payment Received
- Invoice Paid
- Provisioning Completed
- Incident Created
- Incident Resolved
- Work Order Assigned
- Technician En Route
- Technician Arrived
- Work Order Completed

---

# 75. QUEUE

Use Redis + Horizon.

Jobs:
- SyncOLT
- SyncPON
- SyncONU
- PollSNMP
- PollMikrotik
- ProcessRadiusAccounting
- GenerateInvoices
- SendNotifications
- ProcessPaymentWebhook
- ProvisionCustomer
- SuspendCustomer
- ReactivateCustomer
- CalculateUsage
- DetectAlarm
- CalculateTopologyImpact
- ScheduleTechnician
- OptimizeTechnicianRoute
- SendSlaWarning

---

# 76. SCHEDULER

Every minute:
- Network health
- SLA monitoring

Every 5 minutes:
- ONU synchronization

Every 10 minutes:
- RADIUS accounting

Daily:
- Invoice reminder
- Usage processing

Monthly:
- Invoice generation
- FUP reset

---

# 77. SECURITY

Implement:
- CSRF
- XSS protection
- SQL injection protection
- Rate limiting
- RBAC
- 2FA
- Encrypted credentials
- Webhook signature verification
- API authentication
- Audit logs

Never store plaintext:
- OLT passwords
- MikroTik passwords
- RADIUS secrets
- Payment secrets
- API tokens

Sensitive commands require approval.

Examples:
- Delete ONU
- Reboot OLT
- Delete service port
- Mass disconnect
- VLAN change
- Factory reset

Workflow:
REQUEST
→ APPROVE
→ EXECUTE
→ VERIFY
→ AUDIT

---

# 78. OBSERVABILITY

Logs:
- Application
- Network
- OLT
- MikroTik
- RADIUS
- Payment
- Webhook
- Provisioning
- Topology
- Scheduling
- Work Order
- Audit

Never log credentials or secrets.

---

# 79. PERFORMANCE

Support:
- 100 customers
- 1,000 customers
- 10,000 customers
- 50,000+ customers

Use:
- Database indexes
- Pagination
- Server-side filtering
- Caching
- Redis
- Queue workers
- Lazy loading
- Virtualized tables

Avoid N+1 queries.

Do not load all ONU/topology data into browser.

Topology must lazy-load.

---

# 80. SEED DATA

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

Seed:
- 100+ customers
- 100+ ONUs
- 10+ technicians
- 3+ technician teams
- 30+ work orders
- realistic topology
- invoices
- payments
- tickets
- alarms
- incidents

---

# 81. DOCUMENTATION

Create:

README.md
ARCHITECTURE.md
DATABASE.md
ERD.md
API.md
DEPLOYMENT.md
SECURITY.md
TOPOLOGY.md
NETWORK.md
ZTE-OLT.md
MIKROTIK.md
RADIUS.md
PAYMENT.md
PROVISIONING.md
NOC.md
TECHNICIAN.md
SCHEDULING.md
WORK-ORDER.md
PARTNER.md
CUSTOMER-PORTAL.md
TASK.md
DESIGN.md

---

# 82. TASK.MD

Create detailed task tracking.

Statuses:
[ ] Not Started
[~] In Progress
[x] Completed

Sections:

Foundation
Authentication
RBAC
CRM
Billing
Payment
RADIUS
MikroTik
OLT
PON
ONU
IPAM
VLAN
ODC
ODP
Fiber
Topology
NOC
Monitoring
Alarm
Incident
Ticket
PSB
Technician
Work Order
Scheduling
Dispatch
Installation
Partner
Customer Portal
Notification
Reporting
Security
Testing
Deployment

Every task:
- ID
- Priority
- Description
- Dependencies
- Acceptance Criteria
- Status

---

# 83. DESIGN.MD

Create a complete design system.

Include:
- Design principles
- Color system
- Typography
- Spacing
- Layout
- Sidebar
- Topbar
- Dashboard
- Cards
- Tables
- Forms
- Drawer
- Modal
- Toast
- Timeline
- Calendar
- Map
- Topology
- Charts
- Status badges
- Mobile UI
- Dark mode

Design style:
- Premium
- Enterprise
- Modern
- Clean
- Professional
- NOC optimized
- Responsive

Do not create a generic template-looking dashboard.

---

# 84. ERD

Create ERD documentation.

Core:

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
→ Impact Analysis
→ Affected Customer
→ Work Order

---

# 85. TESTING

Create:
- Unit tests
- Feature tests
- Integration tests
- API tests
- Browser tests

Must test:
- Authentication
- RBAC
- Tenant isolation
- Customer
- Billing
- Payment
- Webhook
- RADIUS
- MikroTik
- ZTE
- ONU
- Topology
- Trace
- Impact
- Provisioning
- Incident
- Ticket
- Technician
- Scheduling
- Work Order
- PSB
- Partner
- Customer Portal

---

# 86. DISASTER RECOVERY

Support:
- PostgreSQL backup
- MikroTik backup
- OLT configuration backup
- Application backup

Document:
- Backup
- Restore
- Disaster Recovery

---

# 87. DEVOPS

Provide:
- Dockerfile
- docker-compose.yml
- .env.example
- Nginx configuration
- PHP-FPM
- Queue Worker
- Scheduler
- Horizon
- Reverb
- PostgreSQL
- Redis

Architecture:

Internet
↓
Nginx
↓
Laravel
↓
PostgreSQL
Redis
Horizon
Reverb

Network:

Laravel
↓
RADIUS
MikroTik
ZTE OLT
SNMP
SSH

---

# 88. DEVELOPMENT PHASES

PHASE 1
Foundation
- Laravel
- React
- PostgreSQL
- Redis
- Authentication
- RBAC

PHASE 2
CRM + Billing
- Customer
- Package
- Subscription
- Invoice
- Payment

PHASE 3
Network
- RADIUS
- MikroTik
- OLT
- PON
- ONU

PHASE 4
FTTH
- ODC
- ODP
- Fiber
- Splitter
- Topology
- Trace
- Impact

PHASE 5
NOC
- Monitoring
- Alarm
- Incident

PHASE 6
Field Operations
- Technician
- Work Order
- Checklist
- Evidence
- GPS
- Signature

PHASE 7
Scheduling
- Calendar
- Dispatch
- Availability
- SLA
- Route
- Auto assignment

PHASE 8
Portals
- Customer
- Partner
- Technician mobile

PHASE 9
Automation
- Provisioning
- Suspension
- Reactivation
- Notifications
- Incident automation

PHASE 10
Production
- Security
- Monitoring
- Backup
- Testing
- Deployment

---

# 89. CRITICAL BUSINESS FLOW

Example customer:

CUS-000123

Package:
100 Mbps

Service:
PPPoE

Invoice:
PAID

RADIUS:
ACTIVE

MikroTik:
ACTIVE

IP:
10.x.x.x

ONU:
ZTEG12345678

RX:
-23.4 dBm

ODP:
ODP-PEJATEN-001

Port:
08

ODC:
ODC-PEJATEN-01

PON:
1/1/1

OLT:
OLT-C600-PEJATEN-01

POP:
POP-PEJATEN

If customer reports "Internet mati":

Customer
→ Service
→ RADIUS
→ MikroTik
→ IP
→ ONU
→ ODP
→ ODC
→ PON
→ OLT

Check:
- Alarm
- ONU
- RX
- PON
- OLT
- RADIUS
- MikroTik

If field intervention is required:

Create Work Order
→ Find technician
→ Check skill
→ Check availability
→ Suggest schedule
→ Assign
→ Notify
→ En Route
→ Arrived
→ Repair
→ Checklist
→ Photo
→ Measurement
→ Test
→ Customer Signature
→ Complete
→ Resolve Ticket/Incident
→ Notify Customer

---

# 90. CRITICAL NETWORK INCIDENT FLOW

Example:

PON 1/1/3 DOWN

System:

PON DOWN
→ Topology Engine
→ Impact Analysis
→ 143 affected customers
→ Create Incident
→ Determine root cause
→ Create Work Order
→ Find qualified technician
→ Check area
→ Check schedule
→ Calculate distance
→ Calculate SLA
→ Rank technicians
→ Dispatcher confirms
→ Assign
→ Notify
→ Technician navigates
→ Repair
→ Verify RX/ONU
→ Complete
→ Incident Resolved
→ Customer Notification

---

# 91. ACCEPTANCE CRITERIA

The platform is complete when:

- Customer can be created
- Package can be created
- Subscription can be created
- Invoice can be generated
- Payment can be created
- Payment webhook works
- Invoice becomes PAID
- RADIUS account can be created
- MikroTik integration works
- ZTE OLT integration works
- ONU can be discovered
- ONU can be provisioned
- ONU can be assigned to ODP
- Customer can be linked to ONU
- Topology can be visualized
- Customer can trace to OLT
- OLT can trace to customers
- ODC can trace to customers
- ODP can trace to customers
- PON impact analysis works
- OLT impact analysis works
- ONU failure identifies customer
- PON failure identifies customers
- Incident can be created
- Work Order can be created
- Technician can be assigned
- Schedule conflicts are detected
- Technician can receive job
- Technician can start job
- Technician can upload evidence
- Technician can complete checklist
- Customer can sign
- Work Order can be completed
- Customer receives notification
- PSB can create Work Order
- Ticket can create Work Order
- Incident can create Work Order
- System can suggest technician
- System can suggest schedule
- SLA monitoring works
- Dispatcher dashboard works
- Technician dashboard works
- Management dashboard works
- Partner dashboard works
- Customer portal works
- Sensitive actions are audited
- Topology history is preserved
- Credentials are encrypted
- Payment webhook is idempotent
- Provisioning can retry
- Application can be deployed to production

---

# 92. FINAL PRINCIPLE

Do NOT build:
- only billing
- only CRM
- only NMS
- only topology
- only technician calendar

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
OLT
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
SCHEDULING
+
WORK ORDER
+
PARTNER
+
CUSTOMER

Everything must operate as one integrated system.

---

# 93. EXECUTION RULE

Before writing code:

1. Analyze requirements.
2. Create architecture.
3. Create module map.
4. Create database design.
5. Create ERD.
6. Create TASK.md.
7. Create DESIGN.md.
8. Create API specification.
9. Create integration interfaces.
10. Create migrations.
11. Create models.
12. Create services.
13. Create policies.
14. Create APIs.
15. Create frontend.
16. Create dashboards.
17. Create topology engine.
18. Create scheduling engine.
19. Create integrations.
20. Create tests.
21. Create seed data.
22. Run tests.
23. Fix errors.
24. Update documentation.

Do not skip foundational architecture.

Do not create fake production integrations.

If network equipment is unavailable during development, create proper adapter interfaces and mock implementations while keeping production adapters ready.

Do not stop after generating scaffolding. Continue until the current phase is functional, tested, documented and integrated.

When an implementation decision is ambiguous, choose the most maintainable, secure and scalable approach and document the decision.

============================================================
END OF MASTER PROMPT
============================================================
