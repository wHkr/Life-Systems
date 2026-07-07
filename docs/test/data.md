# Data

!!! example

    === "Table 1"

    | Method      | Description                          |
    | :----------- | :------------------------------------ |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |

    === "Table Center"

    | Method      | Description                          |
    | :-----------: | :------------------------------------: |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |

    === "Table Right"

    | Method      | Description                          |
    | ----------- | ------------------------------------ |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |


## Data Tables

### Data Table 1
| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     Fetch resource  |
| `PUT`       | :material-check-all: Update resource |
| `DELETE`    | :material-close:     Delete resource |


### Column Align
| Method      | Description                          |
| :----------: | :-----------------------------------: |
| `GET`       | :material-check:     Fetch resource  |
| `PUT`       | :material-check-all: Update resource |
| `DELETE`    | :material-close:     Delete resource |

## Pie Chart
```mermaid
pie title Time Spent Learning

"Networking" : 30
"Linux" : 25
"Python" : 20
"Docker" : 15
"Other" : 10
```

## XY Chart
```mermaid
xychart-beta
title "Build Times"

x-axis [Build1, Build2, Build3, Build4]
y-axis "Seconds" 0 --> 100

bar [80,60,45,20]
line [75,55,42,18]
```

## Quadrant Chart
```mermaid
quadrantChart
title Technology Maturity

x-axis Beginner --> Expert
y-axis Low Value --> High Value

quadrant-1 Learn Later
quadrant-2 Learn First
quadrant-3 Ignore
quadrant-4 Master

Python:[0.85,0.90]
Docker:[0.70,0.80]
C++:[0.40,0.95]
Java:[0.30,0.45]
```

## Sankey Diagram
```mermaid
sankey-beta

Salary,Taxes,20
Salary,Savings,30
Salary,Investing,25
Salary,Spending,25

Savings,Emergency Fund,20
Savings,Vacation,10
```