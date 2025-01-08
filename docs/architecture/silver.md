{
  `path`: `C:\\Users\\flying_ace35\\Documents\\apps\
xs-powerbi\\docs\\architecture\\silver.md`,
  `content`: `# Camada Silver - Data Warehouse

## Visão Geral

A camada Silver implementa o modelo dimensional (Star Schema) do Data Warehouse, transformando os dados brutos da camada Bronze em estruturas otimizadas para análise.

```mermaid
flowchart TD
    subgraph DW[\"Data Warehouse\"]
        subgraph FT[\"Tabelas Fato\"]
            FTV[\"Vendas\"]
            FTP[\"Produção\"]
            FTC[\"Compras\"]
            FTE[\"Estoque\"]
        end
        
        subgraph DM[\"Dimensões\"]
            DMP[\"Produto\"]
            DMC[\"Cliente\"]
            DMF[\"Fornecedor\"]
            DMT[\"Tempo\"]
            DMD[\"Depósito\"]
            DME[\"Estabelecimento\"]
        end
        
        DMP --> FTV & FTP & FTC & FTE
        DMC --> FTV
        DMF --> FTC
        DMT --> FTV & FTP & FTC & FTE
        DMD --> FTE
        DME --> FTV & FTP & FTC & FTE
    end

    %% High contrast light theme for better visibility
    classDef fact fill:#f5f5f5,stroke:#000000,stroke-width:2px,color:#000000
    classDef dim fill:#ffffff,stroke:#000000,stroke-width:2px,color:#000000
    classDef container fill:none,stroke:#000000,stroke-width:2px,color:#ffffff

    class FTV,FTP,FTC,FTE fact
    class DMP,DMC,DMF,DMT,DMD,DME dim
    class DW,FT,DM container
```

## Estrutura Dimensional

### Dimensões Principais

#### 1. Produto (DIM_Produto)
```sql
CREATE TABLE dw.DIM_Produto (
    SK_Produto INT IDENTITY(1,1),
    NK_Produto VARCHAR(20),      -- Natural Key do Datasul
    Codigo_Produto VARCHAR(20),
    Descricao_Produto VARCHAR(100),
    Tipo_Produto VARCHAR(50),
    Grupo_Produto VARCHAR(50),
    Subgrupo_Produto VARCHAR(50),
    Unidade_Medida VARCHAR(10),
    Peso_Liquido DECIMAL(18,4),
    Peso_Bruto DECIMAL(18,4),
    Status_Produto VARCHAR(20),
    Data_Cadastro DATE,
    Data_Ultima_Compra DATE,
    Data_Ultima_Venda DATE,
    Flag_Ativo BIT,
    Data_Inicio_Vigencia DATETIME,
    Data_Fim_Vigencia DATETIME,
    Versao_Atual BIT,
    CONSTRAINT PK_DIM_Produto PRIMARY KEY (SK_Produto)
);
```

#### 2. Tempo (DIM_Tempo)
```sql
CREATE TABLE dw.DIM_Tempo (
    SK_Tempo INT,               -- YYYYMMDD
    Data DATE,
    Ano INT,
    Semestre INT,
    Trimestre INT,
    Mes INT,
    Nome_Mes VARCHAR(20),
    Semana_Ano INT,
    Dia_Semana INT,
    Nome_Dia_Semana VARCHAR(20),
    Dia_Util BIT,
    Feriado BIT,
    Nome_Feriado VARCHAR(50),
    CONSTRAINT PK_DIM_Tempo PRIMARY KEY (SK_Tempo)
);
```

#### 3. Cliente (DIM_Cliente)
```sql
CREATE TABLE dw.DIM_Cliente (
    SK_Cliente INT IDENTITY(1,1),
    NK_Cliente VARCHAR(20),      -- Natural Key do Datasul
    Razao_Social VARCHAR(100),
    Nome_Fantasia VARCHAR(100),
    CNPJ VARCHAR(14),
    Tipo_Cliente VARCHAR(50),
    Segmento VARCHAR(50),
    Estado VARCHAR(2),
    Cidade VARCHAR(100),
    Data_Cadastro DATE,
    Status_Cliente VARCHAR(20),
    Data_Inicio_Vigencia DATETIME,
    Data_Fim_Vigencia DATETIME,
    Versao_Atual BIT,
    CONSTRAINT PK_DIM_Cliente PRIMARY KEY (SK_Cliente)
);
```

#### 4. Estabelecimento (DIM_Estabelecimento)
```sql
CREATE TABLE dw.DIM_Estabelecimento (
    SK_Estabelecimento INT IDENTITY(1,1),
    NK_Estabelecimento VARCHAR(20),  -- Natural Key do Datasul
    Codigo_Estabelecimento VARCHAR(20),
    Nome_Estabelecimento VARCHAR(100),
    CNPJ VARCHAR(14),
    Razao_Social VARCHAR(100),
    Cidade VARCHAR(100),
    Estado VARCHAR(2),
    CEP VARCHAR(8),
    Status_Estabelecimento VARCHAR(20),
    Data_Inicio_Vigencia DATETIME,
    Data_Fim_Vigencia DATETIME,
    Versao_Atual BIT,
    CONSTRAINT PK_DIM_Estabelecimento PRIMARY KEY (SK_Estabelecimento)
);
```

#### 5. Fornecedor (DIM_Fornecedor)
```sql
CREATE TABLE dw.DIM_Fornecedor (
    SK_Fornecedor INT IDENTITY(1,1),
    NK_Fornecedor VARCHAR(20),    -- Natural Key do Datasul
    Razao_Social VARCHAR(100),
    Nome_Fantasia VARCHAR(100),
    CNPJ VARCHAR(14),
    Tipo_Fornecedor VARCHAR(50),
    Categoria VARCHAR(50),
    Estado VARCHAR(2),
    Cidade VARCHAR(100),
    Status_Fornecedor VARCHAR(20),
    Data_Cadastro DATE,
    Data_Ultima_Compra DATE,
    Data_Inicio_Vigencia DATETIME,
    Data_Fim_Vigencia DATETIME,
    Versao_Atual BIT,
    CONSTRAINT PK_DIM_Fornecedor PRIMARY KEY (SK_Fornecedor)
);
```

#### 6. Depósito (DIM_Deposito)
```sql
CREATE TABLE dw.DIM_Deposito (
    SK_Deposito INT IDENTITY(1,1),
    NK_Deposito VARCHAR(20),     -- Natural Key do Datasul
    Codigo_Deposito VARCHAR(20),
    Nome_Deposito VARCHAR(100),
    Tipo_Deposito VARCHAR(50),
    SK_Estabelecimento INT,
    Status_Deposito VARCHAR(20),
    Data_Inicio_Vigencia DATETIME,
    Data_Fim_Vigencia DATETIME,
    Versao_Atual BIT,
    CONSTRAINT PK_DIM_Deposito PRIMARY KEY (SK_Deposito),
    CONSTRAINT FK_DIM_Deposito_Estabelecimento FOREIGN KEY (SK_Estabelecimento)
        REFERENCES dw.DIM_Estabelecimento (SK_Estabelecimento)
);
```

### Fatos

#### 1. Produção (FT_Producao)
```sql
CREATE TABLE dw.FT_Producao (
    SK_Producao BIGINT IDENTITY(1,1),
    SK_Produto INT,
    SK_Tempo INT,
    SK_Estabelecimento INT,
    NK_Ordem_Producao INT,
    Quantidade_Planejada DECIMAL(18,4),
    Quantidade_Produzida DECIMAL(18,4),
    Quantidade_Refugada DECIMAL(18,4),
    Tempo_Planejado DECIMAL(18,2),
    Tempo_Realizado DECIMAL(18,2),
    Custo_Planejado DECIMAL(18,2),
    Custo_Realizado DECIMAL(18,2),
    Flag_Ordem_Encerrada BIT,
    CONSTRAINT PK_FT_Producao PRIMARY KEY (SK_Producao),
    CONSTRAINT FK_FT_Producao_Produto FOREIGN KEY (SK_Produto) 
        REFERENCES dw.DIM_Produto (SK_Produto),
    CONSTRAINT FK_FT_Producao_Tempo FOREIGN KEY (SK_Tempo) 
        REFERENCES dw.DIM_Tempo (SK_Tempo),
    CONSTRAINT FK_FT_Producao_Estabelecimento FOREIGN KEY (SK_Estabelecimento)
        REFERENCES dw.DIM_Estabelecimento (SK_Estabelecimento)
);
```

#### 2. Vendas (FT_Vendas)
```sql
CREATE TABLE dw.FT_Vendas (
    SK_Venda BIGINT IDENTITY(1,1),
    SK_Produto INT,
    SK_Cliente INT,
    SK_Tempo INT,
    SK_Estabelecimento INT,
    NK_Pedido_Venda INT,
    Quantidade_Vendida DECIMAL(18,4),
    Valor_Unitario DECIMAL(18,4),
    Valor_Total DECIMAL(18,2),
    Custo_Unitario DECIMAL(18,4),
    Custo_Total DECIMAL(18,2),
    Margem_Contribuicao DECIMAL(18,2),
    CONSTRAINT PK_FT_Vendas PRIMARY KEY (SK_Venda),
    CONSTRAINT FK_FT_Vendas_Produto FOREIGN KEY (SK_Produto)
        REFERENCES dw.DIM_Produto (SK_Produto),
    CONSTRAINT FK_FT_Vendas_Cliente FOREIGN KEY (SK_Cliente)
        REFERENCES dw.DIM_Cliente (SK_Cliente),
    CONSTRAINT FK_FT_Vendas_Tempo FOREIGN KEY (SK_Tempo)
        REFERENCES dw.DIM_Tempo (SK_Tempo),
    CONSTRAINT FK_FT_Vendas_Estabelecimento FOREIGN KEY (SK_Estabelecimento)
        REFERENCES dw.DIM_Estabelecimento (SK_Estabelecimento)
);
```

#### 3. Compras (FT_Compras)
```sql
CREATE TABLE dw.FT_Compras (
    SK_Compra BIGINT IDENTITY(1,1),
    SK_Produto INT,
    SK_Fornecedor INT,
    SK_Tempo INT,
    SK_Estabelecimento INT,
    NK_Ordem_Compra INT,
    Quantidade_Comprada DECIMAL(18,4),
    Valor_Unitario DECIMAL(18,4),
    Valor_Total DECIMAL(18,2),
    Prazo_Entrega INT,
    Status_Entrega VARCHAR(20),
    CONSTRAINT PK_FT_Compras PRIMARY KEY (SK_Compra),
    CONSTRAINT FK_FT_Compras_Produto FOREIGN KEY (SK_Produto)
        REFERENCES dw.DIM_Produto (SK_Produto),
    CONSTRAINT FK_FT_Compras_Fornecedor FOREIGN KEY (SK_Fornecedor)
        REFERENCES dw.DIM_Fornecedor (SK_Fornecedor),
    CONSTRAINT FK_FT_Compras_Tempo FOREIGN KEY (SK_Tempo)
        REFERENCES dw.DIM_Tempo (SK_Tempo),
    CONSTRAINT FK_FT_Compras_Estabelecimento FOREIGN KEY (SK_Estabelecimento)
        REFERENCES dw.DIM_Estabelecimento (SK_Estabelecimento)
);
```

#### 4. Estoque (FT_Estoque)
```sql
CREATE TABLE dw.FT_Estoque (
    SK_Estoque BIGINT IDENTITY(1,1),
    SK_Produto INT,
    SK_Tempo INT,
    SK_Estabelecimento INT,
    SK_Deposito INT,
    Quantidade_Disponivel DECIMAL(18,4),
    Quantidade_Reservada DECIMAL(18,4),
    Quantidade_Bloqueada DECIMAL(18,4),
    Valor_Medio_Unitario DECIMAL(18,4),
    Valor_Total DECIMAL(18,2),
    Data_Ultima_Movimentacao DATE,
    CONSTRAINT PK_FT_Estoque PRIMARY KEY (SK_Estoque),
    CONSTRAINT FK_FT_Estoque_Produto FOREIGN KEY (SK_Produto)
        REFERENCES dw.DIM_Produto (SK_Produto),
    CONSTRAINT FK_FT_Estoque_Tempo FOREIGN KEY (SK_Tempo)
        REFERENCES dw.DIM_Tempo (SK_Tempo),
    CONSTRAINT FK_FT_Estoque_Estabelecimento FOREIGN KEY (SK_Estabelecimento)
        REFERENCES dw.DIM_Estabelecimento (SK_Estabelecimento),
    CONSTRAINT FK_FT_Estoque_Deposito FOREIGN KEY (SK_Deposito)
        REFERENCES dw.DIM_Deposito (SK_Deposito)
);
```

## Processo ETL

### 1. Carga de Dimensões

#### Dimensão Produto
```sql
CREATE PROCEDURE dw.sp_Carga_DIM_Produto
AS
BEGIN
    SET NOCOUNT ON;
    BEGIN TRY
        BEGIN TRANSACTION;
        
        -- Identificar novos registros e alterações
        WITH Changes AS (
            SELECT 
                p.cod_produto,
                p.descricao,
                p.tipo,
                p.grupo,
                p.subgrupo,
                p.unidade,
                p.peso_liquido,
                p.peso_bruto,
                p.status,
                p.data_cadastro
            FROM bronze.datasul.est_produto p
            LEFT JOIN dw.DIM_Produto d 
                ON p.cod_produto = d.NK_Produto 
                AND d.Versao_Atual = 1
            WHERE d.SK_Produto IS NULL 
                OR p.descricao <> d.Descricao_Produto
                OR p.status <> d.Status_Produto
        )
        
        -- Atualizar registros existentes (fechar versão atual)
        UPDATE d
        SET 
            Data_Fim_Vigencia = GETDATE(),
            Versao_Atual = 0
        FROM dw.DIM_Produto d
        INNER JOIN Changes c ON d.NK_Produto = c.cod_produto
        WHERE d.Versao_Atual = 1;
        
        -- Inserir novos registros
        INSERT INTO dw.DIM_Produto (
            NK_Produto,
            Codigo_Produto,
            Descricao_Produto,
            Tipo_Produto,
            Grupo_Produto,
            Subgrupo_Produto,
            Unidade_Medida,
            Peso_Liquido,
            Peso_Bruto,
            Status_Produto,
            Data_Cadastro,
            Data_Inicio_Vigencia,
            Data_Fim_Vigencia,
            Versao_Atual
        )
        SELECT 
            cod_produto,
            cod_produto,
            descricao,
            tipo,
            grupo,
            subgrupo,
            unidade`
}