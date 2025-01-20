# Modelo de Dados - Nexus Ligas

## Dimensões Conformadas

### 1. Dim_Produto
```sql
CREATE TABLE Dim_Produto (
    SK_Produto INT,
    Codigo VARCHAR(20),
    Nome VARCHAR(100),
    Especificacao VARCHAR(200),
    Familia VARCHAR(50),
    Grupo VARCHAR(50),
    Teor_Mn DECIMAL(5,2)
)
```

### 2. Dim_Tempo
```sql
CREATE TABLE Dim_Tempo (
    SK_Tempo INT,
    Data DATE,
    Ano INT,
    Mes INT,
    DiaSemana INT,
    Periodo VARCHAR(50),
    CalendarioFiscal VARCHAR(50)
)
```

### 3. Dim_Versao
```sql
CREATE TABLE Dim_Versao (
    SK_Versao INT,
    Codigo VARCHAR(10),
    Nome VARCHAR(50),
    Status VARCHAR(20),
    Ordem INT,
    DataVersao DATE
)
```

## Tabelas Fato por Base Única

### BU-SOP

#### Fato_Plano
```sql
CREATE TABLE Fato_Plano (
    SK_Produto INT,
    SK_Cliente INT,
    SK_Tempo INT,
    SK_Versao INT,
    Volume_Plan DECIMAL(18,3),
    Preco_Plan DECIMAL(18,2),
    Receita_Plan DECIMAL(18,2)
)
```

#### Fato_Carteira
```sql
CREATE TABLE Fato_Carteira (
    SK_Produto INT,
    SK_Cliente INT,
    SK_Tempo INT,
    SK_Versao INT,
    Volume_Cart DECIMAL(18,3),
    Preco_Cart DECIMAL(18,2),
    Status_Pedido VARCHAR(20)
)
```

### BU-OPERACIONAL

#### Fato_Producao
```sql
CREATE TABLE Fato_Producao (
    SK_Produto INT,
    SK_Processo INT,
    SK_Tempo INT,
    SK_Versao INT,
    Volume_Prod DECIMAL(18,3),
    Horas_Prod DECIMAL(18,2),
    Energia_Cons DECIMAL(18,2)
)
```

### BU-CORP

#### Fato_Resultado
```sql
CREATE TABLE Fato_Resultado (
    SK_Produto INT,
    SK_CC INT,
    SK_Tempo INT,
    SK_Versao INT,
    Volume_Real DECIMAL(18,3),
    Receita_Real DECIMAL(18,2),
    Custo_Real DECIMAL(18,2)
)
```

## Relacionamentos

1. **BU-SOP**
   - Fato_Plano -> Dim_Produto (SK_Produto)
   - Fato_Plano -> Dim_Tempo (SK_Tempo)
   - Fato_Plano -> Dim_Versao (SK_Versao)

2. **BU-OPERACIONAL**
   - Fato_Producao -> Dim_Produto (SK_Produto)
   - Fato_Producao -> Dim_Tempo (SK_Tempo)
   - Fato_Producao -> Dim_Versao (SK_Versao)

3. **BU-CORP**
   - Fato_Resultado -> Dim_Produto (SK_Produto)
   - Fato_Resultado -> Dim_Tempo (SK_Tempo)
   - Fato_Resultado -> Dim_Versao (SK_Versao)

## Granularidade

1. **BU-SOP**
   - Fato_Plano: Produto/Cliente/Mês/Versão
   - Fato_Carteira: Produto/Cliente/Dia/Versão

2. **BU-OPERACIONAL**
   - Fato_Producao: Produto/Processo/Dia/Versão
   - Fato_Consumo: Produto/Processo/Dia/Versão

3. **BU-CORP**
   - Fato_Resultado: Produto/CC/Mês/Versão
   - Fato_Custos: CC/Conta/Mês/Versão