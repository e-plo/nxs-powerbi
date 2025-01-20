# Processo ETL - Nexus Ligas

## Visão Geral do ETL

### Fluxo ACTUAL (Datasul)
1. Extração via SQL das tabelas Datasul
2. Transformação na staging area
3. Carga nas tabelas fato

### Fluxo BGT/MRF (Planilhas)
1. Leitura dos arquivos de input
2. Validação e transformação
3. Carga nas tabelas fato

## Processo Detalhado

### 1. Extração

#### Datasul
```sql
-- Exemplo de extração de pedidos
SELECT 
    cab.num_pedido,
    cab.cod_cliente,
    ite.cod_item,
    ite.qtd_pedida,
    ite.vlr_unit
FROM tgfcab cab
JOIN tgfite ite ON cab.num_pedido = ite.num_pedido
WHERE cab.data_movto >= @data_inicio
```

#### Planilhas
- Formato padronizado
- Validação de estrutura
- Controle de versões

### 2. Transformação

#### Staging Area
1. Padronização de campos
2. Tratamento de nulos
3. Conversão de unidades
4. Validações de negócio

#### Regras de Negócio
1. Cálculo de valores
2. Aplicação de taxas
3. Conversões monetárias
4. Agregações

### 3. Carga

#### Dimensões
1. Carga incremental
2. Tratamento SCD Tipo 2
3. Geração de SKs

#### Fatos
1. Merge com dimensões
2. Validação de integridade
3. Controle de versões

## Agendamento

### Cargas Diárias
- ACTUAL: 06:00
- Dimensões: 05:30

### Cargas Mensais
- BGT: Dia 1
- MRF: Dia 15

## Monitoria

### Logs
- Registro de execução
- Controle de erros
- Alertas automáticos

### Validações
1. Integridade referencial
2. Totais de controle
3. Regras de negócio

## Contingência

### Falhas
1. Retry automático
2. Notificação da equipe
3. Processo manual

### Rollback
1. Backup point
2. Restore procedure
3. Validação pós-restore

## Manutenção

### Rotinas
1. Limpeza de staging
2. Compactação de dados
3. Atualização de estatísticas

### Documentação
1. Registro de mudanças
2. Controle de versões
3. Histórico de execuções