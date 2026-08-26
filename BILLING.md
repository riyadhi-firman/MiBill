# BILLING.md

## Lifecycle

```text
Invoice Created
 ↓
Pending
 ↓
Paid
```

Overdue:

```text
Due Date
 ↓
Overdue
 ↓
Grace Period
 ↓
Suspension
```

Payment:

```text
Payment Received
 ↓
Invoice Paid
 ↓
Subscription Active
 ↓
RADIUS Active
 ↓
Optional CoA
```

## Requirements

- idempotent payment
- webhook verification
- invoice audit
- subscription state machine
- retry
- notification
- reports
- reconciliation

Never suspend a customer because of temporary infrastructure failure.
