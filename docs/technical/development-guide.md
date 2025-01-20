# Guia de Desenvolvimento - Nexus Ligas

## Padrões de Nomenclatura

### 1. Tabelas
```text
# Dimensões
Dim_[Entidade]
- Dim_Produto
- Dim_Cliente
- Dim_Tempo

# Fatos
Fato_[Processo]
- Fato_Producao
- Fato_Vendas
- Fato_Custos

# Staging
STG_[Origem]_[Entidade]
- STG_Datasul_Produtos
- STG_Excel_Budget
```

### 2. Colunas
```text
# Chaves
- SK_[Entidade]: Surrogate Key
- BK_[Entidade]: Business Key
- FK_[Entidade]: Foreign Key

# Atributos
[Entidade]_[Atributo]
- Produto_Codigo
- Cliente_Nome
- Tempo_Data

# Métricas
[Métrica]_[Unidade]
- Volume_Ton
- Valor_BRL
- Energia_MWh
```

### 3. Medidas DAX
```text
# Padrão
[Contexto Métrica]
- [Volume Produção]
- [Receita Bruta]
- [Custo Total]

# Variações
[Métrica] vs [Base]
- [Volume vs Budget]
- [Custo vs Anterior]

# Percentuais
[%] [Contexto]
- [% Margem]
- [% Aderência]
```

## Padrões de Modelagem

### 1. Modelo Estrela
```text
# Centro do Modelo
- Tabelas Fato no centro
- Dimensões nas bordas
- Relacionamentos 1:N

# Granularidade
- Definida por processo
- Documentada por fato
- Consistente por dimensão
```

### 2. Hierarquias
```text
# Padrão Hierarquias
Produto
└── Grupo
    └── Família
        └── Item

Tempo
└── Ano
    └── Semestre
        └── Mês
            └── Dia
```

### 3. Relacionamentos
```text
# Direção Filtro
- Única direção
- Dimensão → Fato
- Sem relacionamentos circulares

# Cardinalidade
- 1:N padrão
- Documentar exceções
```

## Padrões DAX

### 1. Formatação
```dax
// Medida com múltiplas variáveis
[Nome Medida] = 
VAR Valor1 = 
    CALCULATE(
        [Base],
        Filtro
    )
VAR Valor2 = 
    CALCULATE(
        [Base],
        OutroFiltro
    )
RETURN
    Valor1 + Valor2

// Medida com SWITCH
[Status] = 
SWITCH(
    TRUE(),
    [Valor] >= 100, "Alto",
    [Valor] >= 50,  "Médio",
    [Valor] >= 0,   "Baixo",
    "N/A"
)
```

### 2. Comentários
```dax
/* Descrição da Medida
   - Objetivo
   - Premissas
   - Regras
*/
[Medida] = // Nome autoexplicativo
VAR Valor = ... // Explicar se necessário
RETURN ...      // Resultado esperado
```

### 3. Performance
```dax
// Evitar
[Ruim] = 
CALCULATE(
    SUMX(
        Fato,
        Fato[Valor]
    ),
    FILTER(
        Dim,
        Dim[Atributo] = "X"
    )
)

// Preferir
[Bom] = 
CALCULATE(
    [Base],
    Dim[Atributo] = "X"
)
```

## Padrões ETL

### 1. Extração
```sql
-- Template Extração
WITH Base AS (
    SELECT 
        [Campos]
    FROM [Tabela]
    WHERE [Filtros]
),
Transformada AS (
    SELECT
        [Campos Tratados]
    FROM Base
    WHERE [Filtros Adicionais]
)
SELECT * FROM Transformada
```

### 2. Transformação
```text
# Sequência
1. Filtros iniciais
2. Joins necessários
3. Transformações
4. Agregações
5. Filtros finais

# Documentação
-- Origem: [Tabela]
-- Destino: [Tabela]
-- Regras: [Lista]
```

### 3. Carga
```text
# Dimensões
1. Verificar novos
2. Atualizar alterados
3. Manter histórico

# Fatos
1. Truncate/Insert
2. Merge condicional
3. Validar totais
```

## Versionamento

### 1. Estrutura Git
```text
# Branches
main
├── dev
│   ├── feature/[nome]
│   └── bugfix/[nome]
└── release/[versão]

# Tags
v[major].[minor].[patch]
- v1.0.0
- v1.1.0
- v1.1.1
```

### 2. Commits
```text
# Formato
tipo(escopo): descrição

# Tipos
- feat: nova feature
- fix: correção
- docs: documentação
- style: formatação
- refactor: refatoração
- test: testes
```

## Documentação

### 1. Código
```dax
// Template Medida
/*
Objetivo: [Descrever]
Premissas: [Listar]
Fórmula: [Explicar]
*/
```

### 2. Modelo
```text
# Template Tabela
- Nome: [Nome]
- Tipo: [Dim/Fato]
- Granularidade: [Detalhe]
- Origem: [Sistema]
```

### 3. ETL
```text
# Template Processo
- Nome: [Nome]
- Dependências: [Lista]
- Frequência: [Tempo]
- Validações: [Lista]
```

## Governança

### 1. Qualidade
```text
# Checklist
- Nomenclatura padrão
- Documentação completa
- Testes realizados
- Performance ok
```

### 2. Segurança
```text
# Requisitos
- RLS implementado
- Logs ativados
- Backup configurado
- Acesso controlado
```

### 3. Performance
```text
# Métricas
- Tamanho < limite
- Refresh < tempo
- Query < segundos
```