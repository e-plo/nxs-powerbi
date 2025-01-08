# Nexus Ligas - Arquitetura de Dados Power BI

```mermaid
flowchart TD
    %% Styling
    classDef sourceStyle fill:#2F2F2F,stroke:#FFFFFF,stroke-width:2px,color:#FFFFFF,width:200px
    classDef bronzeStyle fill:#4F4F4F,stroke:#FFFFFF,stroke-width:2px,color:#FFFFFF,width:200px
    classDef silverStyle fill:#6F6F6F,stroke:#FFFFFF,stroke-width:2px,color:#FFFFFF,width:200px
    classDef goldStyle fill:#8F8F8F,stroke:#FFFFFF,stroke-width:2px,color:#FFFFFF,width:200px
    classDef publishStyle fill:#AFAFAF,stroke:#FFFFFF,stroke-width:2px,color:#000000,width:200px
    
    subgraph SOURCE["Fonte"]
        DS[(Datasul\nProgress DB)]
    end
    
    subgraph BRONZE["Camada Bronze"]
        SQL[(SQL Server\nWindows)]
    end
    
    subgraph SILVER["Camada Silver"]
        DW[("Data Warehouse\nModelo Dimensional")]
    end
    
    subgraph GOLD["Camada Gold"]
        SEM["Modelo Semântico\nPower BI"]
    end
    
    subgraph PUBLISH["Publicação"]
        WS["Workspace\nBase Única"]
    end

    DS --> SQL
    SQL --> DW
    DW --> SEM
    SEM --> WS

    %% Apply styles
    class SOURCE,DS sourceStyle
    class BRONZE,SQL bronzeStyle
    class SILVER,DW silverStyle
    class GOLD,SEM goldStyle
    class PUBLISH,WS publishStyle

    %% Add links to documentation
    click DS "source.md" "Ver documentação da fonte"
    click SQL "bronze.md" "Ver documentação da camada bronze"
    click DW "silver.md" "Ver documentação da camada silver"
    click SEM "gold.md" "Ver documentação da camada gold"
    click WS "publish.md" "Ver documentação da publicação"
```

## Documentação por Camada

### [📁 Fonte (Datasul)](source.md)
- Origem dos dados transacionais
- Estrutura de tabelas TOTVS
- Periodicidade de atualização
- Gestão de conexões

### [📁 Bronze (SQL Server)](bronze.md)
- Réplica dos dados Datasul
- Estrutura normalizada
- Processos de ETL
- Controle de qualidade

### [📁 Silver (Data Warehouse)](silver.md)
- Modelo dimensional
- Star schemas
- Histórico e snapshots
- Processos de transformação

### [📁 Gold (Semantic Model)](gold.md)
- Modelo semântico Power BI
- Medidas e KPIs
- Relacionamentos
- Otimização de performance

### [📁 Publicação (Workspace)](publish.md)
- Ambientes (DEV/PRD)
- Políticas de atualização
- Segurança e acessos
- Monitoramento
