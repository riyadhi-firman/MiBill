# PAYMENT.md

Use provider adapters.

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
Receive
 ↓
Verify Signature
 ↓
Validate
 ↓
Idempotency Check
 ↓
Persist
 ↓
Update Invoice
 ↓
Update Subscription
 ↓
Network/RADIUS Action
 ↓
Notification
```

Never trust unsigned/unverified payment events.
