``` mermaid
sequenceDiagram
    autonumber
    title: Create Payout without OTP
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal

    a->>b: Create Payout request without OTP
    b->>c: Create Payout request
    c->>c: Execute Payout
    c-->>b: Send Success Payout Request Response
    b->>a: Payout Request Response
```
