# Nexus Ligas - Arquitetura Power BI

## Visão Geral
Arquitetura de bases únicas para a Nexus Ligas, uma siderúrgica de manganês, focando em três PBIX's principais otimizados para performance e manutenção.

## Dimensões Comuns (Conformed Dimensions)

1. **Dim_Produto**
   - SK_Produto
   - Código/Nome
   - Especificação
   - Família/Grupo
   - Teor_Mn

2. **Dim_Tempo**
   - SK_Tempo
   - Data/Período
   - Ano/Mês/Dia
   - Calendário Fiscal

3. **Dim_Versao**
   - SK_Versao
   - BGT/MRF/Real
   - Status/Ordem
   - Data_Versao

## Bases Únicas

### 1. BU-SOP.PBIX

#### Dimensões Específicas
- Dim_Cliente (SK_Cliente, Código/Nome, Grupo/Mercado)
- Dim_Mercado (SK_Mercado, Região/Setor)

#### Fatos
- **Fato_Plano** (BGT/MRF)
  * SK_Produto, SK_Cliente, SK_Tempo, SK_Versao
  * Volume_Plan, Preco_Plan, Receita_Plan
- **Fato_Carteira** (ACTUAL)
  * SK_Produto, SK_Cliente, SK_Tempo, SK_Versao
  * Volume_Cart, Preco_Cart, Status_Pedido

### 2. BU-OPERACIONAL.PBIX

#### Dimensões Específicas
- Dim_Processo (SK_Processo, Forno/Linha, Capacidade)
- Dim_Insumo (SK_Insumo, Tipo/Origem, Teor_Base)
- Dim_Qualidade (SK_Qualidade, Parametro/Limite)

#### Fatos
- **Fato_Producao** (ALL)
  * SK_Produto, SK_Processo, SK_Tempo, SK_Versao
  * Volume_Prod, Horas_Prod, Energia_Cons
- **Fato_Consumo** (ALL)
  * SK_Produto, SK_Processo, SK_Insumo, SK_Tempo, SK_Versao
  * Volume_Cons, Teor_Real
- **Fato_Qualidade** (ACTUAL)
  * SK_Produto, SK_Processo, SK_Qualidade, SK_Tempo, SK_Versao
  * Valor_Medido, Status_Qual

### 3. BU-CORP.PBIX

#### Dimensões Específicas
- Dim_CC (SK_CC, Centro/Área, Hierarquia)
- Dim_Conta (SK_Conta, Natureza/Grupo, Tipo)

#### Fatos
- **Fato_Resultado** (ALL)
  * SK_Produto, SK_CC, SK_Tempo, SK_Versao
  * Volume_Real, Receita_Real, Custo_Real
- **Fato_Custos** (ALL)
  * SK_CC, SK_Conta, SK_Tempo, SK_Versao
  * Valor_Fix, Valor_Var

## Fontes de Dados (ACTUAL)

### Datasul EMS

1. **Comercial**
   - tgfcab/tgfite (Pedidos e Notas)
   - tcicli (Clientes)

2. **Produção**
   - tfpord (Ordens)
   - tfpap1 (Apontamentos)
   - tfpmov (Movimentos)
   - tfprot/tfpemp (Roteiros/Estruturas)

3. **Estoque**
   - tgfest (Estoque)
   - tgfmov (Movimentações)
   - tgfsal (Saldos)

4. **Custos**
   - tcblan (Lançamentos)
   - tcbrat (Rateios)
   - tcccus (Centro Custo)

### Planejamento (BGT/MRF)
- Inputs via Excel/Planilhas
- Processo manual estruturado
- Versionamento controlado

## Processo ETL

1. **Extração**
   - Datasul (ACTUAL)
   - Planilhas (BGT/MRF)

2. **Transformação**
   - Staging Area
   - Padronização
   - Tratamentos

3. **Carga**
   - Dimensões
   - Fatos por Versão
   - Refresh Incremental

## Boas Práticas

1. **Modelagem**
   - Dimensões conformadas
   - Modelo estrela puro
   - Granularidade controlada

2. **Performance**
   - Otimização DAX
   - Particionamento
   - Refresh incremental

3. **Governança**
   - Versionamento
   - Documentação
   - Backup