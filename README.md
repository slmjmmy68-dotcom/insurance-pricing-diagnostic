Insurance Pricing Model Adherence Diagnostic

Executive Summary

    This project evaluates structural pricing dispersion within a personal auto insurance portfolio using model-to-selected premium ratios.

    The analysis identifies lifecycle and geographic interaction effects driving systematic deviation from technical indication, revealing evidence of calibration drift rather than isolated pricing variance.

Business Problem

    Insurance carriers rely on pricing models to align premiums with risk.
    When selected premiums diverge from modeled indication in a structured way, margin leakage and cross-subsidization can occur across customer segments.

    This diagnostic addresses:
    - Is pricing deviation random or structural?
    - Which segments exhibit systematic underpricing or overpricing?
    - Do interaction effects (e.g., Geography × Age) materially amplify dispersion?
    - Where should recalibration and monitoring focus?

Key Findings

    - Portfolio pricing trends 7% below modeled indication
    - 53% of policies are priced below technical indication
    - Geo × Age interaction effects exceed standalone driver strength
    - Segment dispersion exceeds 35%, indicating structural calibration drift
    - Older short-tenure segments show systematic underpricing
    - Younger long-tenure segments appear to subsidize deviation

    Observed pricing variance clusters structurally across lifecycle and geographic dimensions.

Analytical Approach

    I. Data Engineering
        - Cleaned and transformed policy-level data using Python (Pandas)
        - Engineered lifecycle segmentation:
            > Age bands
            > Tenure bands
        - Derived model adherence metrics:
            > Model pricing ratio
            > Renewal change
            > Indicated-to-current ratio
        - Created stable pricing flags to isolate valid comparisons
        
    II. Dimensional Modeling

        Built a star schema and pushed to SQLite:

            Fact Table
                fact_premium
                    Existing Policy-level pricing metrics
                    Derived model adherence metrics
                    Model adherence flags
                    Defined Segment attributes

            Dimension Tables
                dim_territory
                dim_rating_definition

        This supports scalable aggregation and reporting logic.

    III. Interaction Analysis

        Quantified dispersion strength across:
            Age
            Tenure
            Geography
            Age × Tenure
            Geo × Age

        Dispersion driver strength measured using max-min ratio spread across segments.

        Interaction effects materially exceeded standalone drivers.

    IV. Executive Reporting Layer

        Developed an executive-ready Power BI diagnostic including:
            Portfolio-level KPI summary
            Lifecycle dispersion heatmaps
            Geographic deviation analysis
            Interaction strength ranking
            Strategic recommendations & monitoring framework

        The reporting layer translates analytical findings into actionable business insights.

Strategic Extensions

    Future enhancements could include:
        Loss ratio integration by segment (Geo × Age × Tenure)
        Risk alignment validation against claim frequency/severity
        Competitor pricing benchmarks
        Policy lapse behavior analysis
        Model adherence monitoring dashboards
        Alert-based calibration triggers

Technical Stack
    Python (Pandas) – ETL & feature engineering
    SQLite (Star schema) – Reporting layer (Aggregation & interaction analysis)
    Power BI – Executive Visualization dashboard
    Git – Version control

Repository Structure
    insurance-pricing-diagnostic/
    │
    ├── data/
    │   ├── raw/
    │   ├── processed_to_load/
    │
    ├── notebooks/
    │
    ├── sql/
    │
    ├── powerbi/
    │
    ├── outputs/
    │   ├── screenshots/
    │
    ├── README.md
    ├── requirements.txt
    └── .gitignore