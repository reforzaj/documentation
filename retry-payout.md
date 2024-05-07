``` mermaid
sequenceDiagram
    autonumber
    title: Retry Payout
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal

    c-->>b: Send Webhook Payout with status "PENDING"
    b->>a: Send Webhook Payout with status "PENDING"
    a->>a: Top Up Balance
    a->>b: Request Retry Payout
    b->>c: Retry Payout
    c->>c: check UUID
    alt UUID Valid
    c-->>b: Send Payout is executing response 
    b->>a: Send Payout is executing response
    end
    alt UUID Invalid
    c-->>b: Send invalid uuid response
    b->>a: Send invalid uuid response
    end
```
