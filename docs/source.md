# Camada Fonte (Datasul)

## Estrutura
- Base de dados Progress
- Sistema TOTVS Datasul ERP
- Módulos utilizados:
  * Vendas (tgf*)
  * Produção (tap*)
  * Estoque (tgf*)
  * Custos (tpc*)

## Tabelas Principais
```sql
-- Vendas
TGFCAB -- Cabeçalho de pedidos/notas
TGFITE -- Itens de pedidos/notas
TGFPAR -- Parceiros (clientes/fornecedores)

-- Produção
TAPORD -- Ordens de produção
TAPOPI -- Itens de ordem de produção
TAPORT -- Operações de produção

-- Estoque
TGFEST -- Saldos de estoque
TGFMOV -- Movimentações
TGFPRO -- Produtos
```

## Atualização
- Frequência: Tempo real (transacional)
- Latência máxima: 1 segundo
- Horário de backup: 23:00

## Conexão
- Servidor: SRVDATASUL
- Porta: 20xxx
- Método: ODBC Progress
- Usuário: usr_bi (somente leitura)

## Monitoramento
- Log de transações
- Alerta de indisponibilidade
- Controle de performance

## Responsáveis
- TI Infraestrutura
- DBA Datasul
- Suporte TOTVS