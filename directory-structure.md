# Nexus Ligas - Power BI Project Structure

```
nxs-powerbi/
│
├── docs/                           # Documentation
│   ├── architecture/              # Architecture documentation
│   │   ├── overview.md           # High-level architecture
│   │   ├── data-model.md         # Data model documentation
│   │   └── etl-process.md        # ETL process documentation
│   │
│   ├── business/                 # Business documentation
│   │   ├── requirements.md       # Business requirements
│   │   └── metrics.md            # Metrics definitions
│   │
│   └── technical/                # Technical documentation
│       ├── datasul-tables.md     # Datasul table mappings
│       └── maintenance.md        # Maintenance procedures
│
├── src/                          # Source code
│   ├── pbix/                     # Power BI files
│   │   ├── bu-sop/              # S&OP Base Única
│   │   │   ├── bu-sop.pbix      # Main file
│   │   │   └── dataset/         # Dataset files (TMDL)
│   │   │
│   │   ├── bu-operacional/      # Operational Base Única
│   │   │   ├── bu-operacional.pbix
│   │   │   └── dataset/
│   │   │
│   │   └── bu-corp/            # Corporate Base Única
│   │       ├── bu-corp.pbix
│   │       └── dataset/
│   │
│   └── etl/                     # ETL processes
│       ├── queries/             # SQL queries
│       │   ├── actual/         # ACTUAL version queries
│       │   └── plan/          # BGT/MRF version queries
│       │
│       ├── transforms/         # Data transformations
│       └── load/              # Load procedures
│
├── data/                       # Data files
│   ├── input/                 # Input files
│   │   ├── bgt/              # Budget files
│   │   └── mrf/              # MRF files
│   │
│   └── output/               # Output files
│
├── tests/                     # Testing
│   ├── data-quality/         # Data quality tests
│   └── performance/          # Performance tests
│
└── tools/                     # Support tools and scripts
    ├── refresh/              # Refresh scripts
    └── maintenance/          # Maintenance scripts
```

## Key Directories Explained

### /docs
Contains all project documentation, separated into architectural, business, and technical concerns.

### /src/pbix
Contains the three main Power BI files and their associated dataset definitions.

### /src/etl
Houses all ETL-related code and procedures, organized by process stage.

### /data
Stores input files for BGT and MRF versions, plus any output files generated.

### /tests
Contains test definitions and resources for ensuring data quality and performance.

### /tools
Utility scripts and tools for project maintenance and operation.

## Version Control Guidelines

1. **PBIX Files**
   - Use PBIP format for better version control
   - Commit dataset changes separately from report changes
   - Use meaningful commit messages

2. **Documentation**
   - Keep documentation up-to-date with changes
   - Document all business rules and transformations
   - Maintain change log

3. **ETL**
   - Version control all queries and procedures
   - Document dependencies
   - Include error handling procedures