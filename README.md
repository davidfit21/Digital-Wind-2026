# Digital Wind

## A Constraint-Aware Predictive Digital Twin for Offshore Wind Integration

Digital Wind is a grid-informed predictive coordination framework
designed to quantify and reduce offshore wind curtailment within the
operational limits of the Irish transmission system.

The project combines:

-   Multi-horizon machine learning forecasting
-   Constraint-aware feature engineering
-   Closed-loop dispatch simulation
-   Scenario-based offshore expansion stress testing

The framework evaluates how anticipatory coordination --- without new
infrastructure --- can reduce renewable curtailment under realistic
system constraints.

------------------------------------------------------------------------

# Project Structure

    .
    │   01_digital_wind_exploratory_analysis.ipynb
    │   02_digital_wind_constraint_modeling.ipynb
    │   03_offshore_wind_simulation_analysis.ipynb
    │   04_digital_wind_forecasting.ipynb
    │
    │   csv_nodes.csv
    │   dd-hh-2025-v10-CORE.xlsx
    │   LDT_MET_MAST_10M.xlsx
    │   stage1_system_state_2025.csv
    │   stage2_curtailment_model_2025.csv
    │   stage3_offshore_simulation_results.csv
    │   system-data-qtr-hourly-2025-v11-CORE.xlsx
    │
    ├── models/
    │       curtailment_magnitude_bundle.pkl
    │       curtailment_risk_bundle.pkl
    │       full_balancing_bundle.pkl
    │       ic_flow_bundle.pkl
    │       ic_saturation_bundle.pkl
    │
    └── Offshore_Wind_Farms_Generation/
            All_Power_Data.csv
            All_Windspeed_Data.csv
            readme.txt

------------------------------------------------------------------------
# External Files Used:
- EirGrid (2025) System Data Qtr-Hourly 2025 (v11): https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fcms.eirgrid.ie%2Fsites%2Fdefault%2Ffiles%2Fpublications%2FSystem-Data-Qtr-Hourly-2025-v11.xlsx&wdOrigin=BROWSELINK

- EirGrid (2025) DD-HH 2025 (v10): https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fcms.eirgrid.ie%2Fsites%2Fdefault%2Ffiles%2Fpublications%2FDD_HH_2026.xlsx&wdOrigin=BROWSELINK

- A Data Set With 40 Years of Hourly Wind Speeds and Electricity Production: https://figshare.com/articles/dataset/Dataset_for_the_Paper_Analyzing_Europe_s_Biggest_Offshore_Wind_Farms_a_Data_set_With_40_Years_of_Hourly_Wind_Speeds_and_Electricity_Production_/19139648
------------------------------------------------------------------------
# Workflow Overview

## Stage 1 --- Exploratory System Analysis

**Notebook:** `01_digital_wind_exploratory_analysis.ipynb`

-   Quarter-hourly Irish system data ingestion
-   Demand, generation, SNSP, and curtailment profiling
-   Stress regime identification
-   Initial system-state feature construction

**Output:**\
`stage1_system_state_2025.csv`

------------------------------------------------------------------------

## Stage 2 --- Constraint Modelling

**Notebook:** `02_digital_wind_constraint_modeling.ipynb`

-   Curtailment decomposition
-   Transmission congestion indicators
-   Interconnector stress ratios
-   Derived regime indicators

**Output:**\
`stage2_curtailment_model_2025.csv`

------------------------------------------------------------------------

## Stage 3 --- Offshore Expansion Simulation

**Notebook:** `03_offshore_wind_simulation_analysis.ipynb`

-   Offshore scenarios: 0.5 GW, 1 GW, 5 GW
-   Capacity-factor-driven generation synthesis
-   Node-level integration assumptions
-   Curtailment stress testing

**Output:**\
`stage3_offshore_simulation_results.csv`

------------------------------------------------------------------------

## Stage 4 --- Predictive Digital Twin

**Notebook:** `04_digital_wind_forecasting.ipynb`

Implements the multi-model forecasting stack:

-   Offshore generation forecast (Gradient Boosting)
-   Curtailment event probability (Logistic Regression)
-   Conditional curtailment magnitude model
-   Interconnector flow forecast
-   Interconnector saturation classifier

Models are saved in `/models` as deployable bundles including
preprocessing metadata.

The stacked predictions feed into a closed-loop dispatch simulation
implementing:

-   Ramp-constrained export coordination
-   SNSP ceiling enforcement
-   Interconnector capacity limits
-   Mitigation impact quantification

------------------------------------------------------------------------

# Data Sources

-   EirGrid quarter-hourly system data (2025)
-   DD-HH balancing datasets
-   Offshore wind farm generation datasets
-   Meteorological wind speed data

All preprocessing steps are implemented within the notebooks.

------------------------------------------------------------------------

# Reproducing Results

1.  Install required Python packages (see Requirements section below).
2.  Run notebooks sequentially (01 → 04).
3.  Ensure raw datasets are located in the root directory.
4.  Execute forecasting and simulation cells in Notebook 04.

Mitigation outputs will reproduce the reported performance tables.

Model artifacts in `/models` correspond to the final trained
configuration used in the reported results.

------------------------------------------------------------------------

# Requirements

Python 3.10+ recommended.

Core libraries:

-   pandas
-   numpy
-   scikit-learn
-   matplotlib
-   joblib

Install via:

    pip install -r requirements.txt

------------------------------------------------------------------------

# Key Features

-   Chronological train/test splitting (no look-ahead bias)
-   Leakage-controlled feature construction
-   Dimensionless constraint indicators
-   Multi-horizon (4h / 24h) forecasting
-   Closed-loop dispatch simulation
-   Constraint-aware mitigation quantification

------------------------------------------------------------------------

# Research Contribution

Digital Wind demonstrates that predictive coordination alone - without
infrastructure expansion - can reduce offshore wind curtailment within
existing Irish grid limits.

The framework is modular and extensible toward:

-   Battery coordination
-   Solar integration
-   Reactive power and voltage-aware modelling
-   Regional offshore expansion

------------------------------------------------------------------------

# Disclaimer

This repository is a research implementation and proof-of-concept
digital twin. It does not replace transmission system operator dispatch
tools or market clearing systems.
