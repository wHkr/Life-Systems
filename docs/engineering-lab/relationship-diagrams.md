# 🖧 Relationship Diagrams

> Relationship diagrams illustrate **how systems communicate**, not where they are physically located.

!!! info "Purpose"

    Relationship diagrams answer questions like:

    - Which devices communicate?
    - Which interfaces connect them?
    - Which VLAN carries the traffic?
    - Where is the trust boundary?
    - What happens if a device fails?

---

## Enterprise Example
📖 Introduction

🖧 Hero Diagram

```mermaid
flowchart TB

Internet["🌎 Internet"]
ISP["☁️ ISP"]
Router["📡 Router"]
Firewall["🛡️ Firewall"]
Core["🖧 Core Switch"]

AccessA["Switch A"]
AccessB["Switch B"]

NVR["📹 NVR"]

NAS["💾 NAS"]

Docker["🐳 Docker Host"]

WiFi["📶 Access Point"]

Laptop["💻 Laptop"]

Camera1["📷 Camera 1-8"]

Camera2["📷 Camera 9-16"]

Internet --> ISP
ISP -->|WAN| Router
Router -->|LAN1| Firewall
Firewall -->|Gi0/0| Core

Core -->|Gi1/0/1| AccessA
Core -->|Gi1/0/2| AccessB

Core -->|Gi1/0/24| Docker
Core -->|Gi1/0/23| NAS
Core -->|Gi1/0/22| NVR

AccessA -->|PoE1-8| Camera1
AccessB -->|PoE1-8| Camera2

AccessA --> WiFi
WiFi --> Laptop

classDef wan fill:#00b5bb,color:white
classDef security fill:#ef5350,color:white
classDef switching fill:#4361ee,color:white
classDef storage fill:#43aa8b,color:white
classDef client fill:#ffd166,color:black

class Internet,ISP wan
class Router,Firewall security
class Core,AccessA,AccessB switching
class Docker,NVR,NAS storage
class Laptop,WiFi,Camera1,Camera2 client
```

🎨 Color Legend

🔌 Port Naming Standards

🌐 Device Labeling Standards

🏷 VLAN Examples

📋 Engineering Best Practices

💡 Tips

🧪 Practice Lab

🏆 Challenge

📚 Snippet Library