# Nexus Ligas - Governança Power BI

## Sumário da Documentação

- [Arquitetura de Dados](architecture/README.md)
  - [Fonte de Dados](source.md)
  - [Camada Bronze](bronze.md)
  - [Camada Silver](silver.md)
  - [Camada Gold](gold.md)
  - [Publicação](publish.md)
- [Requisitos](requirements/README.md)
- [User Stories](user%20stories/README.md)

## Arquitetura de Dados

```mermaid
flowchart TD
    %% High contrast light theme for better visibility
    classDef source fill:#ffffff,stroke:#000000,stroke-width:2px,color:#000000
    classDef bronze fill:#f5f5f5,stroke:#000000,stroke-width:2px,color:#000000
    classDef silver fill:#ececec,stroke:#000000,stroke-width:2px,color:#000000
    classDef gold fill:#e0e0e0,stroke:#000000,stroke-width:2px,color:#000000
    classDef publish fill:#d3d3d3,stroke:#000000,stroke-width:2px,color:#000000
    classDef users fill:#c0c0c0,stroke:#000000,stroke-width:2px,color:#000000

    subgraph Fonte["Fonte de Dados"]
        DS[(Datasul Progress)]
        class DS source
    end

    subgraph Bronze["Camada Bronze"]
        SQLServer[(SQL Server)]
        class SQLServer bronze
        DS --> SQLServer
    end

    subgraph Silver["Camada Silver"]
        DW[("Data Warehouse\nModelo Dimensional")]
        class DW silver
        SQLServer --> DW
    end

    subgraph Gold["Camada Gold"]
        SM["Modelo Semântico\nPower BI"]
        class SM gold
        DW --> SM
    end

    subgraph Publicacao["Publicação"]
        WS["Workspace\nPower BI Service"]
        APP["App\nBase Única"]
        class WS,APP publish
        SM --> WS
        WS --> APP
    end

    subgraph Usuarios["Usuários"]
        UN["Usuários\nde Negócio"]
        UA["Usuários\nAnalistas"]
        UT["Usuários\nTI"]
        class UN,UA,UT users
        APP --> UN
        APP --> UA
        WS --> UT
    end

    %% Style for subgraph titles
    classDef subgraphStyle fill:none,stroke:none,color:#ffffff
    class Fonte,Bronze,Silver,Gold,Publicacao,Usuarios subgraphStyle
```

[Rest of the file content remains the same...]