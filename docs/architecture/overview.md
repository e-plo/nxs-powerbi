# Nexus Ligas - Visão Geral da Arquitetura

## Objetivo
Estruturar bases únicas para suportar análises e gestão da Nexus Ligas, empresa siderúrgica de manganês, com foco em performance e manutenibilidade.

## Bases Únicas Principais

### 1. BU-SOP (Sales & Operations Planning)
- Integração entre planejamento comercial e operacional
- Comparativo entre versões (BGT/MRF/ACTUAL)
- KPIs de aderência ao plano

### 2. BU-OPERACIONAL (Gestão de Produção)
- Gestão do processo produtivo
- Indicadores metalúrgicos
- Controle de qualidade

### 3. BU-CORP (Gestão Corporativa)
- Resultados consolidados
- Gestão de custos
- KPIs financeiros

## Princípios da Arquitetura

1. **Dimensões Conformadas**
   - Produto
   - Tempo
   - Versão

2. **Versionamento**
   - Budget (BGT)
   - Monthly Rolling Forecast (MRF)
   - Realizado (ACTUAL)

3. **Fontes de Dados**
   - Datasul EMS (ACTUAL)
   - Planilhas estruturadas (BGT/MRF)

4. **Processo ETL**
   - Extração das fontes
   - Staging Area
   - Carga dimensional

## Critérios de Sucesso

1. **Performance**
   - Refresh em até 30 minutos
   - PBIX < 500MB
   - Resposta < 5 segundos

2. **Governança**
   - Versionamento de código
   - Documentação atualizada
   - Processo de backup

3. **Usabilidade**
   - Interface intuitiva
   - Análise drill-through
   - Filtros contextuais