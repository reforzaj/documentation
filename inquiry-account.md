``` mermaid
sequenceDiagram
    autonumber
    title: Inquiry Account
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal
    participant d as SNAP Core

    a->>b: Request Inquiry Account
    b->>c: Request Inquiry Account
    c->>d: Request Inquiry Account
    d->>c: Return Inquiry Account results
    c->>c: Validate accountName vs accountNameActual
    alt accountName is same as accountNameActual
    c->>b: Return Response "status = VALID"
    b->>a: Return Response "status = VALID"
    else accountName is not same as accountNameActual
    c->>b: Return Response "status = WARNING"
    b->>a: Return Callback Results "WARNING" 
    else accountNumber is not exist
    c->>b: Return Response "status = INVALID"
    b->>a: Return Callback Results "INVALID" 
    end
```
