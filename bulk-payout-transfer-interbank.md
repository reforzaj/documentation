``` mermaid
sequenceDiagram
    autonumber
    title: Bulk Payout via Transfer Interbank (Beda Bank)
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal
    participant d as SNAP Core
    participant e as Bank Acquirer
    participant f as Bank Destination

    a->>b: Request bulk payout via Transfer Interbank
    b->>c: Request bulk payout via Transfer Interbank
    c->>c: Validate beneficiary account number 
    c->>c: Debulking
    loop
    c->>d: Request External account inquiry
    d->>e: Request External account inquiry
    e->>f: Request External account inquiry
    f-->>e: Return account result
    e-->>d: Return account result
    d-->>c: Return account result
    end
    alt Account is invalid
    c-->>b: Return error response "Account beneficiary is invalid"
    b-->>a: Return error response "Account beneficiary in invalid"
    else Account is Valid
    c->>c: Debulking
    loop
    c->>d: Request Transfer Interbank
    d->>e: Request Transfer Interbank
    e->>f: Request Transfer Interbank
    f-->>e: Return Transfer status
    e-->>d: Return Transfer status
    d-->>c: Return Transfer status
    end
    c-->>b: Return Bulk Transfer status
    b-->>a: Return Bulk Transfer status
        alt Didn't receive notification
        loop
        c->>d: Request Transfer status
        d->>e: Request Transfer status
        e->>e: Check Transaction status
        e-->>d: Return Transfer status
        d-->>c: Return Transfer status
        end
        c-->>b: Return Bulk Transfer status
        b-->>a: Return Bulk Transfer status
        end
    end
```
