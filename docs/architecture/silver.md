# Camada Silver - Data Warehouse

## Visão Geral

A camada Silver implementa o modelo dimensional (Star Schema) do Data Warehouse, transformando os dados brutos da camada Bronze em estruturas otimizadas para análise.

```mermaid
flowchart TD
    subgraph DW["Data Warehouse"]
        subgraph FT["Tabelas Fato"]
            FTV["Vendas"]
            FTP["Produção"]
            FTC["Compras"]
            FTE["Estoque"]
        end
        
        subgraph DM["Dimensões"]
            DMP["Produto"]
            DMC["Cliente"]
            DMF["Fornecedor"]
            DMT["Tempo"]
            DMD["Depósito"]
            DME["Estabelecimento"]
        end
        
        DMP --> FTV & FTP & FTC & FTE
        DMC --> FTV
        DMF --> FTC
        DMT --> FTV & FTP & FTC & FTE
        DMD --> FTE
        DME --> FTV & FTP & FTC & FTE
    end

    %% High contrast light theme for better visibility
    classDef fact fill:#f5f5f5,stroke:#000000,stroke-width:2px,color:#000000
    classDef dim fill:#ffffff,stroke:#000000,stroke-width:2px,color:#000000
    classDef container fill:none,stroke:#000000,stroke-width:2px,color:#ffffff

    class FTV,FTP,FTC,FTE fact
    class DMP,DMC,DMF,DMT,DMD,DME dim
    class DW,FT,DM container
```

## Estrutura Dimensional

### Dimensões Principais

[Previous content of the file including all SQL and documentation]

## Links Relacionados
- [Camada Bronze](bronze.md)
- [Camada Gold](gold.md)
- [Governança](../governance.md)