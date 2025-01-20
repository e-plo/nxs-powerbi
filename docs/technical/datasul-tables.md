# Mapeamento de Tabelas Datasul

## Comercial

### Pedidos e Notas
```sql
-- Cabeçalho de Pedidos e Notas
SELECT 
    cab.num_pedido,
    cab.cod_cliente,
    cab.dat_emissao,
    cab.dat_entreg,
    cab.cod_transp,
    cab.cod_rep,
    cab.num_nota,
    cab.ser_nota
FROM tgfcab cab
WHERE cab.dat_emissao >= @data_inicio

-- Itens de Pedidos e Notas
SELECT 
    ite.num_pedido,
    ite.cod_item,
    ite.qtd_pedida,
    ite.qtd_entregue,
    ite.vlr_unit,
    ite.vlr_total,
    ite.cod_local
FROM tgfite ite
WHERE ite.dat_emissao >= @data_inicio
```

### Clientes
```sql
SELECT 
    cli.cod_cliente,
    cli.razao_social,
    cli.nome_fantasia,
    cli.cgc_cpf,
    cli.cod_cidade,
    cli.cod_ramo,
    cli.cod_grpcli
FROM tcicli cli
```

## Produção

### Ordens de Produção
```sql
-- Cabeçalho OP
SELECT 
    ord.num_ord,
    ord.cod_item,
    ord.qtd_ord,
    ord.dat_ini,
    ord.dat_fim,
    ord.cod_local,
    ord.cod_ccusto
FROM tfpord ord
WHERE ord.dat_ini >= @data_inicio

-- Apontamentos
SELECT 
    ap1.num_ord,
    ap1.seq_ocor,
    ap1.dat_apon,
    ap1.qtd_prod,
    ap1.tmp_prod,
    ap1.cod_ocor,
    ap1.cod_par
FROM tfpap1 ap1
WHERE ap1.dat_apon >= @data_inicio
```

### Roteiros e Estruturas
```sql
-- Roteiro
SELECT 
    rot.cod_item,
    rot.cod_roteiro,
    rot.cod_operacao,
    rot.tmp_setup,
    rot.tmp_prod,
    rot.cod_recurso
FROM tfprot rot

-- Estrutura
SELECT 
    emp.cod_item,
    emp.cod_comp,
    emp.qtd_comp,
    emp.cod_formula,
    emp.cod_undmed
FROM tfpemp emp
```

## Estoque

### Saldos e Movimentos
```sql
-- Saldos
SELECT 
    est.cod_item,
    est.cod_local,
    est.qtd_saldo,
    est.dat_saldo,
    est.vlr_saldo
FROM tgfest est
WHERE est.dat_saldo >= @data_inicio

-- Movimentos
SELECT 
    mov.cod_item,
    mov.cod_local,
    mov.qtd_mov,
    mov.dat_mov,
    mov.cod_trans,
    mov.vlr_unit
FROM tgfmov mov
WHERE mov.dat_mov >= @data_inicio
```

## Custos

### Lançamentos e Rateios
```sql
-- Lançamentos
SELECT 
    lan.num_lanc,
    lan.dat_lanc,
    lan.cod_ccusto,
    lan.cod_conta,
    lan.vlr_lanc,
    lan.cod_parceiro
FROM tcblan lan
WHERE lan.dat_lanc >= @data_inicio

-- Rateios
SELECT 
    rat.num_rateio,
    rat.cod_ccusto,
    rat.cod_conta,
    rat.vlr_rateio,
    rat.per_rateio
FROM tcbrat rat
WHERE rat.dat_rateio >= @data_inicio
```

## Campos Importantes

### Dimensão Produto (SB1)
- cod_item: Código do produto
- den_item: Descrição
- cod_unimed: Unidade medida
- cod_grpprod: Grupo
- cod_marca: Marca/Família
- peso_unit: Peso unitário
- cod_sit: Situação

### Dimensão Cliente (CLI)
- cod_cliente: Código
- razao_social: Nome
- cgc_cpf: CNPJ/CPF
- cod_grpcli: Grupo
- cod_ramo: Ramo atividade
- cod_cidade: Cidade
- dat_cadastro: Data cadastro

### Dimensão Centro Trabalho (CTR)
- cod_centro: Código
- den_centro: Nome
- cod_ccusto: Centro custo
- cod_recurso: Recurso
- dat_inicial: Data inicial
- ind_situacao: Situação

### Dimensão Conta (CTA)
- cod_conta: Código
- den_conta: Nome
- cod_grpcta: Grupo
- ind_natureza: Natureza
- ind_ctared: Reduzida
- cod_classif: Classificação

## Regras de Extração

1. **Filtros Padrão**
   - Sempre usar dat_* >= @data_inicio
   - Filtrar registros ativos (cod_sit = 'A')
   - Respeitar empresa/filial

2. **Joins Necessários**
   - Usar INNER JOIN entre cab/ite
   - LEFT JOIN para tabelas de domínio
   - Validar cardinalidade

3. **Campos Calculados**
   - Converter unidades quando necessário
   - Aplicar taxas/fatores
   - Tratar nulos