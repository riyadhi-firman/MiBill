# PT Mitra Media Data — ISP & FTTH Management Platform

> Modern ISP OSS/BSS, Billing, Network Management, FTTH Topology, NOC, and Field Service Platform.

[![UI](https://img.shields.io/badge/UI-shadcn%2Fui-black?style=flat-square)](https://ui.shadcn.com/)
[![Frontend](https://img.shields.io/badge/Frontend-React%20%2B%20TypeScript-61DAFB?style=flat-square)](https://react.dev/)
[![Backend](https://img.shields.io/badge/Backend-Laravel-F9322C?style=flat-square)](https://laravel.com/)
[![Network Engine](https://img.shields.io/badge/Network-Go-00ADD8?style=flat-square)](https://go.dev/)
[![Database](https://img.shields.io/badge/Database-PostgreSQL-4169E1?style=flat-square)](https://www.postgresql.org/)
[![Cache](https://img.shields.io/badge/Cache-Redis-DC382D?style=flat-square)](https://redis.io/)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](#license)

---

## Overview

**PT Mitra Media Data — ISP & FTTH Management Platform** is a unified platform designed to manage the complete lifecycle of an ISP/FTTH operation.

The platform combines:

- Billing & invoicing
- Customer management
- Subscription management
- Payment gateway
- RADIUS
- MikroTik
- ZTE OLT
- PON & ONU monitoring
- IPAM & VLAN
- FTTH topology
- ODC / ODP / fiber infrastructure
- NOC & network alarms
- Incidents & tickets
- PSB / new customer provisioning
- Technician management
- Work orders
- Scheduling
- Dispatch
- Partner management
- Customer portal
- Realtime operations
- Reporting & analytics

The goal is to provide **one consistent operating platform for the business, network, and field teams**.

---

## Design Philosophy

The application uses a **premium dark billing/finance dashboard style built with shadcn/ui**.

The main application is **billing-first**, not NOC-first.

The visual hierarchy is:

```text
Revenue
   ↓
Customers
   ↓
Subscriptions
   ↓
Invoices
   ↓
Payments
   ↓
Outstanding
   ↓
Operations
   ↓
Network
   ↓
NOC
```

Network operations remain deeply integrated, but the overall product should feel like a modern commercial ISP management and billing platform.

### UI principles

- shadcn/ui as the primary design system
- dark mode first
- light mode supported
- compact enterprise layout
- consistent sidebar
- consistent topbar
- consistent page header
- consistent cards
- consistent DataTables
- consistent status badges
- consistent forms
- consistent dialogs and sheets
- consistent spacing and typography
- responsive desktop/tablet/mobile layouts
- accessibility-first components
- realtime status indicators
- minimal visual noise

---

## Core Modules

### Dashboard

- Revenue overview
- Customer overview
- Subscription metrics
- Invoice status
- Payment status
- Outstanding balance
- Customer growth
- Network health
- Active alarms
- Technician status
- Recent activity

### Customer Management

- Customer CRUD
- Customer 360
- Customer contacts
- Customer addresses
- Service history
- Billing history
- Payment history
- Network status
- Tickets
- Incidents
- Work orders
- Activity timeline

### Subscription

Support:

- Static IP
- DHCP
- PPPoE
- Hotspot

Subscription management includes:

- Package
- Billing cycle
- IP assignment
- VLAN
- RADIUS profile
- MikroTik profile
- Activation
- Suspension
- Reactivation
- Termination

### Billing

- Invoices
- Invoice items
- Recurring billing
- Outstanding invoices
- Overdue invoices
- Payment history
- Refunds
- Credit notes
- FUP management
- Financial reports

### Payment Gateway

Planned integrations:

- Midtrans
- Xendit

Payment methods:

- QRIS
- Virtual Account
- Bank Transfer
- E-Wallet
- Card

Includes:

- transaction management
- webhook processing
- signature verification
- idempotency
- retries
- payment reconciliation
- audit logs

---

# Network Management

## ZTE OLT Integration

ZTE OLT monitoring is based on:

**`github.com/Cepat-Kilat-Teknologi/snmp-olt-zte@v3.2.0`**

Repository:

https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte

Required release:

https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte/releases/tag/v3.2.0

### Supported ZTE models

- ZTE C300
- ZTE C320

### v3.2.0 capabilities used by this platform

- Multi-OLT in a single instance
- Per-tenant API keys
- Per-OLT SNMP configuration
- Per-OLT Redis cache namespace
- Per-slot PON topology
- C300/C320 support
- Card auto-detection
- Uplink auto-detection
- ENTITY-MIB discovery
- IF-MIB discovery
- `gei` 1G detection
- `xgei` 10G detection
- SNMP connection pooling
- Bounded SNMP concurrency
- Redis caching
- Cache pre-warming
- Singleflight request deduplication
- Batched SNMP GET
- BulkWalk
- Prometheus metrics
- SNMP Trap support
- ONU offline detection
- RX power monitoring
- Configurable RX thresholds
- OpenAPI specification
- Health/readiness endpoints

### ZTE architecture

```text
┌─────────────────────────────┐
│           React             │
│       shadcn/ui             │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│          Laravel            │
│       OSS / BSS / CRM       │
└──────────────┬──────────────┘
               │
          ZteOltClient
               │
               ▼
┌─────────────────────────────┐
│     snmp-olt-zte v3.2.0     │
│             Go              │
└──────────────┬──────────────┘
               │
             SNMP
               │
        ┌──────┴──────┐
        │             │
    ZTE C300      ZTE C320
```

The Laravel application owns business logic, customers, billing, RBAC,
topology relationships, incidents, work orders, and audit records.

The ZTE adapter owns ZTE SNMP communication and monitoring functions.

The platform does **not** reimplement the ZTE OID/SNMP engine when the
upstream adapter already provides the required capability.

---

## OLT Management

OLT management includes:

- OLT registry
- C300/C320 support
- Multi-OLT
- Health status
- Board/card discovery
- PON discovery
- ONU monitoring
- Uplink discovery
- RX monitoring
- Alarm integration
- Topology relationship
- Customer impact analysis
- Audit trail

### Example OLT hierarchy

```text
POP
 │
 └── OLT
      │
      ├── Slot / Card
      │     │
      │     └── PON
      │           │
      │           └── ONU
      │                 │
      │                 └── Customer
      │
      └── Uplink
```

---

## PON Management

- PON health
- ONU count
- Online/offline
- LOS
- Optical power
- Alarms
- Customer impact
- Topology trace

---

## ONU Management

ONU information may include:

- ONU ID
- Serial number
- ONU type
- Customer
- OLT
- Slot
- PON
- ODC
- ODP
- RX power
- TX power where available
- Temperature where available
- Distance where available
- Status
- Last online
- Last offline

Large ONU lists must use server-side pagination.

---

# MikroTik Integration

Supported integration methods:

- RouterOS API
- REST
- SSH fallback

Management areas:

- Interfaces
- VLAN
- Routes
- ARP
- DHCP
- PPPoE
- Hotspot
- Queues
- Address lists
- Health
- Backups

---

# RADIUS

RADIUS integration supports:

- PPPoE
- Hotspot
- Authentication
- Accounting
- Session monitoring
- NAS management
- User management

Session information:

```text
Username
NAS
IP Address
Start Time
Stop Time
Duration
Upload
Download
Status
```

---

# IPAM & VLAN

## IPAM

Support:

- IPv4
- IPv6
- Pools
- Subnets
- IP allocation
- Reservation
- Allocation history

Service types:

- Static
- DHCP
- PPPoE
- Hotspot
- CGNAT
- IPv6

## VLAN

Manage:

- VLAN ID
- Name
- Purpose
- Region
- POP
- OLT
- Service

Example:

```text
VLAN 165 → Static Internet
VLAN 144 → Hotspot
VLAN 100 → TR-069
```

---

# FTTH Infrastructure

## Topology

The platform models:

```text
OLT
  ↓
PON
  ↓
ODC
  ↓
Fiber
  ↓
ODP
  ↓
ODP Port
  ↓
ONU
  ↓
Customer
```

Topology visualization uses **React Flow**.

Features:

- Interactive topology
- Trace path
- Customer trace
- OLT trace
- Impact analysis
- Node status
- Alarm state
- Customer count
- Network dependency mapping

## ODC

- ODC registry
- Fiber core capacity
- Used cores
- Available cores
- Connected ODP
- Customer impact
- Map
- Maintenance

## ODP

- ODP registry
- Port capacity
- Port status
- Customer assignment
- ONU relationship
- Topology
- Maintenance

## Fiber

- Fiber cable
- Fiber core
- Splice
- Joint closure
- Splitter
- Fiber status
- Fiber topology

---

# NOC Command Center

The NOC is a dedicated operational module using the same global
shadcn/ui design system.

Monitoring includes:

- OLT
- PON
- ONU
- RADIUS
- MikroTik
- Network alarms
- Incidents
- Affected customers
- Service availability

### Alarm examples

```text
CRITICAL
OLT OFFLINE

CRITICAL
PON DOWN

WARNING
ONU LOW RX

WARNING
ONU LOS

INFO
RADIUS AUTH FAILURE
```

### Impact analysis

The platform can calculate:

```text
OLT DOWN
   ↓
PON
   ↓
ODC
   ↓
ODP
   ↓
ONU
   ↓
Customers
   ↓
Potential revenue impact
```

---

# Operations

## PSB / New Customer

Workflow:

```text
Lead
  ↓
Survey
  ↓
Approved
  ↓
Scheduled
  ↓
Installation
  ↓
Testing
  ↓
Activation
  ↓
Completed
```

## Tickets

- Customer tickets
- Network tickets
- Billing tickets
- Technical support
- SLA
- Assignment
- Timeline

## Incidents

- Critical
- Major
- Minor
- Info
- Root cause
- Affected services
- Affected customers
- Timeline
- Work order

---

# Field Service

## Technician

Manage:

- Technician profile
- Skills
- Team
- Availability
- Location
- Current job
- Performance
- SLA

## Work Orders

Statuses:

```text
Pending
Scheduled
Assigned
En Route
Arrived
In Progress
Waiting
Completed
Failed
```

Work order supports:

- Customer
- Location
- Technician
- Schedule
- SLA
- Checklist
- Materials
- Tools
- Photos
- Measurements
- Notes
- Customer signature
- Timeline

## Dispatch Center

Dispatch combines:

- Work orders
- Technician availability
- Map
- Schedule
- SLA
- Distance
- Skills
- Workload

Recommended technician scoring:

```text
Skill
+ Availability
+ Distance
+ Workload
+ SLA
+ Region
```

---

# Partner Portal

Partners can manage:

- Customers
- PSB
- Installation
- Revenue
- Commission
- Outstanding balance

---

# Customer Portal

Customer-facing dashboard:

- Internet status
- Package
- Usage
- Invoice
- Payment
- Network
- Ticket
- Work order

Primary action:

**Bayar Sekarang**

---

# Realtime Architecture

Realtime events use:

```text
ZTE / MikroTik / RADIUS / Payment
             │
             ▼
        Go / Laravel
             │
             ▼
           Redis
             │
             ▼
       Event / Queue
             │
             ▼
      Laravel Reverb
             │
             ▼
           React
```

Realtime events may include:

- OLT status
- PON status
- ONU status
- LOS
- RX threshold
- Network alarms
- Incidents
- Payments
- Work orders
- Technician status
- Notifications

The UI must display a clear:

```text
● LIVE
```

indicator.

If disconnected:

```text
● REALTIME DISCONNECTED
```

---

# Technology Stack

## Frontend

| Technology | Purpose |
|---|---|
| React | UI |
| TypeScript | Type safety |
| Inertia.js | SPA experience |
| Tailwind CSS | Styling |
| shadcn/ui | Design system |
| TanStack Table | Enterprise tables |
| React Hook Form | Forms |
| Zod | Validation |
| React Flow | FTTH topology |
| Recharts | Charts |
| FullCalendar | Scheduling |
| MapLibre / Leaflet | Maps |
| Lucide | Icons |

## Backend

| Technology | Purpose |
|---|---|
| Laravel | OSS/BSS/business backend |
| Go | Network engine |
| PostgreSQL | Main database |
| PostGIS | Geospatial data |
| Redis | Cache/events/queues |
| Laravel Horizon | Queue management |
| Laravel Reverb | WebSocket/realtime |

## Network

| System | Integration |
|---|---|
| ZTE C300 | SNMP via snmp-olt-zte v3.2.0 |
| ZTE C320 | SNMP via snmp-olt-zte v3.2.0 |
| MikroTik | API / REST / SSH |
| RADIUS | Authentication/accounting |
| SNMP | Network monitoring |
| ICMP | Reachability |

## Infrastructure

- Docker
- Docker Compose
- Nginx
- Prometheus
- Grafana
- CI/CD

---

# Architecture

```text
                         INTERNET
                            │
                         NGINX
                            │
              ┌─────────────┴─────────────┐
              │                           │
              ▼                           ▼
        React + Inertia               API / Auth
              │                           │
              └──────────────┬────────────┘
                             │
                          Laravel
                             │
          ┌──────────────────┼──────────────────┐
          │                  │                  │
          ▼                  ▼                  ▼
      PostgreSQL           Redis             Reverb
          │                  │                  │
          │                  │                  ▼
          │                  │               React
          │                  │
          │           ┌──────┴──────┐
          │           │             │
          ▼           ▼             ▼
      Business      Queues      Network Events
                                   │
                                   ▼
                              Go Network
                                 Engine
                                   │
             ┌─────────────────────┼─────────────────────┐
             │                     │                     │
             ▼                     ▼                     ▼
      snmp-olt-zte              MikroTik             RADIUS
          v3.2.0
             │
       ┌─────┴─────┐
       ▼           ▼
    ZTE C300     ZTE C320
```

---

# Project Structure

Recommended monorepo:

```text
isp-platform/
├── apps/
│   ├── api/
│   ├── web/
│   └── network-engine/
│
├── packages/
│   └── shared-types/
│
├── database/
│
├── docs/
│
├── infra/
│
├── scripts/
│
├── docker-compose.yml
├── .env.example
├── README.md
├── TASK.md
├── DESIGN.md
├── ERD.md
├── API.md
├── ARCHITECTURE.md
├── NETWORK.md
├── ZTE-OLT.md
├── MIKROTIK.md
├── RADIUS.md
├── TOPOLOGY.md
├── NOC.md
├── TECHNICIAN.md
├── SCHEDULING.md
├── WORK-ORDER.md
├── PROVISIONING.md
├── SECURITY.md
└── DEPLOYMENT.md
```

---

# UI Consistency Standard

Every page must use the same application shell and shared components.

```text
AppShell
├── Sidebar
├── Topbar
└── Main
    ├── Breadcrumb
    ├── PageHeader
    └── PageContent
```

Shared components include:

- `AppShell`
- `Sidebar`
- `Topbar`
- `PageHeader`
- `MetricCard`
- `StatusBadge`
- `DataTable`
- `FilterToolbar`
- `DetailSheet`
- `ConfirmDialog`
- `FormSection`
- `FormActions`
- `EmptyState`
- `ErrorState`
- `LoadingState`
- `NotificationCenter`
- `RealtimeIndicator`
- `CommandPalette`
- `ChartCard`
- `NetworkHealthCard`

### Standard list page

```text
Page Header
     ↓
KPI Summary
     ↓
Filter Toolbar
     ↓
DataTable
     ↓
Pagination
```

### Standard detail page

```text
Page Header
     ↓
Summary
     ↓
Tabs
     ↓
Content Cards
```

### Standard create/edit page

```text
Page Header
     ↓
Form Sections
     ↓
Sticky Action Footer
```

This prevents every module from developing a different UI language.

---

# Security

Security requirements include:

- RBAC
- 2FA
- CSRF protection
- XSS protection
- SQL injection protection
- API authentication
- rate limiting
- secure headers
- webhook signature verification
- tenant isolation
- audit logging
- encrypted credentials

Never expose or log:

- SNMP communities
- API keys
- RADIUS shared secrets
- SSH credentials
- payment gateway secrets

---

# Realtime & Reliability

Network operations must implement:

- timeout
- retry
- exponential backoff
- circuit breaker
- bounded concurrency
- structured logging
- correlation IDs
- health checks
- readiness checks
- metrics

The application must not report a device as online merely because it
exists in the database.

---

# Development

## Requirements

Recommended environment:

- PHP 8.3+
- Composer
- Node.js LTS
- npm / pnpm
- Go
- PostgreSQL
- Redis
- Docker
- Docker Compose

For ZTE monitoring:

- ZTE C300 or C320
- SNMP v2c
- network access from the ZTE adapter to the OLT

---

# Development Workflow

```bash
# Clone
git clone <repository-url>
cd isp-platform

# Environment
cp .env.example .env

# Install backend
composer install

# Install frontend
npm install

# Generate application key
php artisan key:generate

# Database
php artisan migrate --seed

# Start development
composer run dev
```

The exact commands should be updated to match the final repository
structure.

---

# ZTE Adapter

The required ZTE adapter version is:

```text
github.com/Cepat-Kilat-Teknologi/snmp-olt-zte@v3.2.0
```

Do not silently replace it with another version.

Before modifying the ZTE integration:

1. Read the upstream README.
2. Read the v3.2.0 release notes.
3. Read the OpenAPI specification.
4. Verify endpoint and response contracts.
5. Use the adapter rather than duplicating its OID implementation.

Reference:

https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte

Release:

https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte/releases/tag/v3.2.0

---

# API Integration Pattern

Laravel should communicate with the ZTE adapter through an internal
service client.

Example:

```text
Laravel
   │
   ▼
ZteOltClientInterface
   │
   ▼
SnmpOltZteClient
   │
   ▼
snmp-olt-zte v3.2.0
```

Example operations:

```text
listOlts()
getOlt()
getHealth()
getUplinks()
getBoards()
getPons()
getOnus()
getOnu()
getAlarms()
getMetrics()
```

The frontend must never receive the adapter's private credentials.

---

# Testing

Testing should cover:

### Backend

- Unit tests
- Feature tests
- API tests
- Database tests
- Authorization tests

### Frontend

- Component tests
- Form validation
- UI interaction
- Responsive behavior
- Accessibility

### Network

- ZTE adapter contract tests
- C300
- C320
- Multi-OLT
- Per-tenant access
- Slot/PON validation
- Uplink detection
- ONU monitoring
- OLT health
- Redis isolation
- Realtime events

### Integration

- Payment gateway
- RADIUS
- MikroTik
- ZTE
- Provisioning
- Rollback
- Webhooks

---

# CI/CD

Recommended pipeline:

```text
Push
 │
 ├── Lint
 ├── Type Check
 ├── Unit Tests
 ├── Integration Tests
 ├── Build
 ├── Security Checks
 ├── Docker Build
 └── Deploy
```

Production deployment should require passing tests and build checks.

---

# Roadmap

- [ ] Project foundation
- [ ] Authentication
- [ ] RBAC
- [ ] shadcn/ui design system
- [ ] Dashboard
- [ ] Customer management
- [ ] Subscription management
- [ ] Billing
- [ ] Payment gateway
- [ ] RADIUS
- [ ] MikroTik
- [ ] ZTE C300/C320 integration
- [ ] Multi-OLT
- [ ] PON
- [ ] ONU
- [ ] IPAM
- [ ] VLAN
- [ ] ODC
- [ ] ODP
- [ ] Fiber
- [ ] FTTH topology
- [ ] NOC
- [ ] Alarm correlation
- [ ] Incident management
- [ ] Ticketing
- [ ] PSB
- [ ] Technician
- [ ] Work order
- [ ] Scheduling
- [ ] Dispatch
- [ ] Partner portal
- [ ] Customer portal
- [ ] Realtime
- [ ] Reporting
- [ ] Observability
- [ ] Production deployment

---

# Documentation

The repository should maintain detailed documentation:

| Document | Description |
|---|---|
| `TASK.md` | Development task backlog |
| `DESIGN.md` | UI/UX and design system |
| `ERD.md` | Database entity relationship |
| `API.md` | Application API |
| `ARCHITECTURE.md` | System architecture |
| `NETWORK.md` | Network architecture |
| `ZTE-OLT.md` | ZTE integration |
| `MIKROTIK.md` | MikroTik integration |
| `RADIUS.md` | RADIUS integration |
| `TOPOLOGY.md` | FTTH topology |
| `NOC.md` | NOC operations |
| `TECHNICIAN.md` | Technician management |
| `SCHEDULING.md` | Scheduling |
| `WORK-ORDER.md` | Work order |
| `PROVISIONING.md` | Service provisioning |
| `SECURITY.md` | Security architecture |
| `DEPLOYMENT.md` | Deployment guide |

---

# Contributing

1. Create a feature branch.
2. Follow the existing architecture.
3. Reuse shared shadcn/ui components.
4. Do not introduce a second UI design system.
5. Add tests.
6. Update documentation.
7. Update `TASK.md`.
8. Submit a pull request.

For UI changes, ensure that the new page follows the shared design
system and does not introduce a module-specific visual language.

---

# License

This project is intended for PT Mitra Media Data and its authorized
development/operational use.

The final repository license should be selected by the project owner
before public distribution.

---

# Acknowledgements

This project uses and integrates with open-source technologies
including:

- React
- Laravel
- Go
- PostgreSQL
- Redis
- shadcn/ui
- Tailwind CSS
- TanStack Table
- React Flow
- Recharts
- FullCalendar
- MapLibre
- Prometheus

ZTE monitoring integration is based on:

**Cepat-Kilat-Teknologi/snmp-olt-zte v3.2.0**

https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte

---

## PT Mitra Media Data

**ISP & FTTH Management Platform**

> One platform for customers, billing, network, operations, and field service.
