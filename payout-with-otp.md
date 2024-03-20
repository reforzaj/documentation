``` mermaid
sequenceDiagram
    autonumber
    title: Create Payout with OTP
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal

    a->>b: Request OTP
    b->>c: Request OTP
    c->>c: Generate OTP
    c-->>b: Send OTP Response
    b->>a: Send OTP Response
        alt OTP Valid
        a->>b: Create Payout request with OTP
        b->>c: Verify OTP and Payout request
        c->>c: Validate OTP Success
        c->>c: Execute Payout
        c-->>b: Send Success Payout Request Response
        b->>a: Payout Request Response
        end
        alt OTP Invalid
        a->>b: Create Payout request with OTP
        b->>c: Verifty OTP and Payout request
        c->>c: Validate OTP Failed
        c-->>b: Invalid OTP Response
        b->>a: Invalid OTP Response
        end
```
