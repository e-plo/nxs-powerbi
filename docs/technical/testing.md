# Testes e Validações - Nexus Ligas

## 1. Testes de Integridade de Dados

### 1.1. Validações Dimensionais
```dax
-- Teste de Produtos sem Dimensão
TEST_Orphan_Products = 
CALCULATE(
    COUNTROWS(Fato_Producao),
    NOT(RELATED(Dim_Produto[SK_Produto]))
)

-- Teste de Clientes sem Dimensão
TEST_Orphan_Customers = 
CALCULATE(
    COUNTROWS(Fato_Vendas),
    NOT(RELATED(Dim_Cliente[SK_Cliente]))
)

-- Teste de Datas sem Dimensão
TEST_Orphan_Dates = 
CALCULATE(
    COUNTROWS(Fato_Producao),
    NOT(RELATED(Dim_Tempo[SK_Tempo]))
)
```

### 1.2. Validações de Totais
```dax
-- Teste Volume Total de Produção
TEST_Production_Volume = 
VAR VolumeBI = [Volume_Producao_Total]
VAR VolumeERP = SUMX(ERP_Producao, [Volume])
RETURN
IF(
    ABS(VolumeBI - VolumeERP) <= 0.01,
    "OK",
    "ERRO: Diferença " & VolumeBI - VolumeERP
)

-- Teste Receita Total
TEST_Revenue = 
VAR ReceitaBI = [Receita_Total]
VAR ReceitaERP = SUMX(ERP_Vendas, [Valor])
RETURN
IF(
    ABS(ReceitaBI - ReceitaERP) <= 0.01,
    "OK",
    "ERRO: Diferença " & ReceitaBI - ReceitaERP
)
```

## 2. Testes de Qualidade de Dados

### 2.1. Validações de Valores
```dax
-- Teste de Valores Negativos
TEST_Negative_Values = 
CALCULATE(
    COUNTROWS(Fato_Producao),
    Fato_Producao[Volume_Prod] < 0
)

-- Teste de Valores Nulos
TEST_Null_Values = 
CALCULATE(
    COUNTROWS(Fato_Producao),
    ISBLANK(Fato_Producao[Volume_Prod])
)

-- Teste de Valores Zero
TEST_Zero_Values = 
CALCULATE(
    COUNTROWS(Fato_Producao),
    Fato_Producao[Volume_Prod] = 0
)
```

### 2.2. Validações de Limites
```dax
-- Teste Teor de Manganês
TEST_Mn_Content = 
VAR MaxTeor = MAX(Fato_Qualidade[Teor_Mn])
VAR MinTeor = MIN(Fato_Qualidade[Teor_Mn])
RETURN
IF(
    MaxTeor <= 80 && MinTeor >= 60,
    "OK",
    "ERRO: Teor fora do range"
)

-- Teste Recovery Metalúrgico
TEST_Recovery = 
VAR MaxRec = MAX(Fato_Producao[Recovery])
RETURN
IF(
    MaxRec <= 0.95,
    "OK",
    "ERRO: Recovery impossível"
)
```

## 3. Testes de Performance

### 3.1. Métricas de Tempo
```powershell
# Refresh
- Full Refresh < 30 minutos
- Incremental < 5 minutos
- Dimensões < 2 minutos

# Resposta
- Filtros < 1 segundo
- Drill-down < 2 segundos
- Cálculos < 3 segundos

# Carregamento
- Inicial < 10 segundos
- Mudança de Página < 2 segundos
```

### 3.2. Métricas de Tamanho
```powershell
# Limites por PBIX
- BU-SOP < 300MB
- BU-OPERACIONAL < 400MB
- BU-CORP < 300MB

# Tabelas Críticas
- Fato_Producao < 100MB
- Fato_Vendas < 100MB
- Fato_Qualidade < 50MB
```

## 4. Testes de Regras de Negócio

### 4.1. Validações Metalúrgicas
```dax
-- Teste Balanço de Massa
TEST_Mass_Balance = 
VAR Input = SUM(Fato_Consumo[Massa_Input])
VAR Output = SUM(Fato_Producao[Massa_Output])
VAR Delta = ABS(1 - DIVIDE(Output, Input))
RETURN
IF(
    Delta <= 0.02,
    "OK",
    "ERRO: Diferença " & Delta
)

-- Teste Consumo Específico
TEST_Specific_Consumption = 
VAR ConsEsp = DIVIDE(
    SUM(Fato_Consumo[Volume_Minerio]),
    SUM(Fato_Producao[Volume_Prod])
)
RETURN
IF(
    ConsEsp >= 1.5 && ConsEsp <= 2.5,
    "OK",
    "ERRO: Consumo específico " & ConsEsp
)
```

### 4.2. Validações Comerciais
```dax
-- Teste Margem
TEST_Margin = 
VAR Margem = [Margem_Bruta]
RETURN
IF(
    Margem >= 0 && Margem <= 0.50,
    "OK",
    "ERRO: Margem impossível"
)

-- Teste Preço Médio
TEST_Average_Price = 
VAR PrecoMed = [Preco_Medio]
RETURN
IF(
    PrecoMed >= 1000 && PrecoMed <= 5000,
    "OK",
    "ERRO: Preço fora da faixa"
)
```

## 5. Testes de Consistência Temporal

### 5.1. Validações de Série
```dax
-- Teste Tendência
TEST_Trend = 
VAR VarMes = 
    DIVIDE(
        [Volume_Mes_Atual],
        [Volume_Mes_Anterior]
    ) - 1
RETURN
IF(
    VarMes >= -0.3 && VarMes <= 0.3,
    "OK",
    "ALERTA: Variação suspeita"
)

-- Teste Sazonalidade
TEST_Seasonality = 
VAR VarAno = 
    DIVIDE(
        [Volume_Mes_Atual],
        [Volume_Mes_Ano_Anterior]
    ) - 1
RETURN
IF(
    VarAno >= -0.4 && VarAno <= 0.4,
    "OK",
    "ALERTA: Sazonalidade anormal"
)
```

### 5.2. Validações de Consistência
```dax
-- Teste Acumulado
TEST_YTD = 
VAR YTD_Calc = [Volume_YTD]
VAR YTD_Sum = SUM([Volume_Mensal])
RETURN
IF(
    ABS(YTD_Calc - YTD_Sum) <= 0.01,
    "OK",
    "ERRO: YTD inconsistente"
)

-- Teste Forecast
TEST_Forecast = 
VAR Forecast = [Volume_Forecast]
VAR Historico = [Volume_Historico]
RETURN
IF(
    Forecast >= Historico * 0.7 &&
    Forecast <= Historico * 1.3,
    "OK",
    "ALERTA: Forecast suspeito"
)
```

## 6. Processo de Teste

### 6.1. Rotina Diária
1. Executar testes de integridade
2. Validar totais principais
3. Checar performance
4. Verificar atualizações

### 6.2. Rotina Semanal
1. Testes completos de dados
2. Validações de negócio
3. Análise de tendências
4. Verificação de anomalias

### 6.3. Rotina Mensal
1. Teste full refresh
2. Validação completa
3. Análise de performance
4. Revisão de parâmetros