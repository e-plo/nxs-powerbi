# Métricas Nexus Ligas

## BU-SOP Métricas

### 1. Métricas de Volume
```dax
[Volume Carteira] = 
SUM(Fato_Carteira[Volume_Cart])

[Volume Vendas Atual] = 
CALCULATE(
    [Volume Carteira],
    Dim_Versao[Codigo] = "ACTUAL"
)

[Volume Vendas BGT] = 
CALCULATE(
    [Volume Carteira],
    Dim_Versao[Codigo] = "BGT"
)

[Volume Vendas MRF] = 
CALCULATE(
    [Volume Carteira],
    Dim_Versao[Codigo] = "MRF"
)
```

### 2. Métricas de Aderência
```dax
[% Aderência Volume BGT] = 
DIVIDE(
    [Volume Vendas Atual],
    [Volume Vendas BGT],
    BLANK()
)

[% Aderência Volume MRF] = 
DIVIDE(
    [Volume Vendas Atual],
    [Volume Vendas MRF],
    BLANK()
)
```

## BU-OPERACIONAL Métricas

### 1. Métricas de Produção
```dax
[Volume Produção] = 
SUM(Fato_Producao[Volume_Prod])

[Horas Produtivas] = 
SUM(Fato_Producao[Horas_Prod])

[Volume/Hora] = 
DIVIDE(
    [Volume Produção],
    [Horas Produtivas],
    BLANK()
)
```

### 2. Métricas de Consumo
```dax
[Consumo Minério] = 
SUM(Fato_Consumo[Volume_Cons])

[Consumo Energia] = 
SUM(Fato_Producao[Energia_Cons])

[Energia/Ton] = 
DIVIDE(
    [Consumo Energia],
    [Volume Produção],
    BLANK()
)
```

### 3. Métricas de Recovery
```dax
[Recovery Mn] = 
DIVIDE(
    SUM(Fato_Producao[Mn_Output]),
    SUM(Fato_Consumo[Mn_Input]),
    BLANK()
)

[% Teor Liga] = 
AVERAGE(Fato_Qualidade[Teor_Final])
```

## BU-CORP Métricas

### 1. Métricas de Resultado
```dax
[Receita Bruta] = 
SUM(Fato_Resultado[Receita_Real])

[Custos Totais] = 
SUM(Fato_Custos[Valor_Fix]) + 
SUM(Fato_Custos[Valor_Var])

[Margem Bruta] = 
DIVIDE(
    [Receita Bruta] - [Custos Totais],
    [Receita Bruta],
    BLANK()
)
```

### 2. Métricas de Custo
```dax
[Custo/Ton] = 
DIVIDE(
    [Custos Totais],
    [Volume Produção],
    BLANK()
)

[Custo Fixo/Ton] = 
DIVIDE(
    SUM(Fato_Custos[Valor_Fix]),
    [Volume Produção],
    BLANK()
)

[Custo Variável/Ton] = 
DIVIDE(
    SUM(Fato_Custos[Valor_Var]),
    [Volume Produção],
    BLANK()
)
```

## Variações e KPIs

### 1. Variações vs Plano
```dax
[Var Volume vs BGT %] = 
DIVIDE(
    [Volume Vendas Atual] - [Volume Vendas BGT],
    [Volume Vendas BGT],
    BLANK()
)

[Var Volume vs MRF %] = 
DIVIDE(
    [Volume Vendas Atual] - [Volume Vendas MRF],
    [Volume Vendas MRF],
    BLANK()
)
```

### 2. KPIs Principais
```dax
[Status Recovery] = 
SWITCH(
    TRUE(),
    [Recovery Mn] >= 0.80, "✓ Ótimo",
    [Recovery Mn] >= 0.75, "⚠️ Atenção",
    "❌ Crítico"
)

[Status Energia] = 
SWITCH(
    TRUE(),
    [Energia/Ton] <= 3.2, "✓ Ótimo",
    [Energia/Ton] <= 3.5, "⚠️ Atenção",
    "❌ Crítico"
)

[Status Margem] = 
SWITCH(
    TRUE(),
    [Margem Bruta] >= 0.25, "✓ Ótimo",
    [Margem Bruta] >= 0.20, "⚠️ Atenção",
    "❌ Crítico"
)
```