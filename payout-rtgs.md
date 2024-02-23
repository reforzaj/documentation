``` mermaid
sequenceDiagram
    autonumber
    title: Payout via RTGS (Beda Bank)
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal
    participant d as SNAP Core
    participant e as Bank Acquirer
    participant f as RTGS
    participant g as Bank Destination

    a->>b: Request payout via RTGS
    b->>c: Request payout via RTGS
    c->>c: Validate beneficiary account number 
    c->>d: Request External account inquiry
    d->>e: Request External account inquiry
    e->>f: Request External account inquiry
    f->>g: Request External account inquiry
    g-->>f: Return account result
    f-->>e: Return account result
    e-->>d: Return account result
    d-->>c: Return account result
    alt Account is invalid
    c-->>b: Return error response "Account beneficiary is invalid"
    b-->>a: Return error response "Account beneficiary in invalid"
    else Account is Valid
    c->>d: Request Transfer RTGS
    d->>e: Request Transfer RTGS
    e->>f: Request Transfer RTGS
    f->>g: Request Transfer Instruction
    g-->>f : Return Transfer status
    f-->>e: Return Transfer status
    e-->>d: Return Transfer status
    d-->>c: Return Transfer status
    c-->>b: Return Transfer status
    b-->>a: Return Transfer status
        alt Subscribe Notification
        f->>e: Notify Transfer
        e->>d: Notify Transfer
        d->>c: Notify Transfer
        c->>b: Notify Transfer
        b->>a: Notify Transfer 
        end
    end
```
