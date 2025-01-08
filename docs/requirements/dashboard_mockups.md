# Dashboard Mockups - Power BI Governance Nexus

## Sales Performance Dashboard

```mermaid
graph TD
    subgraph Header
        Title["Sales Performance Dashboard"]
        DateFilter["Date Filter"] --> Title
        RegionFilter["Region Filter"] --> Title
        ProductFilter["Product Filter"] --> Title
    end

    subgraph KPISection["Key Metrics"]
        direction LR
        TotalSales["Total Sales\n$ 1.2M\n↑ 12%"]
        AvgMargin["Avg Margin\n24.5%\n↓ 2%"]
        ActiveCustomers["Active Customers\n145\n↑ 5"]
        OpenOrders["Open Orders\n32\n↑ 3"]
    end

    subgraph Charts
        direction TB
        subgraph Row1
            direction LR
            SalesTrend["Sales Trend\nLine Chart\nMonthly Sales vs Target"]
            ProductMix["Product Mix\nDonut Chart\nSales by Category"]
        end
        
        subgraph Row2
            direction LR
            RegionMap["Regional Performance\nMap Visual\nSales by Region"]
            TopCustomers["Top Customers\nBar Chart\nTop 10 by Revenue"]
        end
        
        subgraph Row3
            direction LR
            MarginAnalysis["Margin Analysis\nScatter Plot\nRevenue vs Margin"]
            PaymentStatus["Payment Status\nStacked Bar\nAging Analysis"]
        end
    end

    Title --> KPISection
    KPISection --> Charts
```

## Production Performance Dashboard

```mermaid
graph TD
    subgraph Header
        Title["Production Performance Dashboard"]
        DateFilter["Date Filter"] --> Title
        LineFilter["Production Line"] --> Title
        ProductFilter["Product Filter"] --> Title
    end

    subgraph KPISection["Production Metrics"]
        direction LR
        OEE["OEE\n85.2%\n↑ 1.2%"]
        OutputRate["Output Rate\n520/hr\n↑ 15"]
        QualityRate["Quality Rate\n99.1%\n↓ 0.2%"]
        Downtime["Downtime\n45min\n↓ 15min"]
    end

    subgraph Charts
        direction TB
        subgraph Row1
            direction LR
            ProductionTrend["Production Trend\nLine Chart\nHourly Output"]
            QualityMetrics["Quality Metrics\nColumn Chart\nDefect Rates"]
        end
        
        subgraph Row2
            direction LR
            ResourceUtil["Resource Utilization\nHeat Map\nBy Line & Shift"]
            DowntimePareto["Downtime Analysis\nPareto Chart\nTop Issues"]
        end
        
        subgraph Row3
            direction LR
            CostAnalysis["Cost Analysis\nArea Chart\nProduction Cost"]
            Compliance["Schedule Compliance\nGauge\nPlan vs Actual"]
        end
    end

    Title --> KPISection
    KPISection --> Charts
```

## Inventory Overview Dashboard

```mermaid
graph TD
    subgraph Header
        Title["Inventory Overview Dashboard"]
        DateFilter["Date Filter"] --> Title
        LocationFilter["Location Filter"] --> Title
        CategoryFilter["Category Filter"] --> Title
    end

    subgraph KPISection["Inventory Metrics"]
        direction LR
        TotalValue["Total Value\n$ 2.5M\n↓ 5%"]
        TurnoverRate["Turnover\n4.2x\n↑ 0.3"]
        Stockouts["Stockouts\n3\n↓ 2"]
        Accuracy["Accuracy\n98.5%\n↑ 0.5%"]
    end

    subgraph Charts
        direction TB
        subgraph Row1
            direction LR
            InventoryTrend["Inventory Trend\nArea Chart\nValue Over Time"]
            ABCAnalysis["ABC Analysis\nTreemap\nBy Value"]
        end
        
        subgraph Row2
            direction LR
            LocationUtil["Location Utilization\nHeat Map\nBy Zone"]
            AgingAnalysis["Aging Analysis\nStacked Column\nBy Category"]
        end
        
        subgraph Row3
            direction LR
            StockLevel["Stock Levels\nBullet Chart\nMin/Max/Current"]
            MovementAnalysis["Movement Analysis\nLine Chart\nIn/Out Flow"]
        end
    end

    Title --> KPISection
    KPISection --> Charts
```

## Common Features Across Dashboards

### Navigation & Interactivity
- Consistent header with filters
- Drill-down capabilities on all charts
- Tool tips with detailed information
- Bookmark support for saved views
- Cross-filtering enabled

### Visual Elements
- Corporate color scheme:
  * Primary: #9932cc (Purple)
  * Secondary: #ffa500 (Orange)
  * Accent: #4a90e2 (Blue)
- Consistent font hierarchy:
  * Title: Segoe UI, 24px
  * Subtitles: Segoe UI, 18px
  * Body: Segoe UI, 12px
- Icon set for status indicators:
  * ↑ - Improvement
  * ↓ - Decline
  * → - No change

### Mobile Optimization
- KPI section always visible
- Scrollable chart section
- Touch-optimized filter pane
- Responsive chart sizing

### Drill-Through Options
- From Sales to Customer Details
- From Production to Line Details
- From Inventory to Item Details

## Implementation Notes

### Data Refresh
- Sales: 15-minute intervals
- Production: 5-minute intervals
- Inventory: Hourly updates

### Performance Targets
- Page load: < 3 seconds
- Filter response: < 1 second
- Drill-through: < 2 seconds

### Security Requirements
- Row-level security by:
  * Region (Sales)
  * Production Line
  * Warehouse Location