# Inventory Analysis Report

## User Story
As a Supply Chain/Production Manager  
I want to visualize inventory evolution in tonnes and monetary values by plant  
So that I can monitor stock levels, identify risks and make strategic supply decisions

## Business Value
- Improve inventory management
- Reduce working capital
- Prevent stockouts of critical materials
- Optimize supply chain decisions
- Enable quick response to inventory deviations

## Acceptance Criteria

### 1. Inventory Views
- **Volume View**
  * Show quantities in tonnes
  * Display by material type (FeMn Products and Strategic Raw Materials)
  * Break down by plant
  * Show inventory days calculation
  * Present historical evolution (12-month history)

- **Value View**
  * Show amounts in BRL
  * Include current and historical average costs
  * Present total inventory value by category
  * Show value evolution trends

### 2. Material Categorization
- **FeMn Products**
  * HC FeMn
  * MC FeMn
  * LC FeMn
  * Other FeMn products

- **Strategic Raw Materials**
  * Manganese Ore
  * Coke
  * Coal
  * Other critical raw materials

### 3. Key Metrics
- **Current Status**
  * Current quantity in tonnes
  * Current value in BRL
  * Inventory days
  * Average daily consumption
  * Min/Max stock levels

- **Variations**
  * MoM variation (vs previous month)
  * YoY variation (vs previous year)
  * Deviation from target levels

### 4. Alerts and Thresholds
- Visual indication for:
  * Below minimum stock level
  * Above maximum stock level
  * Significant variations (>10%)
  * Critical inventory days

## Technical Specifications

### 1. Data Sources
```sql
-- Main tables required
F_Estoque (Inventory)
F_Producao (Production - for consumption)
D_Produto (Product)
D_Centro (Plant)
```

### 2. Key DAX Measures
```dax
// Current Stock in Tonnes
[med]EstoqueAtual = 
CALCULATE(
    SUM(F_Estoque[Quantidade]),
    LASTDATE(F_Estoque[Data])
)

// Inventory Days
[med]DiasEstoque = 
VAR ConsumoMedioDiario = 
    AVERAGEX(
        DATESINPERIOD(
            D_Data[Data],
            MAX(D_Data[Data]),
            -90,
            DAYS
        ),
        [med]ConsumoTotal
    )
RETURN
    DIVIDE(
        [med]EstoqueAtual,
        ConsumoMedioDiario,
        0
    )

// Inventory Value
[med]ValorEstoque = 
    SUMX(
        F_Estoque,
        F_Estoque[Quantidade] * F_Estoque[CustoMedio]
    )

// MoM Variation
[med]VariacaoMoM = 
VAR Atual = [med]EstoqueAtual
VAR Anterior = 
    CALCULATE(
        [med]EstoqueAtual,
        DATEADD(D_Data[Data], -1, MONTH)
    )
RETURN
    DIVIDE(
        Atual - Anterior,
        Anterior,
        0
    )
```

### 3. Report Layout

#### Page 1: Overview
- **Top Filters**
  * Plant
  * Material Category (FeMn/RM)
  * Period
- **Main KPIs**
  * Total Inventory (tonnes)
  * Total Inventory (BRL)
  * Average Inventory Days
- **Charts**
  * Monthly evolution qty/value
  * Distribution by material type
  * Inventory days vs target

#### Page 2: Material Detail
- **Detailed Table**
  * Material
  * Current Quantity
  * Current Value
  * Inventory Days
  * Min/Max
  * Status (traffic light)
- **Drill-down chart by category**

### 4. Interactivity
- Category to material drill-down
- Detailed tooltips on charts
- Synchronized filters between pages
- Excel export capability

### 5. Update Frequency
- Inventory data: Daily
- Average calculations: Rolling 90 days
- History: 13 rolling months

## Dependencies
1. Access to Datasul database
2. Correct material categorization in master data
3. Min/Max levels defined for materials
4. Consumption calculation logic validated

## Validation Scenarios
1. Check total inventory matches Datasul
2. Verify inventory days calculation
3. Validate material categorization
4. Test all filters and drill-downs
5. Confirm alert thresholds

## Notes
- Critical for supply chain decisions
- Requires daily monitoring
- Key report for management meetings
- Mobile visualization important