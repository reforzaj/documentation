``` mermaid
sequenceDiagram
    autonumber
    title: QRIS MPM Flow
    participant a as Customer
    participant b as Merchant
    participant c as Payment Gateway
    participant d as Acquirer

    a->>b: Request payment with QRIS
    b->>c: Request Generate QRIS
    c->>d: Request Generate QRIS
    d->>d: Generate QRIS
    d-->>c: Return QRContent
    c-->>b: Return QRContent
    b->>a: Show QR Code
    a->>a: Scan QR Code
    alt Static QR 
    a->>d: Input Amount then Payment process
    else Dynamic QR
    a->>d: Fixed Amount then Payment process
    end
    d-->>a: Return Payment Results
    d-->>c: Notify Payment Results
    c-->>b: Notify Payment Results
    b-->a: Update Payment Sratus
    alt Didn't receive Payment Notify
    b->>c: Request Query Payment
    c->>d: Request Query Payment
    d-->>c: Return Payment Results
    c-->>b: Return Payment Results
    end
```

