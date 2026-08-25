# MASTER BUILD PROMPT
# PT MITRA MEDIA DATA
# ISP FTTH OSS/BSS + NMS + FIELD SERVICE PLATFORM
# UI/UX: SHADCN/UI — NOC COMMAND CENTER STYLE
# STACK: LARAVEL + GO + REACT + INERTIA + SHADCN/UI

============================================================
IMPORTANT — ROLE OF THE AI CODING AGENT
============================================================

You are the principal software architect, senior Laravel engineer,
senior Go network engineer, senior React/TypeScript engineer, database
architect, DevOps engineer, QA engineer and UI/UX designer.

You are responsible for DESIGNING, BUILDING, TESTING, DOCUMENTING and
FIXING the complete application.

Do not only generate scaffolding.

Do not only create a UI prototype.

Do not create fake CRUD screens without real backend integration.

Build functional end-to-end modules.

When a real network device is unavailable, create a proper adapter
interface and realistic simulator/mock. Never claim a real network
operation succeeded if it was not actually executed.

============================================================
0. DESIGN REFERENCE
============================================================

The uploaded/reference UI image is the PRIMARY visual reference.

The selected design direction is:

"NO. 2 — NOC COMMAND CENTER / ENTERPRISE ISP DASHBOARD"

Use the visual language of the reference:

- dark premium enterprise interface
- compact but readable information density
- left sidebar navigation
- top global search
- command palette
- realtime status indicator
- KPI cards
- network health panels
- network topology overview
- active alarms
- charts
- operational tables
- technician status
- clean borders
- subtle shadows
- small/medium radius
- minimal visual noise
- professional typography
- green/blue/purple/orange/red semantic status accents

IMPORTANT:

Do NOT copy the reference image literally.

Use it as a design language and layout inspiration.

The final product must be an original PT Mitra Media Data interface.

Brand:

PT Mitra Media Data

Product subtitle:

ISP & FTTH Operations Platform

Do NOT use:
"PT Susu Teknologi Indonesia"
in the application.

============================================================
1. PRODUCT VISION
============================================================

Build a unified ISP FTTH Operations Platform for:

PT Mitra Media Data

The platform combines:

OSS
BSS
CRM
Billing
Payment Gateway
RADIUS
MikroTik Management
ZTE OLT Management
PON Management
ONU Management
IPAM
VLAN
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
Inventory
Partner Portal
Customer Portal
Reporting
Realtime Operations

The application must feel like ONE unified ISP operating system.

It must NOT look like several separate admin templates glued together.

============================================================
2. PRIMARY DESIGN GOAL
============================================================

The application must feel like:

Cloud/enterprise dashboard
+
ISP NOC
+
FTTH OSS/BSS
+
Field Service Management

Visual characteristics:

- dark-first
- professional
- dense information
- clean spacing
- subtle borders
- restrained shadows
- clear hierarchy
- minimal gradients
- semantic colors
- high-quality tables
- realtime indicators
- responsive
- accessible

Avoid:

- excessive rounded cards
- oversized typography
- excessive gradients
- colorful backgrounds everywhere
- generic SaaS template appearance
- Bootstrap-like UI
- old-fashioned NOC UI
- unnecessary animations

============================================================
3. FRONTEND STACK
============================================================

MANDATORY:

React
TypeScript
Inertia.js
Tailwind CSS
shadcn/ui

Additional libraries:

TanStack Table
React Hook Form
Zod
Lucide React
React Flow
Recharts / shadcn chart
FullCalendar
MapLibre or Leaflet

Do NOT use TailAdmin.

Do NOT use Bootstrap.

Do NOT introduce another complete UI component library.

shadcn/ui MUST be the primary design system.

============================================================
4. BACKEND STACK
============================================================

Business backend:

Laravel 12
PHP 8.3+

Network backend:

Go
current stable version available at implementation time

Database:

PostgreSQL 16+
PostGIS

Cache/Event:

Redis

Realtime:

Laravel Reverb / WebSocket

Queues:

Laravel Horizon + Redis

Infrastructure:

Docker
Docker Compose
Nginx

============================================================
5. HYBRID ARCHITECTURE
============================================================

                    INTERNET
                        |
                      NGINX
                        |
              +---------+---------+
              |                   |
              v                   v
          LARAVEL                GO
          OSS/BSS          NETWORK ENGINE
              |                   |
              |                   +-- ZTE OLT
              |                   +-- MikroTik
              |                   +-- SNMP
              |                   +-- SSH
              |                   +-- ICMP
              |                   +-- RADIUS
              |                   +-- Polling
              |                   +-- Network Events
              |                   +-- Provisioning
              |
              +---------+---------+
                        |
                      REDIS
                        |
                 EVENT / QUEUE
                        |
                    WEBSOCKET
                        |
                      REACT

Laravel owns business rules.

Go owns network operations.

Go must not bypass Laravel business rules for billing/customer logic.

============================================================
6. REPOSITORY STRUCTURE
============================================================

Use a monorepo:

isp-platform/

apps/
  api/
  web/
  network-engine/

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
ARCHITECTURE.md
NETWORK.md
ZTE-OLT.md
MIKROTIK.md
RADIUS.md
TOPOLOGY.md
NOC.md
TECHNICIAN.md
SCHEDULING.md
WORK-ORDER.md
PROVISIONING.md
SECURITY.md
DEPLOYMENT.md

============================================================
7. UI DESIGN SYSTEM — SHADCN/UI
============================================================

The entire frontend MUST use shadcn/ui.

Required components where appropriate:

Button
Card
Badge
Alert
Avatar
Breadcrumb
Calendar
Checkbox
Command
Dialog
Drawer
DropdownMenu
Form
Input
Label
Popover
Progress
RadioGroup
ScrollArea
Select
Sheet
Sidebar
Skeleton
Switch
Table
Tabs
Textarea
Toast
Tooltip
Pagination
NavigationMenu
Separator
Collapsible
Accordion
ContextMenu
HoverCard
Menubar

Use shadcn CSS variables.

Do not hard-code colors into individual components.

Create semantic design tokens.

Example:

--background
--foreground
--card
--card-foreground
--popover
--primary
--primary-foreground
--secondary
--muted
--muted-foreground
--accent
--destructive
--border
--input
--ring

Additional semantic status tokens:

--status-online
--status-warning
--status-critical
--status-info
--status-unknown
--status-success

============================================================
8. BRAND
============================================================

Brand:

PT Mitra Media Data

Subtitle:

ISP & FTTH Operations Platform

Use a professional network/technology logo treatment.

Do not use the old company name.

Sidebar header:

PT Mitra Media Data
ISP & FTTH Operations Platform

Browser title examples:

PT Mitra Media Data — Dashboard
PT Mitra Media Data — NOC
PT Mitra Media Data — OLT
PT Mitra Media Data — Customers

============================================================
9. GLOBAL LAYOUT
============================================================

Desktop layout:

┌─────────────────────────────────────────────────────────────┐
│ Sidebar │ Topbar                                             │
│         ├────────────────────────────────────────────────────┤
│         │ Page Header                                        │
│         │                                                     │
│         │ Content                                             │
│         │                                                     │
└─────────┴────────────────────────────────────────────────────┘

Sidebar:

240–260px

Collapsible:

icon-only mode

Topbar:

- mobile menu
- command/search
- notifications
- realtime indicator
- theme switch
- settings
- user profile

Content should use responsive containers.

============================================================
10. SIDEBAR INFORMATION ARCHITECTURE
============================================================

MAIN

Dashboard
NOC Command Center

BUSINESS

Customers
Subscriptions
Packages
Partners

BILLING

Invoices
Payments
FUP Management

NETWORK

OLT Management
PON Management
ONU Management
MikroTik Routers
RADIUS Servers
IPAM & VLAN

TOPOLOGY

Network Map
ODC Management
ODP Management
Fiber Management
Splitters
Splice / Joint Closure

OPERATIONS

Incidents
Tickets
PSB / New Order
Work Orders
Dispatch Center

FIELD SERVICE

Technicians
Teams
Schedules
Inventory
Tools

REPORTS

Revenue
Customers
Network
Technicians
Operations
Financial

SYSTEM

Users
Roles & Permissions
Notifications
Integrations
Audit Logs
System Settings

Sidebar badges:

Incidents 3
Tickets 12
Critical Alarms 3

============================================================
11. GLOBAL SEARCH
============================================================

Use shadcn Command.

Keyboard:

Ctrl/Cmd + K

Search:

customer
customer ID
phone
ONU serial
ONU MAC
OLT
PON
ODP
ODC
IP address
PPPoE username
invoice
ticket
incident
work order
technician

Quick actions:

New Customer
New Ticket
New Work Order
Generate Invoice
Open NOC
Open Topology
Add OLT
Discover ONU

============================================================
12. REALTIME INDICATOR
============================================================

Always show:

● LIVE

When disconnected:

● REALTIME DISCONNECTED

Tooltip:

"Realtime connection lost. Reconnecting..."

Automatic reconnect:

exponential backoff

After reconnect:

resync current state
reconcile missed events
remove stale state

Never silently show stale network data.

============================================================
13. DASHBOARD
============================================================

Create a dashboard closely inspired by the selected reference style.

Header:

Dashboard

Subtitle:

Overview of your network, customers and operations

Actions:

Date Range
Download

KPI cards:

Total Customers
Active Subscriptions
Total Revenue
Pending Invoices
Open Tickets
Work Orders

Each card:

title
value
percentage change
trend
small sparkline
icon

Use shadcn Card.

Example:

Total Customers
12,842
↑ 8.45% from last month

Active Subscriptions
12,401
↑ 7.12%

Total Revenue
Rp 284.5M
↑ 21.6%

Pending Invoices
1,234

Open Tickets
48

Work Orders
21

============================================================
14. DASHBOARD GRID
============================================================

Row 1:

6 KPI cards

Row 2:

Network Health
Network Topology Overview
Active Alarms

Row 3:

Revenue Overview
Top Customers by Usage
Technicians On Duty

Optional:

Recent Payments
Recent Tickets
Recent Work Orders
Customer Growth

The grid must be responsive.

Desktop:
12-column grid

Tablet:
6-column behavior

Mobile:
single column

============================================================
15. NETWORK HEALTH CARD
============================================================

Show:

OLT
PON
ONU
RADIUS
MikroTik

Example:

OLT       98.7%
PON       99.1%
ONU       98.4%
RADIUS    99.9%
MikroTik  99.2%

Use:

icon
label
progress bar
percentage
status

Clicking a row opens relevant management page.

============================================================
16. NETWORK TOPOLOGY OVERVIEW
============================================================

Use React Flow.

Show:

POP
OLT
PON
ODC
ODP
ONU

Example:

POP
↓
OLT
↓
PON
↓
ODC
↓
ODP
↓
ONU

Nodes show:

name
status
count
critical state

Realtime node state.

Buttons:

View Topology
Trace
Impact

============================================================
17. ACTIVE ALARMS
============================================================

Use shadcn Card + ScrollArea.

Alarm row:

severity indicator
alarm title
device
location
time
severity badge

Examples:

PON DOWN
OLT-PEJATEN-01 / PON 1/1/3
CRITICAL

ONU LOW RX
ODP-001 / ONU-028
WARNING

ONU OFFLINE
ODP-002 / ONU-015
WARNING

HIGH TEMPERATURE
OLT-PEJATEN-02
INFO

RADIUS AUTH FAILED
RADIUS-01
INFO

Click alarm:

open Sheet

Actions:

Acknowledge
Open Incident
View Topology
View Customers
Create Work Order

============================================================
18. REVENUE OVERVIEW
============================================================

Use shadcn chart.

Show:

monthly revenue
paid
pending
overdue

Controls:

This Month
Last Month
This Year
Custom Range

Currency:

IDR

============================================================
19. TOP CUSTOMERS BY USAGE
============================================================

DataTable:

Customer
Package
Usage
Status

Example:

PT. Mitra Data
100 Mbps
4.21 TB
Active

Use shadcn Table + TanStack Table.

============================================================
20. TECHNICIANS ON DUTY
============================================================

Show:

avatar
name
area
status
current job

Statuses:

En Route
On Job
Available
Offline

Click technician:

open Sheet with:
current location
today jobs
performance
SLA
route

============================================================
21. NOC COMMAND CENTER
============================================================

Create dedicated NOC page.

Top KPI:

OLT
PON
ONU
Critical
Affected Customers

Example:

OLT 98.7%
PON 99.1%
ONU 98.4%
Critical 3
Affected 143

Main area:

Network Map
Alarm Feed
Incident Summary
FTTH Topology

Tabs:

Network
Topology
Alarms
Incidents

============================================================
22. NOC NETWORK MAP
============================================================

Use MapLibre or Leaflet.

Map shows:

POP
OLT
ODC
ODP
Technician
Incidents

Marker colors:

green online
red critical
orange warning
blue technician

Clustering for many devices.

Click marker:

Sheet details.

============================================================
23. NOC INCIDENT SUMMARY
============================================================

Donut chart:

Critical
Major
Minor
Info

Show total incidents.

Click segment:

filter incident list.

============================================================
24. FTTH TOPOLOGY PAGE
============================================================

Use React Flow.

Toolbar:

Search node
Filter OLT
Filter status
Trace
Impact Analysis
Fit View
Zoom
Fullscreen

Node hierarchy:

POP
→ OLT
→ PON
→ ODC
→ Fiber
→ ODP
→ ODP Port
→ ONU
→ Customer

Node click opens Sheet.

============================================================
25. TOPOLOGY TRACE
============================================================

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

Highlight path visually.

Show:

status
distance
optical power
fiber core
affected services

============================================================
26. IMPACT ANALYSIS
============================================================

OLT DOWN:

calculate:

PON
ODC
ODP
ONU
Customer
Services
Revenue impact

PON DOWN:

calculate:

ODC
ODP
ONU
Customer

ODP DOWN:

calculate:

ONU
Customer

ONU DOWN:

calculate:

Customer

Use an Impact Analysis Sheet/Dialog.

============================================================
27. OLT MANAGEMENT UI
============================================================

Page:

OLT Management

Header actions:

+ Add OLT
Discover
Sync All
Export

Filters:

Vendor
Model
Region
POP
Status

Table:

OLT Name
Model
Management IP
POP
PON
ONU
Status
Uptime
Actions

Actions:

View
Edit
Sync
Test Connection
Topology
Alarms

OLT Detail page:

Overview
Boards
PON
ONU
Alarms
Metrics
Configuration
Topology
Audit

============================================================
28. PON MANAGEMENT UI
============================================================

Table:

OLT
Slot
Port
PON
ONU Count
Online
Offline
Average RX
Status

Detail:

PON health
ONU list
optical metrics
alarms
topology
affected customers

============================================================
29. ONU MANAGEMENT UI
============================================================

Use high-density shadcn DataTable.

Columns:

Serial
Customer
OLT
PON
ODC
ODP
RX
TX
Distance
Status
Last Seen

Filters:

OLT
PON
ODC
ODP
Status
RX
LOS
Customer

Bulk actions must be permission-protected.

ONU detail Sheet:

Serial
MAC
Customer
Package
OLT
PON
ODC
ODP
RX
TX
Temperature
Distance
Last Seen
Status

Actions:

Trace
Customer
Work Order
Provision
Disable
Delete

Sensitive operations require confirmation and audit.

============================================================
30. CUSTOMER MANAGEMENT UI
============================================================

Customers page:

search
filters
status tabs
export
+ New Customer

Table:

Customer ID
Name
Phone
Package
Service
ONU
ODP
Status
Billing
Actions

Customer detail:

Overview
Subscription
Billing
Payments
Network
Topology
ONU
IP
RADIUS
Tickets
Incidents
Work Orders
Documents
Activity

============================================================
31. CUSTOMER 360
============================================================

The Customer 360 page must be one of the strongest pages.

Header:

Customer name
Customer ID
status
service status

Cards:

Internet
Package
IP
Invoice
ONU

Network chain:

OLT
↓
PON
↓
ODC
↓
ODP
↓
ONU

Show:

RX
TX
Distance
Last Online
Last Offline

Diagnostics:

Service
RADIUS
PPPoE
MikroTik
ONU
Optical
PON
OLT
Topology

============================================================
32. SUBSCRIPTION UI
============================================================

Support:

STATIC
DHCP
PPPOE
HOTSPOT

Fields:

customer
package
service type
username
password
static IP
IPv6 prefix
VLAN
RADIUS profile
MikroTik profile
activation date
billing date
due date
status

============================================================
33. BILLING DASHBOARD
============================================================

KPI:

Total Revenue
Paid
Pending
Overdue
Refunded

Charts:

Revenue
Payment
Overdue

Table:

Invoice
Customer
Amount
Due Date
Status
Payment

Use:

Paid
Pending
Overdue
Cancelled

semantic badges.

============================================================
34. INVOICE PAGE
============================================================

Header:

Invoices

Actions:

+ Generate Invoice
Export

Filters:

Status
Customer
Date
Package
Payment

Invoice detail:

Invoice number
Customer
Items
Subtotal
Tax
Discount
Total
Payment status
Payment history

Actions:

Pay
Send
Download PDF
Cancel
Refund where authorized

============================================================
35. PAYMENT GATEWAY UI
============================================================

Dashboard:

Today Revenue
Successful
Pending
Failed
Refunded

Payment methods:

QRIS
Virtual Account
Bank Transfer
E-wallet
Card

Provider:

Midtrans
Xendit

Show:

gateway
transaction ID
invoice
amount
status
timestamp

Webhook logs page.

============================================================
36. RADIUS UI
============================================================

RADIUS dashboard:

Servers
Online
Sessions
Auth Success
Auth Failed
Accounting

Pages:

RADIUS Servers
Users
Sessions
Accounting
Logs

Show:

PPPoE sessions
Hotspot sessions
NAS
IP
start
stop
duration
traffic

============================================================
37. MIKROTIK UI
============================================================

MikroTik Management:

Device list
status
model
RouterOS
IP
uptime
CPU
memory

Detail:

Interfaces
VLAN
Routes
ARP
DHCP
PPPoE
Hotspot
Queues
Backups
Health

Sensitive operations require permissions.

============================================================
38. IPAM UI
============================================================

Dashboard:

IPv4 utilization
IPv6 utilization
Available
Allocated
Reserved
Blocked

Pages:

Pools
Subnets
IP Addresses
Allocations
History

Support:

STATIC
DHCP
PPPOE
HOTSPOT
CGNAT
IPv6

============================================================
39. VLAN UI
============================================================

Manage:

VLAN ID
Name
Purpose
Region
POP
OLT
Service

Example:

165 STATIC
144 HOTSPOT
100 TR069

============================================================
40. ODC MANAGEMENT
============================================================

Dashboard:

Total ODC
Capacity
Used Core
Available Core
Damaged

Table:

ODC
Region
Capacity
Used
Available
Status

Detail:

ODC
Fiber cores
Connected ODP
Topology
Map
Customers
Maintenance

============================================================
41. ODP MANAGEMENT
============================================================

Table:

ODP
ODC
Capacity
Used Ports
Available Ports
Status

Detail:

ODP
Map
Ports
Customers
ONU
Topology
Work Orders

Port visualization:

1 AVAILABLE
2 USED
3 USED
4 AVAILABLE
5 RESERVED
6 DAMAGED

Use visual port grid.

============================================================
42. FIBER MANAGEMENT
============================================================

Manage:

Fiber Cable
Fiber Core
Splice
Joint Closure
Splitter

Show map and topology.

Fiber core statuses:

AVAILABLE
RESERVED
CONNECTED
DAMAGED

============================================================
43. TICKET UI
============================================================

Ticket dashboard:

Open
Assigned
In Progress
Waiting
Resolved
Closed

Table:

Ticket
Customer
Subject
Priority
Technician
SLA
Status

Ticket detail timeline:

Customer complaint
CS response
Network diagnostics
Technician assignment
Work order
Resolution

============================================================
44. INCIDENT UI
============================================================

Incident list.

Severity:

Critical
Major
Minor
Info

Incident detail:

Root cause
Affected OLT
PON
ODC
ODP
ONU
Customers
Revenue impact
Timeline
Work Order

Actions:

Acknowledge
Assign
Create Work Order
Notify Customers
Resolve

============================================================
45. PSB / NEW ORDER UI
============================================================

PSB pipeline:

Lead
Survey
Approved
Scheduled
Installation
Test
Activation
Completed

Kanban or stepper.

PSB detail:

Customer
Location
Coverage
ODP
Port
Distance
Drop Cable
RX Prediction
Technician
Schedule
Photos
Notes

============================================================
46. TECHNICIAN UI
============================================================

Desktop technician dashboard:

Today's Jobs
Completed
Remaining
Urgent
SLA Risk

List:

Job
Customer
Location
Schedule
Priority
Status

Technician detail:

profile
skills
availability
current location
today route
jobs
performance
SLA

============================================================
47. TECHNICIAN MOBILE UI
============================================================

Mobile-first.

Bottom navigation:

Home
Jobs
Map
Notifications
Profile

Job detail:

Customer
Address
Navigate
Topology
Checklist
Photos
Measurements
Materials
Signature
Complete

Offline support.

============================================================
48. WORK ORDER UI
============================================================

Work Order dashboard:

Pending
Scheduled
Assigned
En Route
Arrived
In Progress
Waiting
Completed
Failed

Use shadcn DataTable and Kanban.

Work Order detail:

customer
job type
technician
schedule
SLA
location
topology
checklist
materials
tools
photos
measurements
comments
signature
timeline

============================================================
49. DISPATCH CENTER
============================================================

This page must look like a professional field operations command center.

Layout:

Left:
unassigned work orders

Center:
live map

Right:
technicians

Bottom:
technician schedule timeline

Statuses:

Unassigned
Scheduled
En Route
Arrived
In Progress
Waiting
Completed

Drag-and-drop assignment.

Before assignment:

show recommended technician.

Ranking:

skill
availability
distance
workload
SLA
region

============================================================
50. SCHEDULING UI
============================================================

Use FullCalendar.

Views:

Month
Week
Day
Timeline

Technician lanes.

Show:

work order
customer
priority
SLA
duration

Detect conflicts.

Display conflict dialog.

============================================================
51. PARTNER DASHBOARD
============================================================

Show:

Customers
Active
PSB
Installations
Revenue
Commission
Outstanding

Partner actions:

New Customer
New PSB
Track Installation
Commission

============================================================
52. CUSTOMER PORTAL
============================================================

Customer portal must be much simpler.

Dashboard:

Internet Status
Package
Usage
Invoice
Payment
ONU
Ticket

Primary action:

Bayar Sekarang

Show:

ONLINE
OFFLINE
SUSPENDED

Use mobile-first shadcn components.

============================================================
53. REPORTING UI
============================================================

Reports:

Customers
Revenue
Invoices
Payments
Packages
Network
OLT
PON
ONU
ODC
ODP
Fiber
Incidents
Tickets
Technicians
Work Orders
SLA

Filters:

date
region
area
POP
OLT
package

Export:

CSV
Excel
PDF

============================================================
54. SETTINGS UI
============================================================

Settings:

Company
Users
Roles
Permissions
Notification
Payment Gateway
RADIUS
MikroTik
ZTE
WebSocket
Email
WhatsApp
SMS
Storage
Backup
Audit

Use tabs and nested settings.

============================================================
55. AUTH UI
============================================================

Login:

dark premium.

Brand:

PT Mitra Media Data

Subtitle:

ISP & FTTH Operations Platform

Fields:

Email
Password

Actions:

Login
Forgot Password
2FA

Use shadcn Card/Form/Input/Button.

============================================================
56. NOTIFICATIONS
============================================================

Notification center:

Unread
All

Events:

Payment received
Invoice overdue
OLT down
PON down
ONU LOS
Ticket assigned
Work Order assigned
Technician en route
PSB approved
Incident created
Incident resolved

Realtime notification badge.

============================================================
57. RESPONSIVE DESIGN
============================================================

Desktop:
NOC/Management optimized

Tablet:
adaptive grid

Mobile:
customer and technician optimized

Sidebar:
desktop sidebar
mobile drawer

Tables:
horizontal scroll or responsive card mode where appropriate.

Never make desktop UI simply shrink on mobile.

============================================================
58. ACCESSIBILITY
============================================================

Use:
keyboard navigation
focus states
ARIA
semantic HTML
screen reader labels
accessible dialogs
accessible forms

Do not rely only on color.

Example:

Online:
green dot + "Online"

Critical:
red dot + "Critical"

============================================================
59. ANIMATION
============================================================

Use subtle animation only.

Allowed:
fade
slide
hover
skeleton
progress
status transition

Do not over-animate.

Network realtime updates should be subtle.

============================================================
60. BUSINESS MODULES
============================================================

Implement fully:

Customer
CRM
Package
Subscription
Billing
Invoice
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
Splitter
Topology
NOC
Alarm
Incident
Ticket
PSB
Technician
Work Order
Scheduling
Dispatch
Inventory
Partner
Customer Portal
Notification
Reports
Audit

============================================================
61. NETWORK SERVICE TYPES
============================================================

Support:

STATIC
DHCP
PPPOE
HOTSPOT

RADIUS for:

PPPoE
Hotspot

MikroTik integration for:

PPPoE
Hotspot
DHCP
Static
Queue
Address
VLAN

============================================================
62. ZTE OLT
============================================================

Support:

ZTE C300
ZTE C320
ZTE C600

Communication:

SSH
SNMP

Operations:

connect
test
discover
sync
ONU discovery
ONU authorization
ONU delete
optical power
distance
temperature
MAC
VLAN
service ports
TCONT
GEM
DBA
line profile
service profile

Vendor CLI must exist only in Go adapter.

============================================================
63. MIKROTIK
============================================================

Support:

RouterOS API
REST
SSH fallback

Operations:

connection
identity
interfaces
VLAN
routes
ARP
DHCP
PPPoE
Hotspot
queues
disconnect
enable/disable
backup

============================================================
64. GO NETWORK ENGINE
============================================================

Create adapter interfaces:

OltAdapter
MikrotikAdapter
RadiusAdapter
SnmpAdapter

Use worker pools.

Use:
timeouts
retries
backoff
circuit breakers
rate limiting
metrics
structured logs

Do not create unlimited goroutines.

============================================================
65. REALTIME
============================================================

Network:

ZTE/MikroTik/SNMP
→ Go collector
→ event
→ Redis
→ Laravel
→ WebSocket
→ React

Realtime:

OLT status
PON status
ONU status
LOS
RX
alarms
incidents
technician
work order
payment
provisioning

============================================================
66. PROVISIONING
============================================================

Flow:

Customer
→ Subscription
→ IP
→ RADIUS
→ MikroTik
→ OLT
→ ONU
→ ODP
→ Verify
→ Activate

Each step:

PENDING
RUNNING
SUCCESS
FAILED
RETRY

Support rollback.

============================================================
67. BILLING + PAYMENT
============================================================

Payment adapters:

Midtrans
Xendit

Webhook:

signature verification
idempotency
retry
audit

Invoice:

DRAFT
PENDING
PARTIAL
PAID
OVERDUE
CANCELLED
REFUNDED

============================================================
68. DATABASE
============================================================

Create proper migrations for:

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
69. SECURITY
============================================================

Implement:

RBAC
2FA
CSRF
XSS protection
SQL injection protection
rate limiting
encrypted credentials
secure headers
API authentication
webhook verification
audit logs

Encrypt:

OLT passwords
MikroTik passwords
RADIUS secrets
API keys
payment secrets
SSH private keys

Never log secrets.

Sensitive network commands require authorization.

============================================================
70. OBSERVABILITY
============================================================

Go:

/health
/ready
/metrics

Metrics:

polling duration
polling success
polling failure
device count
worker count
queue depth
event latency
OLT availability
ONU state
SNMP errors
SSH errors
API errors

============================================================
71. TESTING
============================================================

Create:

Laravel unit tests
feature tests
API tests
browser tests
Go unit tests
Go integration tests
network adapter tests
contract tests
realtime tests
load tests

Test:

authentication
RBAC
tenant isolation
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
PSB
technician
scheduling
work order
partner
customer portal
realtime reconnect
event idempotency

============================================================
72. SEED DATA
============================================================

Company:

PT Mitra Media Data

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

100+ customers
100+ ONUs
10+ technicians
3+ teams
30+ work orders
realistic topology
invoices
payments
tickets
alarms
incidents

============================================================
73. TASK.MD
============================================================

Create detailed task backlog.

Format:

[ ] Not Started
[~] In Progress
[x] Completed

Each task:

ID
Priority
Description
Dependencies
Acceptance Criteria
Status

Phases:

P01 Foundation
P02 Design System
P03 Authentication
P04 RBAC
P05 CRM
P06 Customers
P07 Packages
P08 Subscriptions
P09 Billing
P10 Payment
P11 RADIUS
P12 MikroTik
P13 Go Network Engine
P14 ZTE OLT
P15 PON
P16 ONU
P17 IPAM
P18 VLAN
P19 ODC
P20 ODP
P21 Fiber
P22 Topology
P23 NOC
P24 Monitoring
P25 Alarm
P26 Incident
P27 Ticket
P28 PSB
P29 Technician
P30 Work Order
P31 Scheduling
P32 Dispatch
P33 Inventory
P34 Partner
P35 Customer Portal
P36 Notification
P37 Realtime
P38 Reports
P39 Security
P40 Testing
P41 Deployment

============================================================
74. DESIGN.MD
============================================================

Create DESIGN.md documenting:

brand
logo
color tokens
dark mode
light mode
typography
spacing
border radius
sidebar
topbar
cards
tables
forms
dialogs
sheets
drawers
badges
alerts
charts
maps
topology
calendar
mobile
accessibility
animation
realtime states

The reference image should be explicitly documented as the design
direction.

============================================================
75. ACCEPTANCE CRITERIA
============================================================

The platform is accepted when:

Customer creation works.
Subscription works.
Billing works.
Payment gateway works.
Webhook works.
RADIUS works.
MikroTik integration works.
ZTE integration works.
ONU discovery works.
ONU provisioning works.
ODP assignment works.
Topology works.
Trace works.
Impact analysis works.
NOC works.
Realtime works.
Alarm correlation works.
Incident works.
Ticket works.
PSB works.
Technician works.
Scheduling works.
Dispatch works.
Work Order works.
Customer portal works.
Partner portal works.
Reports work.
RBAC works.
Audit works.
Credentials are encrypted.
Provisioning retry works.
Provisioning rollback works.
WebSocket reconnect works.
Docker deployment works.

============================================================
76. DEVELOPMENT EXECUTION RULE
============================================================

Before coding:

1. Inspect repository.
2. Inspect existing files.
3. Inspect the provided/reference design image.
4. Create architecture.
5. Create module map.
6. Create ERD.
7. Create TASK.md.
8. Create DESIGN.md.
9. Create API.md.
10. Create documentation skeleton.

Then implement in phases.

For every phase:

1. implement
2. test
3. lint
4. build
5. fix errors
6. update TASK.md
7. update documentation

Do not skip tests.

Do not mark incomplete work as completed.

Do not create fake API responses.

Do not create fake network success.

Do not build only the frontend.

Do not build only the backend.

Build end-to-end.

============================================================
77. FINAL DESIGN RULE
============================================================

The selected UI direction is:

SHADCN/UI
+
DARK ENTERPRISE
+
NOC COMMAND CENTER
+
ISP OSS/BSS

The reference image establishes:

- overall density
- sidebar behavior
- card proportions
- typography hierarchy
- dark background
- subtle borders
- chart treatment
- table treatment
- status badges
- spacing
- visual hierarchy

Create an original design for:

PT Mitra Media Data

The result should look like a professional commercial ISP operations
platform, not a generic admin dashboard.

============================================================
78. FINAL PRODUCT
============================================================

Build:

PT MITRA MEDIA DATA
ISP & FTTH OPERATIONS PLATFORM

One platform for:

Customers
Billing
Payments
RADIUS
MikroTik
ZTE OLT
PON
ONU
IPAM
VLAN
ODC
ODP
Fiber
Topology
NOC
Alarms
Incidents
Tickets
PSB
Technicians
Work Orders
Scheduling
Dispatch
Inventory
Partners
Customer Portal
Reports
Realtime Operations

============================================================


============================================================
OLT INTEGRATION — MANDATORY IMPLEMENTATION STANDARD
============================================================

IMPORTANT:

For ZTE OLT monitoring/integration, DO NOT implement a new custom
SNMP engine from scratch for the supported monitoring capabilities.

Use the official/reference project:

https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte

Required release:

v3.2.0

GitHub release:
https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte/releases/tag/v3.2.0

Go module:

github.com/Cepat-Kilat-Teknologi/snmp-olt-zte@v3.2.0

The project is the canonical ZTE C320/C300 SNMP monitoring adapter
for this application.

Reference capabilities of v3.2.0 include:

- ZTE C320 support
- ZTE C300 support
- multi-OLT in one instance
- per-OLT SNMP configuration
- per-tenant API key access control
- Redis cache namespacing
- per-OLT API paths
- per-slot PON counts
- slot-parametric OID generation
- uplink/card auto-detection
- ENTITY-MIB card detection
- IF-MIB uplink detection
- SNMP connection pooling
- bounded SNMP concurrency
- Redis caching
- cache pre-warming
- singleflight request deduplication
- batched SNMP GET
- BulkWalk
- Prometheus metrics
- structured logging
- SNMP Trap support for ONU offline detection
- RX power monitoring
- configurable RX thresholds
- OpenAPI specification
- health/readiness endpoints
- load testing with k6

The implementation MUST pin and document v3.2.0.

Do not silently upgrade to another version.

If a newer release is considered, create a documented compatibility
assessment first and do not change the required version automatically.

============================================================
OLT SERVICE ARCHITECTURE
============================================================

Use:

                    Laravel
                       |
                  OLT Service
                       |
                Internal HTTP API
                       |
                       v
              snmp-olt-zte v3.2.0
                       |
                    SNMP
                       |
                ZTE C320 / C300
                       |
                    Redis

The Laravel application owns:

- OLT records
- tenant ownership
- authorization
- UI
- business metadata
- topology relationships
- customer relationships
- audit
- work orders
- incidents
- permissions

snmp-olt-zte owns the ZTE SNMP monitoring/collection layer.

Do not duplicate the ZTE SNMP OID implementation in Laravel.

The existing Go network-engine architecture may act as an integration
or orchestration layer around snmp-olt-zte, but MUST NOT unnecessarily
reimplement its C320/C300 SNMP logic.

Prefer composition:

network-engine
    |
    +-- snmp-olt-zte v3.2.0
    |
    +-- MikroTik adapter
    |
    +-- RADIUS adapter
    |
    +-- other network adapters

============================================================
ZTE OLT REGISTRY
============================================================

Laravel database must maintain an OLT registry.

Suggested fields:

id
tenant_id
name
code
vendor
model
serial_number
management_ip
snmp_port
snmp_version
snmp_community_encrypted
api_device_id
olt_type
pop_id
region_id
latitude
longitude
status
last_seen_at
last_sync_at
created_at
updated_at

Supported model values:

C300
C320

The OLT database record is the business/source-of-truth record.

The snmp-olt-zte registry/configuration is the network monitoring
runtime representation.

Maintain an explicit mapping:

Laravel OLT ID
↔
snmp-olt-zte OLT ID

Do not use management IP as the only identifier.

============================================================
MULTI-OLT
============================================================

The application MUST support multiple ZTE OLTs in one deployment.

Examples:

OLT-PEJATEN-C320-01
OLT-PEJATEN-C320-02
OLT-PEJATEN-C300-01
OLT-SERANG-C300-01
OLT-SERANG-C320-01

Do not assume one OLT per service instance.

Each OLT must have:

- independent SNMP configuration
- independent slot topology
- independent cache namespace
- independent health state
- independent metrics
- independent tenant/ownership relationship

Use the v3.2.0 multi-OLT API.

Per-OLT API pattern:

GET /api/v1/olt/{olt_id}/...

Examples:

GET /api/v1/olt/{olt_id}/uplinks

GET /api/v1/olt/{olt_id}/board/{slot}/pon/{pon}/...

Do not rely exclusively on the legacy default-OLT routes.

============================================================
C320 / C300 SLOT TOPOLOGY
============================================================

Do not hard-code:

board 1
board 2
16 PON

The v3.2.0 implementation supports configurable slot topology and
per-slot PON counts.

Examples:

C320:
1:16
2:16

C300:
3:16
5:8

The application UI MUST read actual discovered/configured topology.

The UI must not assume every slot has 16 PON ports.

Display:

Slot
Card Type
Role
PON Count
Online PON
Offline PON
ONU Count
Status

============================================================
UPLINK AUTO-DETECTION
============================================================

Use the v3.2.0 uplink auto-detection API.

Endpoint:

GET /api/v1/olt/{id}/uplinks

Also support:

GET /api/v1/uplinks

where appropriate for the default OLT compatibility path.

The UI must display:

Cards
Card Slot
Card Type
Card Role
Uplink Ports
Port Name
Port Type
Admin Status
Oper Status
Speed

Recognize:

gei = 1G
xgei = 10G

Example UI:

┌──────────────────────────────────────────────────┐
│ OLT UPLINKS                                      │
├──────────┬──────────┬──────────┬────────────────┤
│ Slot     │ Card     │ Role     │ Ports          │
├──────────┼──────────┼──────────┼────────────────┤
│ 3        │ GTGH     │ GPON     │ 16 PON         │
│ 19       │ HUVQ     │ UPLINK   │ xgei_1/19/1    │
└──────────┴──────────┴──────────┴────────────────┘

Port:

xgei_1/19/1
10 Gbps
Admin UP
Oper UP
● ONLINE

This is detection-only.

Do not create configuration-write functionality through this endpoint.

If uplink configuration is needed later, implement it through a separate
write-capable adapter and explicit authorization.

============================================================
ONU MONITORING
============================================================

Use snmp-olt-zte v3.2.0 for supported ONU monitoring.

The UI must support:

ONU ID
Serial Number
ONU Type
Name
Board
PON
Status
RX Power
TX Power where available
Uptime
Last Online
Last Offline
Distance where available
Temperature where available
MAC where available

Use paginated API responses for large ONU datasets.

Do not load every ONU from every OLT into the browser.

Use server-side pagination.

For fresh serial-list checks, support:

?nocache=true

where the upstream v3.2.0 API supports it.

Use this for operations where stale serial cache could cause an incorrect
provision/delete/replace decision.

============================================================
REDIS CACHE
============================================================

Do not create a second competing cache layer for the same ZTE data
unless there is a documented reason.

Respect snmp-olt-zte v3.2.0 per-OLT Redis namespacing.

If Laravel caches summarized data, use a separate namespace such as:

laravel:olt:{tenant_id}:{olt_id}:...

Do not overwrite or collide with the adapter's keys.

============================================================
TENANT ISOLATION
============================================================

The v3.2.0 service supports API_USERS and per-tenant OLT ownership.

The Laravel application MUST remain the primary authorization boundary.

Implement:

Laravel tenant authorization
+
network adapter API key
+
OLT ownership validation

A user must never access another tenant's OLT.

When a tenant requests an OLT it does not own:

return an appropriate application-level 404/forbidden response
according to the platform security policy.

Do not reveal the existence of another tenant's OLT.

============================================================
OLT HEALTH
============================================================

Use v3.2.0 readiness/health behavior.

Display:

ONLINE
DEGRADED
OFFLINE
UNKNOWN

The application must not mark an OLT ONLINE only because the database
record exists.

Health should be based on actual monitoring state.

If an OLT becomes unreachable:

- show OFFLINE/DEGRADED as appropriate
- create/update alarm
- update NOC
- calculate topology impact
- calculate affected customers
- optionally create incident according to automation policy
- notify authorized NOC users

Do not create an incident storm when many ONUs disappear because a
single parent PON/OLT failed.

============================================================
OLT NOC UI
============================================================

OLT detail page must contain:

Overview
Health
Cards
PON
ONU
Uplinks
Alarms
Metrics
Topology
Customers
Incidents
Work Orders
Audit

Header:

OLT-C600-PEJATEN-01
ZTE C320
● ONLINE

Quick metrics:

PON
ONU
Online ONU
Offline ONU
LOS
Uplinks
Critical Alarms

Actions:

Sync
Test Connection
Refresh
Topology
Impact Analysis
Create Work Order

============================================================
OLT DASHBOARD
============================================================

Use shadcn/ui style consistent with the selected reference design.

Example:

┌──────────────────────────────────────────────────────────────┐
│ OLT-C320-PEJATEN-01                         ● ONLINE         │
│ ZTE C320                                                    │
├─────────────┬─────────────┬─────────────┬───────────────────┤
│ PON         │ ONU         │ ONLINE      │ ALARMS            │
│ 32          │ 486         │ 472         │ 3                 │
├─────────────┴─────────────┴─────────────┴───────────────────┤
│                                                              │
│ CARDS / SLOTS                                                │
│                                                              │
│ Slot 3   GTGH   GPON      16 PON      ●                     │
│ Slot 19  HUVQ   UPLINK    10G         ●                     │
│                                                              │
├──────────────────────────────────────────────────────────────┤
│ UPLINKS                                                     │
│                                                              │
│ xgei_1/19/1     10G     UP     UP      ●                    │
│ gei_1/19/2      1G      UP     UP      ●                    │
│                                                              │
├──────────────────────────────────────────────────────────────┤
│ PON HEALTH                                                   │
│                                                              │
│ 1/3/1  ●  16 ONU     1/3/2  ●  15 ONU                      │
│ 1/3/3  🔴  0 ONU     1/3/4  ●  14 ONU                      │
└──────────────────────────────────────────────────────────────┘

============================================================
PON UI
============================================================

PON page must derive actual PON availability from the OLT/card
topology.

Show:

OLT
Slot
PON
Card Type
ONU Count
Online
Offline
LOS
Average RX
Status

Clicking PON:

open Sheet

Tabs:

Overview
ONUs
Optical
Alarms
Topology
Customers
Impact

============================================================
SNMP TRAP / REALTIME
============================================================

Where supported by v3.2.0, integrate SNMP Trap events for ONU offline
detection.

Flow:

ZTE OLT
→ SNMP Trap
→ snmp-olt-zte
→ webhook/event
→ Laravel event processing
→ Redis
→ WebSocket/Reverb
→ React

For polling-based events:

ZTE OLT
→ snmp-olt-zte
→ polling
→ state change
→ event
→ Laravel
→ WebSocket
→ React

Do not assume SNMP Trap is available on every deployment.

Provide fallback polling.

============================================================
PROMETHEUS / OBSERVABILITY
============================================================

Consume/expose monitoring metrics without duplicating collection.

Where possible, use the adapter's Prometheus-compatible metrics.

Laravel dashboard may aggregate:

OLT availability
PON availability
ONU online ratio
SNMP request latency
SNMP errors
cache hit ratio where available
polling health
event latency

============================================================
API ADAPTER
============================================================

Create a Laravel service:

ZteOltClientInterface

Suggested methods:

listOlts()
getOlt(id)
getHealth(id)
getUplinks(id)
getBoards(id)
getPons(id, board)
getOnus(id, board, pon)
getOnu(id, board, pon, onuId)
getOnuSerialList(id, board, pon, forceFresh)
getAlarms(id)
getMetrics(id)

Implementation:

SnmpOltZteClient

The client communicates with the v3.2.0 service.

Use:

HTTP timeout
retry
circuit breaker
structured errors
correlation ID
request logging without secrets

Do not expose upstream adapter API keys to the browser.

============================================================
CONFIGURATION
============================================================

Provide environment variables such as:

SNMP_OLT_ZTE_BASE_URL=
SNMP_OLT_ZTE_API_KEY=
SNMP_OLT_ZTE_TIMEOUT=
SNMP_OLT_ZTE_RETRY=

If using a separate multi-OLT service registry:

SNMP_OLT_ZTE_REGISTRY_MODE=

Document all environment variables in:

.env.example
ZTE-OLT.md
DEPLOYMENT.md

Never commit real credentials.

============================================================
DOCKER
============================================================

The production architecture may include:

nginx
laravel
queue
horizon
reverb
network-engine
snmp-olt-zte
postgres
redis

Do not embed the ZTE SNMP adapter directly into the Laravel PHP
container.

Keep the adapter as a separate Go service/container.

============================================================
TESTING — ZTE
============================================================

Create tests for:

C320
C300
multi-OLT
per-tenant access
invalid OLT
invalid board
invalid PON
per-slot PON count
uplink detection
ONU pagination
ONU cache
nocache=true
OLT offline
OLT recovery
Redis isolation
API authentication
timeout
retry
circuit breaker
readiness
realtime state update

Use simulator/mocks for CI.

For integration testing, allow a real lab OLT profile.

Never require a production OLT to run the normal CI test suite.

============================================================
ACCEPTANCE — ZTE
============================================================

The implementation is accepted only when:

[ ] C320 can be registered
[ ] C300 can be registered
[ ] Multiple OLTs can run
[ ] Each OLT has isolated configuration
[ ] OLT ownership is enforced
[ ] Boards/cards are discovered
[ ] Per-slot PON counts are respected
[ ] Uplinks are auto-detected
[ ] 1G gei ports are displayed
[ ] 10G xgei ports are displayed
[ ] PON list works
[ ] ONU list works
[ ] ONU pagination works
[ ] ONU status works
[ ] RX monitoring works
[ ] Serial-list refresh works
[ ] nocache=true is supported where applicable
[ ] Redis cache does not collide between OLTs
[ ] OLT health is realtime
[ ] ONU offline events reach NOC
[ ] alarms reach NOC
[ ] topology updates
[ ] impact analysis works
[ ] OLT detail page works
[ ] PON detail page works
[ ] ONU detail page works
[ ] API keys are never exposed to frontend
[ ] all network operations are audited
[ ] tests pass
[ ] documentation is complete

============================================================
REFERENCE
============================================================

Primary upstream/reference project:

Cepat-Kilat-Teknologi/snmp-olt-zte

Required release:

v3.2.0

GitHub:
https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte

Release:
https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte/releases/tag/v3.2.0

Go module:

github.com/Cepat-Kilat-Teknologi/snmp-olt-zte@v3.2.0

The AI coding agent MUST read the upstream README, OpenAPI specification,
examples and release notes before implementing the integration.

Do not guess endpoint paths or response structures when the upstream
OpenAPI specification provides the correct contract.

============================================================
END OF ZTE OLT INTEGRATION STANDARD
============================================================

END OF MASTER BUILD PROMPT
============================================================


============================================================
UI/UX OVERRIDE — BILLING-FIRST DESIGN
============================================================

IMPORTANT:

This section OVERRIDES the previous NOC-first visual direction.

The application MUST use a:

SHADCN/UI BILLING / FINANCE / ISP MANAGEMENT DASHBOARD STYLE

The network/NOC features remain fully functional, but the overall
visual identity and primary dashboard hierarchy must feel like a
modern premium BILLING application.

The application must NOT look primarily like a NOC dashboard.

NOC is a module inside the platform.

The main application experience is:

BILLING
+
CUSTOMER MANAGEMENT
+
SUBSCRIPTIONS
+
PAYMENTS
+
REVENUE
+
OPERATIONS
+
NETWORK

The design reference should feel similar to a premium modern SaaS
billing/finance dashboard using shadcn/ui:

- dark mode as primary
- clean compact sidebar
- compact topbar
- KPI cards
- revenue charts
- invoice tables
- payment tables
- customer tables
- subscription metrics
- cash-flow summaries
- payment status badges
- clean forms
- drawers/sheets
- command palette
- subtle borders
- subtle shadows
- small/medium radius
- restrained colors
- high information density
- strong typography hierarchy

Do NOT make the interface look like:
- a traditional ISP NOC
- an old network monitoring system
- a generic Bootstrap admin panel
- an overly colorful accounting application

============================================================
BILLING-FIRST VISUAL HIERARCHY
============================================================

The main dashboard priority must be:

1. Revenue
2. Customers
3. Active Subscriptions
4. Invoices
5. Payments
6. Outstanding / Overdue
7. Service Status
8. Operations
9. Network Health
10. NOC / Incidents

The network is still important, but should not visually dominate the
main management dashboard.

============================================================
BILLING DASHBOARD
============================================================

The main Dashboard MUST resemble a premium billing SaaS dashboard.

Header:

Dashboard

Subtitle:

Overview of your business, billing and network

Top-right:

Date Range
Export / Download
Notifications
Realtime
User

KPI cards:

Total Revenue
Paid Invoices
Outstanding
Overdue
Active Customers
Active Subscriptions

Example:

┌────────────────┐
│ Total Revenue  │
│ Rp 284.5M      │
│ ↑ 12.4%        │
│ vs last month  │
└────────────────┘

┌────────────────┐
│ Paid Invoices  │
│ 10,482         │
│ ↑ 8.2%         │
└────────────────┘

┌────────────────┐
│ Outstanding    │
│ Rp 48.2M       │
│ ↓ 4.1%         │
└────────────────┘

┌────────────────┐
│ Overdue        │
│ Rp 12.7M       │
│ 184 invoices   │
└────────────────┘

Use shadcn Card.

Use compact typography.

Avoid oversized KPI numbers.

============================================================
BILLING DASHBOARD LAYOUT
============================================================

Recommended layout:

Row 1:
6 KPI cards

Row 2:
Revenue Overview
Invoice Status

Row 3:
Recent Payments
Recent Invoices

Row 4:
Customer Growth
Subscription Distribution

Row 5:
Service Status
Network Health

Example:

┌─────────────────────────────────────────────────────────────┐
│ Dashboard                                                   │
│ Overview of your business, billing and network              │
│                                                             │
│ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐    │
│ │Revenue │ │Paid    │ │Pending │ │Overdue │ │Customer│    │
│ │Rp284M  │ │10.4K   │ │1.2K    │ │184     │ │12.8K   │    │
│ └────────┘ └────────┘ └────────┘ └────────┘ └────────┘    │
│                                                             │
│ ┌──────────────────────────────────┐ ┌────────────────────┐ │
│ │ Revenue Overview                 │ │ Invoice Status      │ │
│ │                                  │ │                    │ │
│ │        ╭────╮                    │ │ Paid       78%     │ │
│ │   ╭────╯    ╰────╮               │ │ Pending    12%     │ │
│ │ ──╯              ╰──             │ │ Overdue     7%     │ │
│ │                                  │ │ Cancelled   3%     │ │
│ └──────────────────────────────────┘ └────────────────────┘ │
│                                                             │
│ ┌──────────────────────────────────┐ ┌────────────────────┐ │
│ │ Recent Payments                  │ │ Recent Invoices     │ │
│ │                                  │ │                    │ │
│ │ Customer  Amount     Status      │ │ INV-001   Paid     │ │
│ │ Ahmad     Rp150K     Paid        │ │ INV-002   Pending  │ │
│ │ Budi      Rp250K     Paid        │ │ INV-003   Overdue  │ │
│ └──────────────────────────────────┘ └────────────────────┘ │
└─────────────────────────────────────────────────────────────┘

============================================================
BILLING SIDEBAR
============================================================

The sidebar must visually prioritize Billing.

MAIN

Dashboard

CUSTOMERS

Customers
Subscriptions
Packages
Partners

BILLING

Invoices
Payments
Payment Gateway
Outstanding
FUP
Revenue

NETWORK

OLT
PON
ONU
MikroTik
RADIUS
IPAM
VLAN

FTTH

Topology
ODC
ODP
Fiber
Splitters

OPERATIONS

PSB
Tickets
Incidents
Work Orders
Dispatch

FIELD SERVICE

Technicians
Schedule
Inventory

REPORTS

Financial
Customers
Network
Operations

SYSTEM

Users
Roles
Integrations
Notifications
Audit Logs
Settings

Use section labels in small muted typography.

Use badges for:
Overdue
Critical
Open Tickets
Pending Work Orders

============================================================
BILLING PAGE DESIGN
============================================================

Billing pages should use a consistent layout:

Page Header
→ KPI Summary
→ Filter Toolbar
→ DataTable
→ Pagination

Example:

Invoices

[Search invoices...] [Status] [Customer] [Date] [Export] [+ Invoice]

┌───────────────────────────────────────────────────────────────┐
│ Invoice      Customer       Amount       Due Date      Status │
├───────────────────────────────────────────────────────────────┤
│ INV-000123   Ahmad         Rp150.000    25 Aug        PAID   │
│ INV-000124   Budi          Rp250.000    25 Aug        PENDING│
│ INV-000125   Rudi          Rp150.000    20 Aug        OVERDUE│
└───────────────────────────────────────────────────────────────┘

Use:
shadcn Table
+
TanStack Table

============================================================
PAYMENT UI
============================================================

Payment pages should visually resemble a modern finance dashboard.

Payment status:

PAID
PENDING
FAILED
REFUNDED

Use subtle semantic badges.

Payment detail Sheet:

Transaction
Invoice
Customer
Gateway
Payment Method
Amount
Fee
Net Amount
Status
Created
Paid At
Gateway Reference
Webhook Status

Actions:

View Invoice
Send Receipt
Refund
Open Customer

============================================================
INVOICE DETAIL UI
============================================================

Invoice detail must resemble a modern digital billing document.

Header:

Invoice #INV-000123
PAID

Customer:
Ahmad

Billing period:
01 Aug 2026 — 31 Aug 2026

Items:

Internet 100 Mbps
Rp150.000

Subtotal
Tax
Discount
Total

Payment history.

Actions:

Download PDF
Send Invoice
Record Payment
Refund
Cancel

Use shadcn Card, Separator, Badge, DropdownMenu and Sheet/Dialog.

============================================================
CUSTOMER BILLING UI
============================================================

Customer page should prioritize billing information.

Header:

Customer Name
Customer ID
ACTIVE

KPI:

Monthly Bill
Outstanding
Last Payment
Next Due Date

Tabs:

Overview
Subscriptions
Invoices
Payments
Network
Tickets
Work Orders
Activity

Billing tab should show:

Invoice history
Payment history
Outstanding
Payment methods
Billing cycle
Discount
Tax

============================================================
SUBSCRIPTION UI
============================================================

Subscription cards should look like modern SaaS subscription management.

Example:

┌────────────────────────────────────┐
│ Internet 100 Mbps                  │
│ ACTIVE                             │
│                                    │
│ Rp150.000 / month                  │
│                                    │
│ PPPoE                              │
│ IP: 103.xxx.xxx.xxx                │
│                                    │
│ Next Billing: 25 Sep 2026          │
│                                    │
│ [Manage] [View Invoice]            │
└────────────────────────────────────┘

Support:

STATIC
DHCP
PPPOE
HOTSPOT

============================================================
REVENUE ANALYTICS UI
============================================================

Revenue dashboard should be the primary analytics page.

Show:

Gross Revenue
Net Revenue
Paid
Outstanding
Overdue
Refunds

Charts:

Revenue trend
Daily collections
Monthly revenue
Payment method distribution
Package revenue
Partner revenue

Use shadcn chart styling.

Avoid flashy charts.

============================================================
CUSTOMER GROWTH UI
============================================================

Show:

New Customers
Churn
Active
Suspended
Terminated

Chart:

New Customers vs Churn

Also:

Package Distribution
Service Type Distribution

============================================================
NOC VISUAL STYLE INSIDE BILLING UI
============================================================

NOC pages may use a slightly darker/higher-density layout, but MUST
still use the same shadcn billing design system.

NOC should NOT introduce a completely separate visual language.

Use:

same sidebar
same topbar
same cards
same badges
same typography
same spacing
same table design

Only the content density changes.

============================================================
NETWORK UI STYLE
============================================================

OLT/PON/ONU pages must follow the billing application's design system.

Example:

OLT Management

┌─────────────────────────────────────────────────────────────┐
│ OLT Management                             + Add OLT         │
│ Manage your ZTE network devices                              │
│                                                             │
│ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐               │
│ │ 12     │ │ 11     │ │ 32     │ │ 2,842  │               │
│ │ OLTs   │ │ Online │ │ PON    │ │ ONUs   │               │
│ └────────┘ └────────┘ └────────┘ └────────┘               │
│                                                             │
│ [Search...] [Vendor] [Model] [Status] [Region]             │
│                                                             │
│ OLT          Model     PON    ONU     Status       Actions │
│ C320-01      C320      32     486     ONLINE       ...     │
│ C300-01      C300      16     245     ONLINE       ...     │
└─────────────────────────────────────────────────────────────┘

This keeps the network module visually consistent with billing.

============================================================
TOPOLOGY UI
============================================================

Topology can be visually richer, but surrounding controls must still
use the billing/shadcn design language.

Toolbar:

Search
Filters
Trace
Impact
Fullscreen

Use React Flow only for the topology canvas.

Node detail must use shadcn Sheet.

============================================================
TECHNICIAN / OPERATIONS UI
============================================================

Technician pages should also use the same billing-oriented design
system.

Use:

Cards
Tables
Calendar
Sheet
Dialog
Badge
Command

Do not create a separate field-service design system.

============================================================
COLOR STRATEGY
============================================================

Primary:

neutral / monochrome shadcn palette

Accent:

blue or indigo for primary actions

Success:

green

Warning:

amber

Critical:

red

Info:

blue

Billing statuses should remain subtle.

Example:

PAID       → success
PENDING    → muted/blue
OVERDUE    → red
FAILED     → red
REFUNDED   → purple/neutral

Do not flood the screen with colored backgrounds.

============================================================
TYPOGRAPHY
============================================================

Use:

Geist or Inter

Hierarchy:

Page title:
24–28px

Section title:
16–18px

Card title:
14–16px

Body:
13–14px

Table:
12–14px

Metadata:
11–12px

KPI:
22–30px

Keep typography compact like the selected billing reference.

============================================================
BORDER / RADIUS
============================================================

Use:

small to medium radius.

Avoid excessive rounded cards.

Prefer:

rounded-md
rounded-lg

Avoid:

rounded-3xl

Borders should be subtle.

Use shadcn border tokens.

============================================================
LIGHT / DARK MODE
============================================================

Support:

Dark
Light
System

Default:

Dark

The dark theme should resemble a premium finance/billing SaaS.

Light mode should remain clean and professional.

============================================================
MOBILE BILLING UI
============================================================

Customer and billing interfaces must be mobile friendly.

Mobile dashboard:

Revenue
Outstanding
Invoice
Payment
Service

Use stacked cards.

Invoice and payment tables may switch to compact cards on mobile.

============================================================
FINAL UI PRINCIPLE
============================================================

The visual identity of PT Mitra Media Data is:

SHADCN/UI
+
PREMIUM BILLING
+
FINANCE DASHBOARD
+
ISP MANAGEMENT
+
NETWORK OPERATIONS

NOT:

SHADCN/UI
+
NOC-FIRST

The NOC is a powerful module, but the overall product must feel like
a professional BILLING/ISP MANAGEMENT PLATFORM.

The main dashboard should immediately communicate:

Revenue
Customers
Subscriptions
Invoices
Payments
Outstanding
Operations

The network should appear as an integrated operational layer.

============================================================
END OF BILLING-FIRST UI OVERRIDE
============================================================


============================================================
FINAL IMPLEMENTATION OVERRIDE — USE THIS AS THE FINAL AUTHORITY
============================================================

If any earlier section conflicts with this section, this section wins.

PRODUCT:
PT Mitra Media Data
ISP & FTTH Platform

PRIMARY UI:
SHADCN/UI — PREMIUM BILLING / FINANCE DASHBOARD

NETWORK:
ZTE C300/C320 monitoring MUST use:
github.com/Cepat-Kilat-Teknologi/snmp-olt-zte@v3.2.0

Reference release:
v3.2.0 — Multi-OLT, per-tenant keys, uplink auto-detect (C320/C300)

Do NOT replace the required ZTE adapter with another project.

Do NOT implement a second competing ZTE SNMP/OID engine for the same
monitoring functions.

============================================================
A. FINAL UI DIRECTION
============================================================

The uploaded visual reference is the design direction.

The application must look like a premium dark billing SaaS dashboard:

- dark black/charcoal background
- compact left sidebar
- subtle borders
- medium/small rounded corners
- white primary typography
- muted gray secondary typography
- restrained purple accent
- green success
- orange warning
- red critical
- compact KPI cards
- financial charts
- tables
- payment cards
- invoice management
- customer management
- network health integrated below business/billing information

The main dashboard MUST feel like a billing platform first.

The NOC is a powerful module, not the visual identity of the entire
application.

Use the visual hierarchy:

Revenue
Customers
Subscriptions
Invoices
Payments
Outstanding
Operations
Network

============================================================
B. FINAL SIDEBAR
============================================================

BRAND

PT Mitra Media Data
ISP & FTTH Platform

MAIN
Dashboard
NOC Command Center

BILLING
Customers
Subscriptions
Invoices
Payments
Outstanding
Payment Gateway
FUP Management

NETWORK
OLT Management
PON Management
ONU Management
MikroTik Routers
RADIUS Servers
IPAM & VLAN

FTTH INFRASTRUCTURE
Topology Map
ODC Management
ODP Management
Fiber Management
Splitters

OPERATIONS
PSB / New Order
Tickets
Work Orders
Dispatch Center
Incidents

FIELD SERVICE
Technicians
Schedules
Inventory

PARTNER & ADMIN
Partners
Reports
Settings

Use sidebar badges for:

Critical Alarms
Open Tickets
Open Work Orders
Overdue Invoices

============================================================
C. FINAL DASHBOARD
============================================================

Header:

Dashboard
Overview of your business, billing and network

Top-right:

Date range
Download
Notifications
Realtime
Theme
Settings
Profile

KPI row:

Total Revenue
Total Paid
Pending Invoices
Overdue Amount
Total Customers

Each KPI card contains:

label
large value
trend percentage
comparison period
mini sparkline
icon

Second row:

Customer Support / Activity
Revenue Overview
Invoice Status

Third row:

Latest Payments
Payment Method

Fourth row:

Network Health
Active Alarms

The dashboard must remain visually close to the supplied reference:
dark, compact, premium, clean, information-dense.

============================================================
D. BILLING-FIRST UX
============================================================

The most common workflows must be fast:

1. Search customer
2. View customer
3. View subscription
4. View invoice
5. Receive payment
6. Check outstanding
7. Open ticket
8. Check service
9. Trace network
10. Create work order

Use:

Command Palette
Quick Actions
Sheet
Drawer
Dialog
Context Menu
Keyboard shortcuts

============================================================
E. ZTE OLT — NON-NEGOTIABLE
============================================================

Use exactly:

github.com/Cepat-Kilat-Teknologi/snmp-olt-zte@v3.2.0

GitHub:
https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte

Release:
https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte/releases/tag/v3.2.0

The v3.2.0 release is the canonical ZTE C320/C300 SNMP adapter.

It supports:

- C320
- C300
- multi-OLT
- per-tenant API keys
- per-OLT SNMP pools
- per-OLT Redis namespaces
- per-slot PON counts
- uplink/card auto-detection
- ENTITY-MIB discovery
- IF-MIB discovery
- gei 1G detection
- xgei 10G detection
- SNMP pooling
- bounded concurrency
- Redis caching
- cache prewarming
- singleflight
- batched SNMP GET
- BulkWalk
- Prometheus metrics
- SNMP Trap
- RX power monitoring
- configurable thresholds
- OpenAPI
- readiness/health endpoints
- load tests

These capabilities must be integrated rather than reimplemented.

============================================================
F. ZTE SERVICE ARCHITECTURE
============================================================

Use a separate container/service:

snmp-olt-zte

Architecture:

React
  |
Laravel
  |
ZteOltClient
  |
HTTP
  |
snmp-olt-zte v3.2.0
  |
SNMP
  |
ZTE C300/C320

Redis is shared where appropriate but cache namespaces MUST remain
isolated.

Laravel is responsible for:

- OLT business records
- tenant ownership
- RBAC
- UI
- topology relationships
- customers
- incidents
- tickets
- work orders
- audit
- business rules

snmp-olt-zte is responsible for:

- ZTE SNMP communication
- OLT discovery/monitoring
- board/card discovery
- PON monitoring
- ONU monitoring
- uplink auto-detection
- SNMP health
- supported realtime/trap functions
- Redis cache used by the adapter
- Prometheus metrics

============================================================
G. MULTI-OLT
============================================================

Support unlimited practical OLT registry.

Examples:

C320-PEJATEN-01
C320-PEJATEN-02
C300-PEJATEN-01
C300-SERANG-01

Each OLT:

id
tenant_id
name
code
vendor
model
management_ip
snmp_port
snmp_version
encrypted_community
user_id/tenant owner
POP
region
latitude
longitude
status
last_seen_at
last_sync_at

Use a stable OLT ID.

Do NOT use management IP as the primary identifier.

Use per-OLT endpoints:

/api/v1/olt/{olt_id}/...

The adapter v3.2.0 supports the OLT dimension in the API.

============================================================
H. TENANT SECURITY
============================================================

Use Laravel RBAC as the primary application authorization.

The adapter's API_USERS / API key mechanism must also be respected.

Rules:

unknown API key → 401
unauthorized OLT → 404
authorized OLT → normal response
admin → all permitted OLTs

Never expose another tenant's OLT existence.

Never expose the adapter API key to React.

Never expose SNMP community strings.

Encrypt credentials at rest.

============================================================
I. OLT UI
============================================================

OLT Management should look like a billing SaaS data-management page.

Header:

OLT Management
Manage your ZTE network devices

Actions:

+ Add OLT
Discover
Sync
Export

KPI:

Total OLTs
Online
Offline
Total PON
Total ONU

Table:

OLT
Model
POP
Management IP
PON
ONU
Status
Last Sync
Actions

Actions:

View
Sync
Test
Topology
Alarms

============================================================
J. OLT DETAIL
============================================================

Header:

OLT-C320-PEJATEN-01
ZTE C320
● ONLINE

KPI:

PON
ONU
Online ONU
Offline ONU
LOS
Uplinks
Alarms

Tabs:

Overview
Cards
PON
ONU
Uplinks
Alarms
Metrics
Topology
Customers
Incidents
Work Orders
Audit

============================================================
K. UPLINK AUTO-DETECT
============================================================

Use v3.2.0:

GET /api/v1/olt/{id}/uplinks

Also support the default:

GET /api/v1/uplinks

The adapter detects:

cards via ENTITY-MIB
ports via IF-MIB

Classify:

gpon
control
uplink
power

Detect:

gei = 1G
xgei = 10G

Display:

Slot
Card Type
Role
Port
Kind
Admin
Oper
Speed

Example:

Slot 19
HUVQ
UPLINK

xgei_1/19/1
10G
UP
UP

This is detection-only.

Do not use the endpoint for configuration writes.

============================================================
L. C320/C300 SLOT TOPOLOGY
============================================================

Do NOT assume fixed slot numbers.

Do NOT assume every card has 16 PON.

Use actual adapter-discovered/configured slot topology.

v3.2.0 supports per-slot PON counts such as:

3:16
5:8

The UI must show actual:

slot
card
role
PON count
online PON
offline PON

Invalid board/PON combinations must be rejected.

============================================================
M. PON UI
============================================================

Table:

OLT
Slot
PON
Card
ONU
Online
Offline
LOS
Average RX
Status

Detail Sheet:

Overview
ONU
Optical
Alarms
Topology
Customers
Impact

============================================================
N. ONU UI
============================================================

Table:

Serial
ONU ID
Customer
OLT
Slot
PON
ODC
ODP
RX
TX
Status
Last Seen

Filters:

OLT
Slot
PON
ODC
ODP
Status
LOS
RX

Use server-side pagination.

Never load all ONU records into the browser.

Use adapter paginated endpoints where available.

============================================================
O. FORCED-FRESH ONU SERIAL LIST
============================================================

Support v3.2.0:

?nocache=true

for serial-list reads where a fresh SNMP state is required.

Use it for:

provisioning validation
replace
delete
uniqueness checks
post-provision verification

Normal reads may use cache.

Do not disable caching globally.

============================================================
P. REDIS CACHE
============================================================

Respect adapter cache namespacing.

v3.2.0 uses per-OLT Redis namespaces.

Laravel's own cache namespace must be separate.

Example:

laravel:tenant:{tenant}:olt:{olt}:...

Do not overwrite adapter keys.

============================================================
Q. ZTE HEALTH
============================================================

Use:

/healthz
/readyz

where exposed by the adapter deployment.

Display:

ONLINE
DEGRADED
OFFLINE
UNKNOWN

If one secondary OLT is unreachable, do not mark the entire service
not-ready when v3.2.0 readiness semantics classify it as non-critical.

Generate:

alarm
NOC update
incident according to policy
topology impact
affected customers

Avoid alarm storms.

============================================================
R. REALTIME ZTE
============================================================

Supported event flow:

ZTE
→ SNMP Trap / polling
→ snmp-olt-zte
→ event
→ Redis
→ Laravel
→ WebSocket/Reverb
→ React

Realtime UI:

OLT state
PON state
ONU state
LOS
RX threshold
alarms
incidents
affected customers

If traps are unavailable:

use polling fallback.

============================================================
S. FTTH TOPOLOGY
============================================================

Topology:

POP
→ OLT
→ SLOT
→ PON
→ ODC
→ FIBER
→ ODP
→ ODP PORT
→ ONU
→ CUSTOMER

Use React Flow.

Use shadcn for:

toolbar
filters
Sheet
Dialog
Badge
Command
menus

Click node:

open Sheet.

============================================================
T. BILLING + NETWORK RELATIONSHIP
============================================================

Every customer service should be traceable:

Customer
→ Subscription
→ IP/RADIUS
→ MikroTik
→ ONU
→ ODP
→ Fiber
→ ODC
→ PON
→ OLT
→ POP

Customer page must show both:

Billing status
Network status

Example:

CUSTOMER
Ahmad Fauzi

Billing:
PAID
Rp150.000/month

Service:
ACTIVE
100 Mbps PPPoE

Network:
ONLINE

ONU:
ZTEGC123456
RX -21.4 dBm

OLT:
C320-PEJATEN-01

PON:
1/1/3

ODP:
ODP-001

============================================================
U. PAYMENT GATEWAY
============================================================

Support:

Midtrans
Xendit

Payment methods:

QRIS
Virtual Account
Bank Transfer
E-Wallet
Card

Implement:

webhook signature validation
idempotency
retry
transaction log
audit

============================================================
V. RADIUS
============================================================

Support:

PPPoE
Hotspot

Show:

sessions
username
NAS
IP
start
stop
duration
traffic
auth result

============================================================
W. MIKROTIK
============================================================

Support:

RouterOS API
REST
SSH fallback

Manage:

PPPoE
Hotspot
DHCP
Static
VLAN
Queues
Address
Routes
Interfaces

============================================================
X. SERVICE TYPES
============================================================

STATIC
DHCP
PPPOE
HOTSPOT

Provisioning must support the appropriate backend combination.

============================================================
Y. PROVISIONING
============================================================

Flow:

Customer
→ Subscription
→ Billing activation
→ IP allocation
→ RADIUS
→ MikroTik
→ OLT/ONU
→ ODP
→ Verification
→ Activation

Each step:

PENDING
RUNNING
SUCCESS
FAILED
RETRY

Support:

retry
rollback
audit
operator approval where required

============================================================
Z. TECHNICIAN / WORK ORDER
============================================================

Support:

PSB
Installation
LOS Repair
ONU Replacement
ODP Repair
Fiber Repair
Maintenance
Survey

Work Order statuses:

Pending
Scheduled
Assigned
En Route
Arrived
In Progress
Waiting
Completed
Failed

============================================================
AA. DISPATCH
============================================================

Use:

FullCalendar
MapLibre/Leaflet
shadcn Sheet/Dialog/Card/Badge

Recommend technician using:

skill
distance
availability
workload
SLA
region

============================================================
AB. CUSTOMER PORTAL
============================================================

Customer sees:

Internet
Package
Invoice
Payment
Usage
Network
Ticket
Work Order

Primary action:

Bayar Sekarang

============================================================
AC. PARTNER PORTAL
============================================================

Partner sees:

Customers
PSB
Installations
Commission
Revenue
Outstanding

============================================================
AD. REPORTING
============================================================

Financial:

Revenue
Paid
Outstanding
Overdue
Refund

Customer:

New
Active
Suspended
Churn

Network:

OLT
PON
ONU
Availability
LOS

Operations:

Tickets
Incidents
Work Orders
SLA

Technician:

Jobs
Completion
SLA
Performance

============================================================
AE. DATABASE
============================================================

Use PostgreSQL + PostGIS.

Create proper migrations for:

users
roles
permissions
tenants
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
radius_accounts
radius_sessions
mikrotik_devices
mikrotik_profiles
olts
olt_boards
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
ip_pools
ip_subnets
ip_addresses
vlans
alarms
incidents
tickets
ticket_comments
psb_orders
surveys
installations
technicians
technician_teams
technician_skills
technician_availability
technician_locations
work_orders
work_order_assignments
work_order_checklists
work_order_materials
work_order_tools
work_order_photos
work_order_measurements
work_order_comments
work_order_status_histories
customer_appointments
partners
partner_customers
partner_commissions
notifications
webhooks
audit_logs
provisioning_jobs
provisioning_steps

============================================================
AF. OBSERVABILITY
============================================================

Go services:

/health
/ready
/metrics

Collect:

request latency
SNMP latency
SNMP errors
OLT health
PON health
ONU health
worker count
queue depth
event latency
cache health

Use Prometheus-compatible metrics.

============================================================
AG. SECURITY
============================================================

Implement:

RBAC
2FA
CSRF
XSS protection
rate limiting
secure headers
encrypted credentials
API authentication
webhook verification
audit logs
tenant isolation

Never log:

SNMP community
API keys
payment secrets
SSH credentials
RADIUS shared secrets

============================================================
AH. TASK.MD
============================================================

Create a complete TASK.md with:

ID
Phase
Priority
Task
Dependencies
Acceptance Criteria
Status

Phases:

P01 Foundation
P02 UI Design System
P03 Auth
P04 RBAC
P05 Customer
P06 Subscription
P07 Billing
P08 Payment
P09 RADIUS
P10 MikroTik
P11 ZTE Adapter Integration
P12 OLT
P13 PON
P14 ONU
P15 IPAM
P16 VLAN
P17 ODC
P18 ODP
P19 Fiber
P20 Topology
P21 NOC
P22 Incident
P23 Ticket
P24 PSB
P25 Technician
P26 Work Order
P27 Scheduling
P28 Dispatch
P29 Partner
P30 Customer Portal
P31 Realtime
P32 Reporting
P33 Security
P34 Testing
P35 Deployment

============================================================
AI EXECUTION RULE
============================================================

Before coding:

1. Inspect repository.
2. Read the ZTE v3.2.0 README.
3. Read the ZTE v3.2.0 OpenAPI specification.
4. Read v3.2.0 release notes.
5. Inspect the existing application.
6. Create architecture.
7. Create ERD.
8. Create TASK.md.
9. Create DESIGN.md.
10. Create API documentation.

Then implement phase by phase.

For every phase:

implement
→ test
→ lint
→ build
→ fix
→ update TASK.md
→ update documentation

Do not claim completion without verification.

============================================================
FINAL ACCEPTANCE
============================================================

The application is accepted only when:

UI matches the selected shadcn billing design direction.

PT Mitra Media Data branding is used everywhere.

Billing works.

Customers work.

Subscriptions work.

Payments work.

Payment gateway works.

RADIUS works.

MikroTik works.

ZTE C300 works through snmp-olt-zte v3.2.0.

ZTE C320 works through snmp-olt-zte v3.2.0.

Multi-OLT works.

Per-tenant access works.

Uplink auto-detection works.

Per-slot PON topology works.

ONU monitoring works.

ONU pagination works.

nocache=true flow works.

Redis isolation works.

OLT health works.

Realtime events work.

Topology works.

Trace works.

Impact analysis works.

NOC works.

Tickets work.

Incidents work.

PSB works.

Technician scheduling works.

Dispatch works.

Work Orders work.

Partner portal works.

Customer portal works.

Reports work.

RBAC works.

Audit works.

Tests pass.

Docker deployment works.

Documentation is complete.

============================================================
END OF FINAL IMPLEMENTATION OVERRIDE
============================================================


============================================================
MASTER UI CONSISTENCY STANDARD — MANDATORY
============================================================

IMPORTANT:

Every page in the application MUST look like it belongs to the same
product.

Do NOT design each module independently.

Do NOT allow:
- different sidebar layouts
- different topbars
- different button styles
- different card styles
- different table styles
- different form layouts
- different spacing systems
- different typography
- different status colors
- different border radius
- different page-header patterns
- different empty states
- different loading states
- different confirmation dialogs

The application must feel like one coherent product:

PT MITRA MEDIA DATA
ISP & FTTH PLATFORM

The UI reference style is the approved shadcn/ui dark premium billing
dashboard.

============================================================
1. SINGLE DESIGN SYSTEM
============================================================

Use ONE shared design system across:

Dashboard
Customers
Subscriptions
Packages
Invoices
Payments
Payment Gateway
Outstanding
FUP
OLT
PON
ONU
MikroTik
RADIUS
IPAM
VLAN
Topology
ODC
ODP
Fiber
PSB
Tickets
Incidents
Work Orders
Dispatch
Technicians
Schedules
Inventory
Partners
Reports
Settings
Customer Portal
Partner Portal
NOC

No module may introduce a separate visual language.

============================================================
2. SHARED APP SHELL
============================================================

Every authenticated admin/management page MUST use the same:

AppShell
Sidebar
Topbar
Breadcrumb
PageContainer
PageHeader
NotificationCenter
RealtimeIndicator
UserMenu

Structure:

<AppShell>
  <Sidebar />
  <Main>
    <Topbar />
    <PageContainer>
      <Breadcrumb />
      <PageHeader />
      <PageContent />
    </PageContainer>
  </Main>
</AppShell>

Do not duplicate shell markup in individual pages.

============================================================
3. SHARED SIDEBAR
============================================================

Create ONE reusable Sidebar component.

All pages use the same sidebar.

Sidebar states:

Expanded
Collapsed
Mobile Drawer

Sidebar width:

Expanded: 240–260px
Collapsed: 64–72px

Section labels:

MAIN
BILLING
NETWORK
FTTH INFRASTRUCTURE
OPERATIONS
FIELD SERVICE
PARTNER & ADMIN

Active navigation:

subtle highlighted background
left/edge indicator where appropriate
consistent icon
consistent text

Badges:

Critical alarms
Open tickets
Work orders
Overdue invoices

Badge styling must be consistent everywhere.

============================================================
4. SHARED TOPBAR
============================================================

Every page uses the same Topbar.

Elements:

Global Search
Command Menu shortcut
Realtime status
Notifications
Theme switch
Settings
User avatar
User menu

Do not create page-specific topbars unless it is a specialized
full-screen experience such as a topology canvas.

Even specialized pages must preserve the same visual language.

============================================================
5. GLOBAL PAGE HEADER
============================================================

Every management page follows:

Breadcrumb

Page Title
Short Description

Right-side Actions

Example:

Customers
Manage your customers and internet services

[Export] [+ Add Customer]

For simple pages:

Page Title
Description
Actions

For complex pages:

Page Title
Description
Primary Action
Secondary Actions

Use ONE shared PageHeader component.

============================================================
6. PAGE CONTAINER
============================================================

Use a common max-width and spacing system.

Default:

px-4
sm:px-6
lg:px-8

Vertical:

space-y-6

Do not randomly use different spacing on different pages.

Dashboard may use tighter grid spacing.

Operational tables may use compact spacing.

But all spacing must come from the design token system.

============================================================
7. STANDARD PAGE PATTERNS
============================================================

Every page MUST use one of the following standardized patterns.

PATTERN A — LIST

PageHeader
KPI Summary
Filter Toolbar
DataTable
Pagination

Used for:

Customers
Invoices
Payments
OLT
PON
ONU
Tickets
Work Orders
Technicians
Partners

PATTERN B — DETAIL

PageHeader
Summary Card
Tabs
Content Sections

Used for:

Customer Detail
OLT Detail
ONU Detail
Invoice Detail
Work Order Detail
Technician Detail

PATTERN C — DASHBOARD

PageHeader
KPI Grid
Charts
Tables
Status Panels

Used for:

Main Dashboard
Billing Dashboard
NOC
Network
Reports

PATTERN D — CREATE / EDIT

PageHeader
Form Card
Sections
Sticky Action Footer

Used for:

Customer
Subscription
Package
OLT
ODC
ODP
Work Order
Technician

PATTERN E — COMMAND CENTER

PageHeader
KPI Bar
Map/Canvas
Side Panels
Activity Feed

Used for:

NOC
Dispatch
Topology

============================================================
8. STANDARD PAGE HEADER
============================================================

Example:

┌──────────────────────────────────────────────────────────────┐
│ Customers                                      + Add Customer│
│ Manage customers and internet services                       │
└──────────────────────────────────────────────────────────────┘

Every page should have similar visual proportions.

Title:

text-xl / text-2xl

Description:

text-sm muted

Actions:

shadcn Button

Primary action:

default/primary

Secondary:

outline

Danger:

destructive

============================================================
9. STANDARD KPI CARDS
============================================================

Use one reusable MetricCard component.

All KPI cards use:

Card
Icon
Label
Value
Trend
Comparison
Optional Sparkline

Example:

┌────────────────────────────┐
│ Total Revenue          $   │
│                            │
│ Rp 284.5M                  │
│ ↑ 12.4% from last month    │
│ ~~~~~~~~                   │
└────────────────────────────┘

Do not create custom KPI cards per module.

Supported variants:

default
success
warning
critical
info

The visual structure stays identical.

============================================================
10. STANDARD TABLE
============================================================

Use ONE shared enterprise DataTable.

Technology:

shadcn/ui
TanStack Table

Features:

Search
Filters
Sorting
Pagination
Column visibility
Row selection
Bulk actions
Export
Row actions

All tables must have consistent:

header height
row height
font size
border
hover state
selected state
empty state
pagination

Recommended density:

compact but readable.

============================================================
11. TABLE TOOLBAR
============================================================

Every list page uses:

┌──────────────────────────────────────────────────────────────┐
│ Search...    [Filter] [Status] [Date]        [Export] [+ Add]│
└──────────────────────────────────────────────────────────────┘

Search on left.

Filters next.

Actions on right.

For mobile:

search
filter button
more actions

============================================================
12. STANDARD STATUS BADGES
============================================================

Create ONE StatusBadge component.

Examples:

PAID
PENDING
OVERDUE
FAILED
REFUNDED

ONLINE
OFFLINE
WARNING
CRITICAL
UNKNOWN

ACTIVE
SUSPENDED
TERMINATED

PENDING
ASSIGNED
IN PROGRESS
COMPLETED

Never create module-specific badge styles.

Same status must always have the same appearance.

============================================================
13. STANDARD COLOR SEMANTICS
============================================================

Success:

green

Warning:

amber/orange

Critical:

red

Info:

blue

Primary:

purple/indigo accent

Neutral:

gray

Billing:

PAID = success
PENDING = info/neutral
OVERDUE = critical
FAILED = critical
REFUNDED = purple/neutral

Network:

ONLINE = success
DEGRADED = warning
OFFLINE = critical
UNKNOWN = neutral

Work Order:

PENDING = neutral
SCHEDULED = blue
ASSIGNED = purple
EN ROUTE = cyan/blue
IN PROGRESS = amber
COMPLETED = green
FAILED = red

Never change these meanings from page to page.

============================================================
14. STANDARD CARD
============================================================

Create one reusable Card pattern.

Card:

rounded-md / rounded-lg
subtle border
dark background
small shadow where appropriate

Header:

title
description
optional action

Content:

consistent padding

Footer:

optional actions

Do not use excessive rounded-xl/2xl/3xl cards.

============================================================
15. STANDARD FILTERS
============================================================

Use shared:

SearchInput
FilterButton
StatusFilter
DateRangeFilter
SelectFilter
ComboboxFilter
ResetFilters

All pages must behave consistently.

Filter state should be URL-persisted where appropriate.

============================================================
16. STANDARD DRAWER / SHEET
============================================================

Use shadcn Sheet for quick detail.

Examples:

Customer quick view
ONU quick view
OLT quick view
Invoice quick view
Technician quick view
Ticket quick view

Structure:

SheetHeader
Summary
Tabs/sections
Actions

Do not create custom drawer designs per module.

============================================================
17. STANDARD DIALOG
============================================================

Use shadcn Dialog for:

Create
Edit
Delete confirmation
Approve
Reject
Assign
Suspend
Reactivate
Refund
Cancel

Confirmation dialogs must have:

title
description
impact
cancel
confirm

Destructive actions:

destructive button

============================================================
18. STANDARD FORMS
============================================================

Use:

React Hook Form
Zod
shadcn Form

Every form follows:

PageHeader
Form sections
Card sections
Validation
Action footer

Example:

┌─────────────────────────────────────────────┐
│ Customer Information                        │
├─────────────────────────────────────────────┤
│ Name                                        │
│ [____________________________]              │
│                                             │
│ Phone                                       │
│ [____________________________]              │
│                                             │
│ Email                                       │
│ [____________________________]              │
└─────────────────────────────────────────────┘

Form sections:

Customer Information
Service Information
Billing Information
Network Information
Additional Information

Do not put all fields into one giant unstructured form.

============================================================
19. STANDARD FORM FOOTER
============================================================

Create/edit pages use a consistent footer:

[Cancel]                    [Save Changes]

For long forms:

sticky bottom action bar.

For destructive editing:

[Cancel] [Save Changes]

Never move the primary action randomly.

============================================================
20. STANDARD TABS
============================================================

Detail pages use shadcn Tabs.

Example Customer:

Overview
Subscriptions
Invoices
Payments
Network
Tickets
Work Orders
Activity

Example OLT:

Overview
Cards
PON
ONU
Uplinks
Alarms
Metrics
Topology
Customers
Audit

Same tab styling everywhere.

============================================================
21. STANDARD EMPTY STATE
============================================================

Create one EmptyState component.

Example:

No invoices found

There are no invoices matching your filters.

[Clear Filters]

For first-time setup:

No OLTs configured

Add your first ZTE OLT to start monitoring.

[+ Add OLT]

Use consistent:

icon
title
description
action

============================================================
22. STANDARD LOADING STATE
============================================================

Create reusable:

PageSkeleton
CardSkeleton
TableSkeleton
ChartSkeleton
DetailSkeleton

Use shadcn Skeleton.

Never show a blank screen during loading.

============================================================
23. STANDARD ERROR STATE
============================================================

Create reusable ErrorState.

Example:

Unable to load invoices

We couldn't retrieve the invoice data.

[Try Again]

For network:

Unable to connect to OLT

The OLT monitoring service is unavailable.

[Retry]

============================================================
24. STANDARD TOASTS
============================================================

Use one toast system.

Success:

Customer created successfully.

Payment:

Payment recorded successfully.

Network:

OLT synchronization completed.

Error:

Unable to synchronize OLT.

Never use different toast designs.

============================================================
25. STANDARD NOTIFICATIONS
============================================================

Use one NotificationCenter.

Notification categories:

Billing
Payment
Network
Incident
Ticket
Work Order
PSB
System

All use the same notification item layout.

============================================================
26. STANDARD SEARCH
============================================================

Use one global Command component.

Ctrl/Cmd + K.

Search all major entities.

Search result structure:

icon
entity type
name
metadata
shortcut/action

Examples:

Customer
Invoice
OLT
ONU
Ticket
Work Order

============================================================
27. STANDARD CHARTS
============================================================

Use one chart design system.

Charts must share:

font
axis style
tooltip
grid
legend
colors
spacing

Use:

Recharts
shadcn chart patterns

Primary chart color:

purple/indigo

Success:

green

Warning:

amber

Critical:

red

Do not use random palettes on different pages.

============================================================
28. STANDARD PAYMENT UI
============================================================

Payment cards, payment table, transaction detail and payment gateway
must use the same Card/Table/Badge patterns.

Payment method cards:

QRIS
Virtual Account
E-Wallet
Card
Bank Transfer

All use same dimensions.

============================================================
29. STANDARD NETWORK UI
============================================================

Network pages MUST NOT introduce a separate NOC design system.

OLT
PON
ONU
MikroTik
RADIUS
IPAM
VLAN

must use the same:

PageHeader
MetricCard
FilterToolbar
DataTable
StatusBadge
Sheet
Dialog
Tabs

Only the data/content changes.

============================================================
30. STANDARD OLT UI
============================================================

OLT Management:

PageHeader
KPI Cards
FilterToolbar
DataTable

OLT Detail:

PageHeader
Summary Metrics
Tabs
Cards

Same layout rules as Customer and Invoice details.

============================================================
31. STANDARD TOPOLOGY UI
============================================================

Topology is a specialized canvas.

However, surrounding UI MUST remain consistent:

same topbar
same sidebar
same buttons
same badges
same dialogs
same sheets
same filters

React Flow canvas may have its own visualization, but controls must
use shadcn components.

============================================================
32. STANDARD NOC UI
============================================================

NOC can be denser than billing pages.

But use the same:

Card
Badge
Button
Table
Sheet
Dialog
Tabs
Typography
Spacing
Color tokens

NOC is not allowed to introduce another design system.

============================================================
33. STANDARD DISPATCH UI
============================================================

Dispatch may use:

map
calendar
technician lanes

But all panels use the same Card and Sheet patterns.

Technician cards must use:

avatar
name
status badge
location
job count
current job

============================================================
34. STANDARD MOBILE UI
============================================================

Mobile must preserve the same design language.

Use:

same typography
same badges
same buttons
same colors
same cards

Only layout changes.

Desktop:

sidebar

Mobile:

drawer/bottom navigation where appropriate.

============================================================
35. STANDARD CUSTOMER PORTAL
============================================================

Customer Portal can simplify navigation, but must retain the same
brand and visual language.

Use:

same shadcn components
same colors
same cards
same status badges
same typography

Do not create a completely different consumer UI.

============================================================
36. STANDARD PARTNER PORTAL
============================================================

Partner Portal also uses the same design system.

Only navigation and permissions differ.

============================================================
37. DESIGN TOKENS
============================================================

Create a central token definition.

Files should include something similar to:

resources/js/design-system/
  tokens.ts
  colors.ts
  spacing.ts
  typography.ts
  status.ts

Centralize:

colors
spacing
radius
shadows
typography
status semantics
breakpoints

No page should define arbitrary design values unless required by a
specialized visualization.

============================================================
38. SHARED COMPONENT LIBRARY
============================================================

Create application-specific components on top of shadcn:

AppShell
Sidebar
Topbar
PageHeader
PageContainer
MetricCard
SectionCard
StatusBadge
DataTable
DataTableToolbar
DataTablePagination
FilterToolbar
SearchInput
EmptyState
ErrorState
LoadingState
ConfirmDialog
DetailSheet
FormSection
FormActions
StatGroup
ActivityTimeline
NotificationCenter
RealtimeIndicator
CommandPalette
DateRangePicker
EntityAvatar
EntityStatus
NetworkHealthCard
PaymentStatus
InvoiceStatus
WorkOrderStatus
NetworkStatus
ChartCard
MapPanel
Timeline
FileUpload
ImagePreview
SignaturePad

These components become the approved building blocks.

============================================================
39. PAGE IMPLEMENTATION RULE
============================================================

Before implementing any new page:

1. Identify the standard page pattern.
2. Reuse existing shared components.
3. Do not create a new visual pattern if an existing one fits.
4. Only create a new component when there is a real reusable need.
5. Add the new component to the design system if it will be reused.

Example:

New ODP page

MUST reuse:

AppShell
PageHeader
MetricCard
FilterToolbar
DataTable
StatusBadge
DetailSheet

Do not create:

ODPTable
ODPCard
ODPStatusBadge

unless there is a genuinely reusable specialized behavior that cannot
be represented by the standard components.

============================================================
40. ROUTE-TO-UI CONSISTENCY
============================================================

All routes should follow predictable visual rules.

Examples:

/dashboard
/customers
/customers/{id}
/subscriptions
/invoices
/invoices/{id}
/payments
/payments/{id}
/olts
/olts/{id}
/pons
/onus
/onus/{id}
/topology
/tickets
/tickets/{id}
/work-orders
/work-orders/{id}
/technicians
/technicians/{id}
/dispatch
/schedules
/reports

List routes:

PageHeader
KPI
Toolbar
Table

Detail routes:

PageHeader
Summary
Tabs

Create/edit:

PageHeader
Form
Actions

============================================================
41. RESPONSIVE CONSISTENCY
============================================================

Breakpoints must be consistent.

Use Tailwind standard breakpoints.

Desktop:
full sidebar + multi-column

Tablet:
collapsed sidebar + responsive grid

Mobile:
drawer + stacked content

Tables:
responsive scroll/card transformation

Charts:
responsive width

Cards:
grid collapse

Do not make individual pages invent their own breakpoints.

============================================================
42. DARK MODE CONSISTENCY
============================================================

Default:

Dark

Every page must use the same dark background.

Avoid:

one page pure black
another page dark gray
another page blue-gray

Use centralized shadcn CSS variables.

Example:

background
card
popover
muted
border
foreground

============================================================
43. LIGHT MODE CONSISTENCY
============================================================

Light mode must use the same layout and component system.

Only colors change.

Do not redesign pages between light and dark.

============================================================
44. REALTIME CONSISTENCY
============================================================

Realtime updates must use the same visual patterns.

Examples:

Payment received:
toast + table update + KPI update

OLT offline:
status badge + alarm + notification + NOC update

ONU LOS:
status badge + alarm + affected customer update

Work Order assigned:
notification + schedule update + technician update

No custom realtime animations per module.

============================================================
45. ACCESSIBILITY CONSISTENCY
============================================================

All shared components must support:

keyboard navigation
focus states
screen readers
ARIA
contrast
reduced motion

Do not rely only on color.

============================================================
46. UI QA CHECKLIST
============================================================

For EVERY page verify:

[ ] Same sidebar
[ ] Same topbar
[ ] Same page header
[ ] Same typography
[ ] Same spacing
[ ] Same card style
[ ] Same button style
[ ] Same table style
[ ] Same filters
[ ] Same badge style
[ ] Same dialog
[ ] Same Sheet
[ ] Same loading state
[ ] Same empty state
[ ] Same error state
[ ] Same toast
[ ] Same responsive behavior
[ ] Same dark mode
[ ] Same light mode
[ ] Same accessibility behavior

============================================================
47. VISUAL REGRESSION
============================================================

Add visual regression testing for the main shared layouts.

Capture screenshots for:

Dashboard
Customers
Customer Detail
Invoices
Invoice Detail
Payments
OLT
OLT Detail
ONU
Topology
NOC
Work Orders
Dispatch
Technicians
Reports
Settings

Compare against approved baseline.

A new page is not considered UI-complete until it follows the shared
design system.

============================================================
48. FINAL UI ACCEPTANCE
============================================================

The application must pass this visual test:

If the PT Mitra Media Data logo/name is removed from two different
pages, users should still immediately recognize both pages as part of
the same application.

The following must remain visually identical across modules:

Sidebar
Topbar
PageHeader
Buttons
Cards
Tables
Filters
Badges
Tabs
Sheets
Dialogs
Forms
Toasts
Charts
Spacing
Typography
Status semantics

Only the content changes.

============================================================
END OF MASTER UI CONSISTENCY STANDARD
============================================================
