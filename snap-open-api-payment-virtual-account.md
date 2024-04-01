``` mermaid
sequenceDiagram
    autonumber
    title: Payment SNAP Open API - Virtual Account
    participant a as Customer
    participant b as Merchant
    participant c as Open API
    participant d as Payment Gateway
    participant e as Bank
   
    a->>b: Choose Virtual Account as Payment Method
    b->>c: Create Virtual Account
    c->>d: Request Create Virtual Account
    d->>d: Generate/retrieve Virtual Account number
    d-->>c: Return Virtual Account number
    c-->>b: Return Virtual Account number
    b-->>a: Return Virtual Account number
    a->>e: Initiate transfer to Virtual Account
    e->>d: Send Bill Inquiry
    d->>d: Check Bill information
    d-->>e: Return Virtual Account information
    e-->>a: Show Bill information
    a->>e: Confirm transfer to Virtual Account
    e->>d: Send Payment notification
    d->>d: Record Payment
    d-->>e: Return Acknowledgement
    d-->>c: Send Payment callback
    c-->>b: Send Payment callback
    b-->>a: Generate transfer receipt
       
    alt Update VA
        b->>c: Update Virtual Account
        c->>d: Request Update Virtual Account
        d->>d: Check Status VA and Status Payment Order VA
        alt Status VA: PENDING / ACTIVE & Payment Order Status: PENDING
            d-->>c: Return Virtual Account number
            c-->>b: Return Virtual Account Number
        else Status VA: INACTIVE & Payment Order Status : FAILED / SUCCESS
            d-->>c: Return Error Response
            c-->>b: Return Error Response
        end
    alt GET VA
        b->>c: GET Virtual Account
        c->>d: Request GET Virtual Account
        d->>d: Check trxId and virtualAccountNumber
        alt trxId and virtualAccountNumber exist
            d-->>c: Return Virtual Account number
            c-->>b: Return Virtual Account Number
        else trxId and virtualAccountNumber doesn't exist
            d-->>c: Return Error Response
            c-->>b: Return Error Response
        end
    end
    end
```
