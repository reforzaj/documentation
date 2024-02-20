``` mermaid
sequenceDiagram
    autonumber
    title: Payout via Transfer Intrabank (Sesama Bank)
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal
    participant d as SNAP Core
    participant e as Bank

    a->>b: Request payout via Transfer Intrabank
    b->>c: Request payout via Transfer Intrabank
    c->>c: Validate beneficiary account number 
    c->>d: Request Internal account inquiry
    d->>e: Request Internal account inquiry
    e-->>d: Return account result
    d-->>c: Return account result
    alt Account is invalid
    c-->>b: Return error response "Account beneficiary is invalid"
    b-->>a: Return error response "Account beneficiary in invalid"
    else Account is Valid
    c->>d: Request Transfer Intrabank
    d->>e: Request Transfer Intrabank
    e-->>d: Return Transfer status
    d-->>c: Return Transfer status
    c-->>b: Return Transfer status
    b-->>a: Return Transfer status
        alt Didn't receive notification
        d->>e: Request transfer status
        e->>e: Check Transaction status
        e-->>d: Return Transfer status
        d-->>c: Return Transfer status
        c-->>b: Return Transfer status
        b-->>a: Return Transfer status
        end
    end
```
