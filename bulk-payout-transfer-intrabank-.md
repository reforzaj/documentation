``` mermaid
sequenceDiagram
    autonumber
    title: Bulk Payout via Transfer Intrabank (Sesama Bank)
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal
    participant d as SNAP Core
    participant e as Bank Acquirer

    a->>b: Request bulk payout via Transfer Intrabank
    b->>c: Request bulk payout via Transfer Intrabank
    c->>c: Validate beneficiary account number
    c->>c: Debulking
    loop 
    c->>d: Request Internal account inquiry
    d->>e: Request Internal account inquiry
    e-->>d: Return account result
    d-->>c: Return account result
    end
    alt Account is invalid
    c-->>b: Return error response "Account beneficiary is invalid"
    b-->>a: Return error response "Account beneficiary in invalid"
    else Account is Valid
    c->>c: Debulking
    loop
    c->>d: Request Transfer Intrabank
    d->>e: Request Transfer Intrabank
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
