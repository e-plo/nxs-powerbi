# Arquitetura Power BI - Nexus Ligas

## Visão Geral da Arquitetura
Documentação da arquitetura de integração entre o Power BI e os sistemas da Nexus Ligas, focando na extração de dados do Datasul e distribuição via Power BI Service.

## Sistemas Fonte
- **ERP Principal**: TOTVS Datasul
  - Base Progress
  - Fonte primária de dados transacionais
  - Extração para SQL Server

## Camadas de Dados
1. **Origem (Datasul Progress)**
   - Dados transacionais do ERP
   - Sistema OLTP

2. **Camada SQL**
   - Banco SQL Server
   - Modelos semânticos otimizados
   - Views e procedures para transformação

3. **Camada de Apresentação**
   - Datasets Power BI
   - Relatórios e dashboards
   - Distribuição via Power BI Service

## Fluxo de Dados
1. Extração Datasul (Progress) → SQL Server
2. Modelagem semântica no SQL
3. Conexão Power BI → SQL Server
4. Distribuição → Power BI Service

## Segurança
- Autenticação SQL Server
- RLS (Row Level Security) quando necessário
- Controle de acesso via grupos no Power BI Service

## Ambientes
- DEV: Desenvolvimento e testes
- PROD: Ambiente produtivo

## Stack Tecnológica
- TOTVS Datasul (Progress)
- Microsoft SQL Server
- Power BI Desktop
- Power BI Service