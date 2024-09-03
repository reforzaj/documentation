``` mermaid
sequenceDiagram
    autonumber
    title: Update Virtual Account
    participant a as Merchant
    participant b as Payment Gateway
    participant c as SNAP Core
    participant d as Bank
   
    a->>b: Update Virtual Account 
    b->>b: Check eligibility
    b->>c: Request Update VA 
    c->>d: Request Update VA
    d-->>c: Return VA Update results
    c-->>b: Return VA Update results
    b->>b: Update VA information
    b->>a: Return VA Update results
    alt VA is not eligible
    b->>a: Return Failed Response
    end
```
