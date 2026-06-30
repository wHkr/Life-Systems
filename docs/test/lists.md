## Entity Relationship Diagram

```mermaid
erDiagram

USER {
    string username
    string email
    string password
}

SERVER {
    string hostname
    string ip
}

CONTAINER {
    string image
    string port
}

USER ||--o{ SERVER : owns
SERVER ||--o{ CONTAINER : hosts
```

## Requirement Diagram

```mermaid
requirementDiagram

requirement security {
    id: 1
    text: All traffic must be encrypted
    risk: High
    verifymethod: Test
}

element Firewall

Firewall - satisfies -> security
```

