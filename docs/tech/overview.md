# Network & Technology Overview
---
# Camera Network Topology

The following diagram illustrates the logical layout of the kennel camera network.

```mermaid
flowchart TD
    A[Router] --> B[Core Switch] --> C[NVR]
    C --> D{Access Switch A}
    C --> E{Access Switch B}

    D -- "PoE Cameras" --> F((Camera 1-15))
    E -- "PoE Cameras" --> G((Camera 16-30))

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#ccf,stroke:#333,stroke-width:2px
    style C fill:#afa,stroke:#333,stroke-width:1px
    style D fill:#eee,stroke:#333,stroke-width:1px
    style E fill:#ddd,stroke:#333,stroke-width:0.5px
    style F fill:#ddd,stroke:#333,stroke-width:0.5px
    style G fill:#eee,stroke:#333,stroke-width:1px
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

