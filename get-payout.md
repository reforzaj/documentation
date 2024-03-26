``` mermaid
sequenceDiagram
    autonumber
    title: GET Payout by UUID
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal

    a->>b: GET Payout Detail
    b->>c: GET Payout
    c->>c: check UUID
    alt UUID Valid
    c-->>b: Send Payout Detail response
    b->>a: Send Payout Detail response
    end
    alt UUID Invalid
    c-->>b: Send invalid uuid response
    b->>a: Send invalid uuid response
    end
```
