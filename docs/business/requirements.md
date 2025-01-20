# Requisitos de Negócio - Nexus Ligas

## Objetivos de Negócio

### 1. S&OP (BU-SOP)
1. Integração entre vendas e operações
2. Análise de aderência ao plano
3. Gestão de carteira
4. Forecast de vendas
5. Controle de versões (BGT/MRF)

### 2. Produção (BU-OPERACIONAL)
1. Controle de produção por forno
2. Gestão metalúrgica
3. Controle de qualidade
4. Eficiência operacional
5. Gestão de energia

### 3. Corporativo (BU-CORP)
1. DRE Gerencial
2. Custos por produto
3. Análise de margens
4. EBITDA
5. Working Capital

## Indicadores Chave

### S&OP
1. Volume de Vendas
   - Meta: 5000 ton/mês
   - Medição: Mensal
   - Fonte: Faturamento

2. Aderência ao Plano
   - Meta: 95%
   - Medição: Mensal
   - Base: Volume e Receita

3. Carteira
   - Cobertura: 3 meses
   - Atualização: Diária
   - Composição: Firme + Previsão

### Operacional
1. Produção
   - Meta: 5500 ton/mês
   - Rendimento: 75%
   - OEE: 85%

2. Qualidade
   - Teor Mn: Conforme spec
   - Granulometria: ±5%
   - FMA: < 1%

3. Energia
   - Consumo: 3.5 MWh/ton
   - Demanda: < contratada
   - FC: > 92%

### Corporativo
1. Custos
   - MP: 65%
   - Energia: 20%
   - Outros: 15%

2. Margens
   - Bruta: 25%
   - EBITDA: 15%
   - Líquida: 10%

## Requisitos Funcionais

### Análises Requeridas
1. Comparativo Plan vs Real
2. Análise de Tendências
3. Drill-down por dimensão
4. Simulações de cenário
5. Dashboards executivos

### Funcionalidades
1. Filtros dinâmicos
2. Export para Excel
3. Alertas automáticos
4. Comentários/Notas
5. Sharing controlado

## Requisitos Não Funcionais

### Performance
1. Refresh: < 30 min
2. Resposta: < 5 seg
3. Tamanho: < 500MB

### Segurança
1. RLS por área
2. Logs de acesso
3. Backup diário

### Disponibilidade
1. 24/7
2. Uptime 99%
3. DR Plan