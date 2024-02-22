``` mermaid
sequenceDiagram
    autonumber
    title: Bulk Payout via BI Fast Transfer (Beda Bank)
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal
    participant d as SNAP Core
    participant e as Bank Acquirer
    participant f as BI Fast
    participant g as Bank Destination

    a->>b: Request bulk payout via Transfer Interbank
    b->>c: Request bulk payout via Transfer Interbank
    c->>c: Validate beneficiary account number 
    c->>d: Request Bulk External account inquiry
    d->>d: Debulking
    loop
    d->>e: Request External account inquiry
    e->>f: Request External account inquiry
    f->>g: Request External account inquiry
    g-->>f: Return account result
    f-->>e: Return account result
    e-->>d: Return account result
    end
    d-->>c: Return bulk account result
    alt Account is invalid
    c-->>b: Return error response "Account beneficiary is invalid"
    b-->>a: Return error response "Account beneficiary in invalid"
    else Account is Valid
    c->>d: Request Bulk Transfer Interbank
    d->>d: Debulking
    loop
    d->>e: Request Transfer Interbank
    e->>f: Request Transfer Interbank
    f->>g: Request Transfer Instruction
    g-->>f : Return Transfer status
    f-->>e: Return Transfer status
    e-->>d: Return Transfer status
    end
    d-->>c: Return Bulk Transfer status
    c-->>b: Return Bulk Transfer status
    b-->>a: Return Bulk Transfer status
        alt Didn't receive notification
        loop
        d->>e: Request transfer status
        e->>e: Check Transaction status
        e-->>d: Return Transfer status
        end
        d-->>c: Return Bulk Transfer status
        c-->>b: Return Bulk Transfer status
        b-->>a: Return Bulk Transfer status
        end
    end
```
