``` mermaid
sequenceDiagram
    autonumber
    title: GET Payout by referenceId
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal

    a->>b: GET Payout Detail
    b->>c: GET Payout
    c->>c: check referenceId
    alt referenceId Valid
    c-->>b: Send Payout Detail response
    b->>a: Send Payout Detail response
    end
    alt referenceId Invalid
    c-->>b: Send invalid referenceId response
    b->>a: Send invalid referenceId response
    end
```
