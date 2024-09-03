``` mermaid
sequenceDiagram
    autonumber
    title: Inquiry Virtual Account if we didn't get final status
    participant a as Merchant
    participant b as Payment Gateway
    participant c as SNAP Core
    participant d as Bank
   
    a->>b: GET Virtual Account 
    b->>a: Return VA information
    alt Virtual Account already paid but status is not final
    b->>c: Request Inquiry VA (Via Retool)
    c->>d: Request Inquiry VA
    d-->>c: Return VA Status informaiton
    c-->>b: Return VA Status information
    b->>b: Update VA Status
    end
```
