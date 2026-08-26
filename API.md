# API.md

Base:

```text
/api/v1
```

## Auth

```text
POST /auth/login
POST /auth/logout
POST /auth/refresh
POST /auth/forgot-password
```

## Customer

```text
GET /customers
POST /customers
GET /customers/:id
PATCH /customers/:id
DELETE /customers/:id
```

## Subscription

```text
GET /subscriptions
POST /subscriptions
GET /subscriptions/:id
PATCH /subscriptions/:id
POST /subscriptions/:id/suspend
POST /subscriptions/:id/activate
POST /subscriptions/:id/terminate
```

## Billing

```text
GET /invoices
POST /invoices
GET /invoices/:id
GET /payments
POST /payments
POST /payments/webhooks/:provider
```

## RADIUS

```text
GET /radius/users
POST /radius/users
GET /radius/users/:id
PATCH /radius/users/:id
POST /radius/users/:id/suspend
POST /radius/users/:id/activate
POST /radius/users/:id/disconnect
GET /radius/sessions
GET /radius/nas
POST /radius/nas
```

## MikroTik

```text
GET /mikrotik/devices
POST /mikrotik/devices
GET /mikrotik/devices/:id
GET /mikrotik/sessions
GET /mikrotik/devices/:id/health
```

## OLT

```text
GET /olts
POST /olts
GET /olts/:id
GET /olts/:id/pons
GET /olts/:id/onus
GET /onus
GET /onus/:id
```

## Topology

```text
GET /topology
GET /topology/nodes
GET /topology/links
GET /topology/nodes/:id
GET /topology/nodes/:id/dependencies
```

## FieldOps

```text
GET /technicians
GET /technician-schedules
GET /work-orders
POST /work-orders
GET /work-orders/:id
PATCH /work-orders/:id
```

## NOC

```text
GET /tickets
POST /tickets
GET /tickets/:id
PATCH /tickets/:id
GET /incidents
POST /incidents
```

## Response

```json
{
  "data": {},
  "meta": {},
  "error": null
}
```

## Error

```json
{
  "data": null,
  "meta": {},
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid request",
    "details": {}
  }
}
```
