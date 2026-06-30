# Diagrams
===

!!! tip
    > Syntax: [Custom Shapes](https://mermaid.ai/open-source/syntax/flowchart.html)

## Networking Flowchart
```mermaid
flowchart LR

Laptop["💻 Laptop"]
Router["📡 Router"]
Firewall["🛡️ Firewall"]
Docker["🐳 Docker"]
Database["🗄️ Database"]

Laptop --> Router
Router --> Firewall
Firewall --> Docker
Docker --> Database

classDef secure fill:#009688,color:#fff,stroke:#004d40,stroke-width:3px
class Firewall secure
```

## Flowcharts
``` mermaid
---
title: Flowchart
---
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```
!!! tip
    > You can also use `graph` in place of flowchart

## Sequence Diagrams
``` mermaid
---
title: Sequence Diagrams
---
sequenceDiagram
  autonumber
  Alice->>John: Hello John, how are you?
  loop Healthcheck
      John->>John: Fight against hypochondria
  end
  Note right of John: Rational thoughts!
  John-->>Alice: Great!
  John->>Bob: How about you?
  Bob-->>John: Jolly good!
```

## State Diagrams
``` mermaid
stateDiagram-v2
  state fork_state <<fork>>
    [*] --> fork_state
    fork_state --> State2
    fork_state --> State3

    state join_state <<join>>
    State2 --> join_state
    State3 --> join_state
    join_state --> State4
    State4 --> [*]
```

## Class Diagrams
``` mermaid
---
title: Class Diagrams
---
classDiagram
  Person <|-- Student
  Person <|-- Professor
  Person : +String name
  Person : +String phoneNumber
  Person : +String emailAddress
  Person: +purchaseParkingPass()
  Address "1" <-- "0..1" Person:lives at
  class Student{
    +int studentNumber
    +int averageMark
    +isEligibleToEnrol()
    +getSeminarsTaken()
  }
  class Professor{
    +int salary
  }
  class Address{
    +String street
    +String city
    +String state
    +int postalCode
    +String country
    -validate()
    +outputAsLabel()
  }
```

## Entity-Relationship Diagrams
``` mermaid
---
title: Entity-Relationship Diagrams
---
erDiagram
  CUSTOMER ||--o{ ORDER : places
  ORDER ||--|{ LINE-ITEM : contains
  LINE-ITEM {
    string name
    int pricePerUnit
  }
  CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
```
## Containers
```mermaid
flowchart LR
    id1(This is the text in the box)
```

```mermaid
flowchart LR
    id1([This is the text in the box])
```

```mermaid
flowchart LR
    id1[[This is the text in the box]]

```

```mermaid
flowchart LR
    id1[(Database)]
```

```mermaid
flowchart LR
    id1>This is the text in the box]
```

## Image Shape
```mermaid
flowchart TD
  %% My image with a constrained aspect ratio
  A@{ img: "https://mermaid.js.org/favicon.svg", label: "My example image label", pos: "t", h: 60, constraint: "on" }
```
???+ example
     - ***img:*** The URL of the image
     - ***label:*** Text label associated with the image. `<str>`
     - ***pos:*** Position label
    > - `t` - Top
    > - `b` - Bottom
     - ***w:*** Width of Image
     - ***h:*** Height of Image
     - ***Constraint:*** Constrain Node? *Default: `off`
    > - `on`
    > - `off`


### For dotted or thick links, the characters to add are equals signs or dots, as summed up in the following table:

| Length | 1 | 2 | 3 |
| ------ | --- | --- | --- |
Normal |--- |---- |----- |
Normal with arrow |--> |---> |----> |
Thick |=== |==== | ===== |
Thick with arrow |==> |===> |====> |
Dotted |-.- |-..- |-...- |
Dotted with arrow |-.-> |-..-> |-...-> |

---

## Subgraphs (Customizable Shapes)
```mermaid
---
title: Subgraph Name
---
flowchart TB
    c1===>a2
    subgraph one
    a1-.->a2
    end
    subgraph two
    b1-->A@{ shape: dbl-circ, label: "b2" }
    end
    subgraph three
    c1-->c2
    end
```

## Markdown Strings
The "Markdown Strings" feature enhances flowcharts and mind maps by offering a more versatile string type, which supports text formatting options such as **bold** and *italics*, and automatically wraps text within labels.

Code:
```mermaid
---
config:
  htmlLabels: false
---
flowchart LR
subgraph "One"
  a("`The **cat** in the hat`")
    -- "edge label"
    --> b{{"`The **dog** in the hog`"}}
end
subgraph "`**Two**`"
    c("`The **cat** in the hat`")
    -- "`Bold **edge label**`"
    --> d("The dog in the hog")
end
```
## Diagram Level Curve Style
```mermaid
---
title: Diagram Level Curve
config:
    flowchart:
        curve: catmullRom
---
flowchart LR
    A e1@==> B
    A e2@--> C
    e1@{ curve: linear }
    e2@{ curve: natural }
```

## Styling a Node
```mermaid
flowchart LR
    id1(Start)-->id2(Stop)
    style id1 fill:#f9f,stroke:#333,stroke-width:4px
    style id2 fill:#bbf,stroke:#f66,stroke-width:2px,color:#fff,stroke-dasharray: 5 5
```
### Classes

!!! example "Ex.1: Define a single example:"
    `classDef className fill:#f9f,stroke:#333,stroke-width:4px;`

!!! example "Ex.2: Define multiple examples:"
    `classDef firstClassName,secondClassName font-size:12pt;`


!!! example "Ex.3: Attach a class to a Node:"
    `class nodeId1 className;`


!!! example "Ex.4: Attach a class to a list of Nodes:"
    `class nodeId1,nodeId2 className;


!!! info
> A shorter form of adding a class is to attach the classname to the node using the `:::` operator.
```mermaid
flowchart LR
    A:::someclass --> B
    classDef someclass fill:#f96
```

## Used when declaring multiple links between nodes:
```mermaid
flowchart LR
    A:::foo & B:::bar --> C:::foobar
    classDef foo stroke:#f00
    classDef bar stroke:#0f0
    classDef foobar stroke:#00f
```


```mermaid
---
title: Ex. 3 - flowchart TD
---
flowchart TD
    B[":material-router-wireless:"]
    B-->C[fa:fa-ban forbidden]
    B-->D(fa:fa-spinner)
    B-->E(A fa:fa-camera-retro perhaps?)
```

## Networking Flowchart -- Color
```mermaid
---
title: Networking flowchart
---
flowchart LR

    Internet([🌎 Internet])
    Router{{Router}}
    Firewall[[Firewall]]
    Switch[(Core Switch)]
    Server[(Docker Host)]
    NAS[(Storage)]

    Internet --> Router
    Router --> Firewall
    Firewall --> Switch
    Switch --> Server
    Switch --> NAS

    style Internet fill:#8fd3ff,stroke:#006699,stroke-width:3px
    style Router fill:#ffd166,stroke:#333
    style Firewall fill:#ff595e,color:#fff
    style Switch fill:#8ac926
    style Server fill:#6a4c93,color:#fff
    style NAS fill:#1982c4,color:#fff

    linkStyle 0 stroke:#0099ff,stroke-width:3px
    linkStyle 1 stroke:red,stroke-width:2px
```

## Animated Packet flow
```mermaid
flowchart LR

A([Laptop]) -->|HTTPS| B((Router))
B --> C{Firewall}
C --> D[(Server)]

linkStyle default stroke:#00b5bb,stroke-width:4px;
```

## Mind Map
```mermaid
mindmap
root((Engineering))

    Networking
        Routing
        VLANs
        Firewalls

    Programming
        Python
        C++
        JavaScript

    Linux
        Bash
        Docker
        WSL

    Documentation
        MkDocs
        Mermaid
        Markdown
```

## Timeline
```mermaid
timeline
    title Engineering Journey

    2024 : Networking
         : Linux

    2025 : Python
         : Docker

    2026 : AI
         : Documentation
```

## Git Graph
```mermaid
gitGraph
commit
branch feature
checkout feature
commit
commit
checkout main
merge feature
commit
```

