``` mermaid
sequenceDiagram
    autonumber
    title: Update VA Bill Information - Close Multiple Use (Close Static)
    participant a as Merchant
    participant b as Open API
    participant c as BE Portal
    a->>b : Request Update VA - Close Static
    note left of a : Attach VA number & new Bill information
    b->>c : Request Update VA - Close Static
    c->>c : VA Validation ? Is Va Exist ?
    alt VA is Exist
    c-->>b : Return VA updated bill number
    note right of c : Expired date set to be null
    b-->>a : Return VA updated bill number
    else VA is not Exist
    c-->>b : Return VA updated bill error response [VA is not exist]
    b-->>a : Return VA updated bill error response [VA is not exist]
    end
```
