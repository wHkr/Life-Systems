# Network & Technology Overview
---
# Camera Network Topology

The following diagram illustrates the logical layout of the kennel camera network.

```mermaid
flowchart LR
    A[Router] --> B[Core Switch]
    B --> C{Access Switch A}
    B --> D{Access Switch B}

    C -- "PoE Cameras" --> E((Camera 1-15))
    D -- "PoE Cameras" --> F((Camera 16-30))

    E --> G[NVR<br/>IDS-9632]
    F --> G

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#ccf,stroke:#333,stroke-width:2px
    style C fill:#eee,stroke:#333,stroke-width:1px
    style D fill:#eee,stroke:#333,stroke-width:1px
    style E fill:#ddd,stroke:#333,stroke-width:0.5px
    style F fill:#ddd,stroke:#333,stroke-width:0.5px
    style G fill:#afa,stroke:#333,stroke-width:1px
```

# Camera Network

## Purpose

...

## Physical Topology

```mermaid
...
```

## Logical Topology

```mermaid
...
```

## Packet Flow

```mermaid
...
```

## VLAN Layout

```mermaid
...
```

## Failure Domains

```mermaid
...
```

## Power Distribution

```mermaid
...
```

