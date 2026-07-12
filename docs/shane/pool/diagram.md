# Diagram
---


```mermaid
flowchart LR

%%==========================
%% POOL
%%==========================

subgraph Pool["🏊 Above Ground Pool"]

    RETURN["Return Port
(Left Side)

◄ Water Returns Here
Air Valve"]

    SUCTION1["Suction Port #1
(Upper Right)

Skimmer Intake"]

    SUCTION2["Suction Port #2
(Lower Right)

Main Drain /
Secondary Intake"]

end

%%==========================
%% VALVE
%%==========================

subgraph Plumbing["🔧 Plumbing"]

    TEE{{T-Connector
Lock / Unlock
Valve}}

end

%%==========================
%% EQUIPMENT
%%==========================

subgraph Equipment["⚙️ Equipment Pad"]

    PUMP["SX1200 Pump

IN ◄
OUT ►"]

    FILTER["Sand Filter

IN ◄
OUT ►"]

    ECO["QS1200 E.C.O.

IN ◄
OUT ►

Salt Cell"]

end

%%==========================
%% FLOW
%%==========================

SUCTION1 -->|"Hose A"| TEE
SUCTION2 -->|"Hose B"| TEE

TEE -->|"Combined Suction"| PUMP

PUMP -->|"Pressurized Water"| FILTER

FILTER -->|"Filtered Water"| ECO

ECO -->|"Chlorinated Water"| RETURN

%%==========================
%% COLORS
%%==========================

classDef pool fill:#d6f5ff,stroke:#0077b6,stroke-width:2px;
classDef pipe fill:#fff4cc,stroke:#b8860b,stroke-width:2px;
classDef equip fill:#d9fdd3,stroke:#2e8b57,stroke-width:2px;

class RETURN,SUCTION1,SUCTION2 pool;
class TEE pipe;
class PUMP,FILTER,ECO equip;
```

| Component     | IN                | OUT            | Notes                                       |
| ------------- | ----------------- | -------------- | ------------------------------------------- |
| Pool          | Return Port       | Suction Ports  | Water leaves from suction, returns to inlet |
| T-Connector   | Two suction hoses | One hose       | Combines both intakes                       |
| SX1200 Pump   | From pool         | To sand filter | Never run dry                               |
| Sand Filter   | Pump output       | E.C.O. input   | Backwash when pressure rises                |
| QS1200 E.C.O. | Sand filter       | Pool return    | Must always receive filtered water          |
