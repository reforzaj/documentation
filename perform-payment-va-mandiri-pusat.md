``` mermaid
sequenceDiagram
    title: Perform Payment Virtual Account Mandiri Pusat
    autonumber
    participant a as Merchant
    participant b as Payment Gateway
    participant c as SNAP Core
    participant d as Mandiri Pusat
   
    a->>b: Create Payment VA Mandiri Pusat
    b->>c: Request Creaet Payment VA Mandiri Pusat
    c->>c: Generate VA Number
    c->>d: Request Create VA API
    d->>c: Return VA creation result
    c->>b: Return VA creation result
    b->>a: Return VA creation result
    a->>d: Initiate transfer to Virtual Account
    d->>d: Check Bill information
    d-->>a: Show Bill information
    a->>d: Confirm transfer to VA
    d->>c: Send Payment notification
    c-->>d: Return Acknowledgement
    c-->>b: Send Payment notification
    b->>b: Record Payment
    b-->>a: Send Payment notification
    d-->>a: Generate transfer receipt
```
