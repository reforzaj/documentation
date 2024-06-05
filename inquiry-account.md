``` mermaid
sequenceDiagram
    autonumber
    title: Inquiry Account
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal
    participant d as SNAP Core

    a->>b: Request batch Inquiry Account
    b->>c: Request batch Inquiry Account
    c->>d: Request batch Inquiry Account
    d->>c: Return Inquiry Account results
    c->>c: Pooling batch Inquiry Account
    c->>c: Validate accountName vs accountNameActual
    alt accountName is same as accountNameActual
    c->>b: Return Callback Results "Match" 
    b->>a: Return Callback Results "Match"
    else accountName is not same as accountNameActual
    c->>b: Return Callback Results "Not Match" 
    b->>a: Return Callback Results "Not Match" 
    alt GET Inquiry Account Detail
    a->>b: Request GET Inquiry Account Detail
    b->>c: Request GET Inquiry Account Detail
    c->>b: Return Inquiry Account Detail
    b->>a: Return Inquiry Account Detail
    end
    end
```
