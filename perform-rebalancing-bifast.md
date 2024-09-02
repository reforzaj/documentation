``` mermaid
sequenceDiagram
    autonumber
    title: Perform Rebalancing via Internal Dashboard
    participant a as Ops Team
    participant b as Internal Dashboard
    participant c as SNAP Core
    participant d as Acquirer

    a->>b: Request transfer Inter Harsya Account
    b->>c: Request transfer BI Fast Transfer 
    c->>d: Request transfer BI Fast Transfer
    d->>d: Process transfer
    d->>c: Return transfer Status
    c->>b: Return transfer Status
    b->>a: Return transfer Status
```
