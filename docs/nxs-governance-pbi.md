# Nexus Ligas - Governança Power BI

## Arquitetura de Dados

```mermaid
flowchart TD
    subgraph Fonte["Fonte de Dados"]
        DS[(Datasul Progress)]
    end

    subgraph Bronze["Camada Bronze"]
        SQLServer[(SQL Server)]
        style SQLServer fill:#cd7f32
        DS --> SQLServer
    end

    subgraph Silver["Camada Silver"]
        DW[("Data Warehouse\nModelo Dimensional")]
        style DW fill:#c0c0c0
        SQLServer --> DW
    end

    subgraph Gold["Camada Gold"]
        SM["Modelo Semântico\nPower BI"]
        style SM fill:#ffd700
        DW --> SM
    end

    subgraph Publicacao["Publicação"]
        WS["Workspace\nPower BI Service"]
        APP["App\nBase Única"]
        style WS fill:#9932cc
        style APP fill:#ffa500
        SM --> WS
        WS --> APP
    end

    subgraph Usuarios["Usuários"]
        UN["Usuários\nde Negócio"]
        UA["Usuários\nAnalistas"]
        UT["Usuários\nTI"]
        APP --> UN
        APP --> UA
        WS --> UT
    end
```

## Papéis e Responsabilidades

### TI (Tecnologia da Informação)
- Gestão da infraestrutura
- Manutenção da camada bronze (SQL Server)
- Monitoramento de performance
- Gestão de acessos e segurança
- Backup e disaster recovery

### Analistas de Dados
- Desenvolvimento dos modelos dimensionais (Silver)
- Criação e manutenção do modelo semântico (Gold)
- Desenvolvimento de relatórios e dashboards
- Documentação técnica
- Suporte aos usuários de negócio

### Usuários de Negócio
- Consumo dos relatórios via App
- Validação das regras de negócio
- Solicitação de novos desenvolvimentos
- Feedback sobre usabilidade
- Participação nas homologações

## Template Padrão

### Elementos Visuais
- Logotipo Nexus Ligas (superior esquerdo)
- Marca d'água corporativa
- Cores principais:
  * Roxo: #9932cc
  * Laranja: #ffa500

### Layout de Página
- Header fixo com:
  * Logo
  * Título do relatório
  * Data atualização
- Área de filtros (slicers):
  * Data/Período
  * Centro/Planta
  * Produto/Material
  * Outros contextuais
- Área principal de visualizações
- Rodapé com informações de versão

### Navegação
- Menu lateral consistente
- Botões de navegação padronizados
- Drill-through configurado
- Tooltips informativos

## Fluxo de Desenvolvimento

1. **Solicitação**
   - Template de requisição
   - Aprovação do gestor
   - Priorização

2. **Desenvolvimento**
   - Ambiente de desenvolvimento
   - Testes unitários
   - Documentação

3. **Homologação**
   - Validação com usuários
   - Ajustes necessários
   - Aprovação formal

4. **Publicação**
   - Workspace de produção
   - Atualização do App
   - Comunicação aos usuários

## Boas Práticas

### Nomenclatura
- Tabelas: F_ (fatos) e D_ (dimensões)
- Medidas: [med]NomeMedida
- Colunas calculadas: [cc]NomeColuna

### Performance
- Modo Import preferencial
- Direct Query quando necessário
- Refresh incremental configurado
- Particionamento adequado

### Segurança
- RLS (Row Level Security) implementado
- Grupos de segurança AD
- Classificação de dados
- Auditoria ativa

## Suporte e Manutenção

### Níveis de Suporte
1. Autoajuda (documentação)
2. Suporte N1 (analistas)
3. Suporte N2 (TI)

### SLAs
- Criticidade Alta: 4h
- Criticidade Média: 8h
- Criticidade Baixa: 24h