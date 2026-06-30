# Network & Technology Overview
---
# 🧜 Mermaid Laboratory

> Welcome to the Mermaid showcase for **Life Systems**.
>
> This page demonstrates diagrams, Material for MkDocs components, colors,
> icons, tabs, buttons, and interactive callouts that can be reused
> throughout the engineering documentation.

---

```mermaid
flowchart LR

Internet["🌎 Internet"]
Router["📡 Router"]
Firewall["🛡️ Firewall"]
Core["🖧 Core Switch"]
Docker["🐳 Docker Host"]
Storage["💾 NAS"]

Internet --> Router
Router --> Firewall
Firewall --> Core
Core --> Docker
Core --> Storage

classDef internet fill:#00b5bb,color:#fff,stroke:#005b66,stroke-width:3px
classDef network fill:#3a86ff,color:#fff
classDef server fill:#6a4c93,color:#fff
classDef storage fill:#8ac926,color:#000

class Internet internet
class Router,Firewall,Core network
class Docker server
class Storage storage
```

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

