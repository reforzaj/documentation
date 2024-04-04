``` mermaid
sequenceDiagram
    autonumber
    title: GET B2B Token for Merchant
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal

    a->>b: GET B2B Token
    b->>c: Request GET B2B Token
    c->>c: Validate client_id and X-SIGNATURE
    alt client_id and X-SIGNATURE valid
    c->>b: Return success and B2B Access Token
    b->>a: Return success and B2B Access Token
    else client_id or/and X-SIGNATURE invalid
    c->>b: Return error
    b->>a: Return error
    end
```
