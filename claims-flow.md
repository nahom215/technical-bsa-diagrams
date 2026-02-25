# Healthcare Claims Processing Sequence
This diagram models the system-to-system communication required to process a provider claim.

```mermaid
sequenceDiagram
    participant P as Provider Portal
    participant C as Claims Engine
    participant E as Eligibility API
    participant D as Database

    P->>C: Submit Claim (837 Professional)
    C->>E: Validate Member ID & Coverage
    E-->>C: Response: Active/Inactive
    
    alt Member is Active
        C->>D: Store Claim & Assign ID
        D-->>C: Confirmation
        C-->>P: Status: Received / Pending
    else Member is Inactive
        C-->>P: Status: Denied (Invalid Eligibility)
    end
