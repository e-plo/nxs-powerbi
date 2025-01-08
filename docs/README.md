# Documentation - Power BI Governance Nexus Ligas

This directory contains the complete documentation for the Power BI Governance implementation at Nexus Ligas.

## Structure

```
docs/
├── architecture/        # Technical architecture specs
│   ├── bronze.md       # Bronze layer details
│   ├── silver.md       # Silver layer specifications
│   ├── gold.md         # Gold layer documentation
│   ├── source.md       # Source systems integration
│   └── README.md       # Architecture overview
├── requirements/        # Project requirements
│   ├── backlog.md      # Product backlog
│   └── user_stories.md # User stories and acceptance criteria
├── data-architecture.md # Data architecture and flows
├── governance.md       # Governance framework
├── implementation_plan.md # Implementation phases
├── publish.md         # Publishing procedures
└── timeline.md        # Project timeline
```

## Core Documents

### Architecture
The `architecture/` directory contains detailed specifications for each layer of our medallion architecture:
- **Bronze**: SQL Server implementation and CDC setup
- **Silver**: Data warehouse design and ETL processes
- **Gold**: Power BI semantic model and security implementation

### Requirements
The `requirements/` directory includes:
- Business requirements and specifications
- Product backlog items
- User stories with acceptance criteria

### Governance Framework
The `governance.md` outlines:
- Roles and responsibilities
- Security policies
- Development standards
- Monitoring procedures

### Implementation
Implementation details are split across:
- `implementation_plan.md`: Detailed phase breakdown
- `timeline.md`: Project schedule and milestones
- `publish.md`: Deployment procedures

## Maintenance

Please follow these guidelines when updating documentation:

1. Use Markdown formatting
2. Keep diagrams up to date (Mermaid format preferred)
3. Update related documents when making changes
4. Keep the directory structure organized