# DESIGN.md — PT MITRA MEDIA DATA UI/UX

## 1. DESIGN GOAL

Create one unified premium ISP/FTTH enterprise application.

Visual direction:

```text
Dark shadcn/ui
+
Premium Billing Dashboard
+
Network Operations
+
Modern SaaS
```

The supplied UI reference image is the visual benchmark.

Do not create different themes for different modules.

---

## 2. BRAND

```text
PT Mitra Media Data
```

Use the name consistently.

---

## 3. APP SHELL

```text
Sidebar
   +
Topbar
   +
Breadcrumb
   +
Page Header
   +
KPI
   +
Charts
   +
Tables
```

All pages use the same shell.

---

## 4. SIDEBAR

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

## 5. TOPBAR

```text
Search
⌘K
Notifications
Realtime
Theme
Tenant
User
```

---

## 6. DESIGN TOKENS

Use centralized shadcn tokens:

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

Use Tailwind utilities and CSS variables.

---

## 7. CARDS

Cards:

```text
rounded-xl
subtle border
compact padding
clear header
dark surface
```

Types:

```text
MetricCard
ChartCard
DataCard
StatusCard
```

---

## 8. KPI

Example:

```text
Active Sessions
4,821
↑ 12.5%
```

Keep cards compact.

---

## 9. TABLES

Use TanStack Table.

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

Status badges:

```text
ACTIVE
ONLINE
SUSPENDED
OFFLINE
WARNING
PENDING
```

---

## 10. FORMS

Use:

```text
React Hook Form
Zod
shadcn/ui
```

Forms use sections:

```text
General
Service
Network
Billing
Advanced
```

---

## 11. RADIUS DASHBOARD

KPI:

```text
Active Sessions
Auth Success
Auth Reject
RADIUS Requests
NAS Online
Traffic
```

Charts:

```text
Authentication Trend
Session Trend
Traffic Trend
```

Tables:

```text
Active Sessions
Recent Authentication
Recent Accounting
CoA/Disconnect
```

---

## 12. BILLING DASHBOARD

KPI:

```text
Revenue
Paid
Unpaid
Overdue
MRR
Active Customers
```

Charts:

```text
Revenue Trend
Payment Methods
Invoice Status
```

---

## 13. CUSTOMER DASHBOARD

KPI:

```text
Total
Active
Suspended
New
Online
```

Customer 360 tabs:

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

## 14. MIKROTIK DASHBOARD

```text
Routers Online
PPPoE Sessions
Hotspot Users
Traffic
CPU
Memory
```

---

## 15. OLT DASHBOARD

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
ONU
Serial
Customer
PON
Status
RX
TX
Temperature
Uptime
```

---

## 16. TOPOLOGY

Interactive:

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

Features:

```text
zoom
pan
search
filter
node detail
status
alarm
dependency highlight
customer lookup
```

---

## 17. FIELDOPS

Dashboard:

```text
Today's Jobs
Pending
In Progress
Completed
Overdue
Technicians Online
```

Calendar:

```text
Day
Week
Month
```

---

## 18. NOC

KPI:

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

## 19. MONITORING

Pages:

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

Realtime indicator:

```text
● LIVE
```

Fallback:

```text
● REALTIME DISCONNECTED
```

---

## 20. RESPONSIVE

Desktop:
persistent sidebar.

Tablet:
collapsible sidebar.

Mobile:
drawer.

Tables:
horizontal scroll or responsive cards.

---

## 21. ACCESSIBILITY

Implement:

```text
keyboard navigation
focus state
semantic HTML
ARIA
accessible labels
contrast
status text
```

Never rely only on color.

---

## 22. SHARED COMPONENTS

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

---

## 23. VISUAL QA

Before marking UI task DONE:

1. Compare against UI reference.
2. Verify spacing.
3. Verify typography.
4. Verify card treatment.
5. Verify table density.
6. Verify status badges.
7. Verify responsive behavior.
8. Verify loading state.
9. Verify empty state.
10. Verify error state.

Every module must visually belong to the same product.
