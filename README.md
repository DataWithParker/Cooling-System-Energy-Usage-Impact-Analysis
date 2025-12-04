# Cooling-System-Energy-Usage-Impact-Analysis

*Course: IST 687 – Introduction to Data Science - Syracuse University*

## Project Objective
This project investigates how residential cooling systems impact electricity consumption during peak summer conditions, focusing on July, historically the highest energy-use month for energy company (eSC), a regional electricity provider serving South Carolina and parts of North Carolina.

(eSC) anticipates increased grid strain due to hotter summers brought on by climate change. Rather than building new power plants, the company aims to understand:

  - The key drivers of residential energy usage
  - How cooling systems contribute to peak loads
  - How to encourage customers to adopt energy-saving behaviors
  - How to predict future energy demand under hotter conditions

**Guiding Question:**
“How do residential cooling systems impact energy usage during peak summer conditions, and what strategies can be implemented to optimize cooling efficiency and reduce overall electricity demand?”

## Data Sources 
  **1. Static House Data (Parquet)**: Contains building IDs, square footage, HVAC type, and other attributes that do not change over time. (~5,000 homes included.)
  
  **2. Energy Usage Data (Parquet file per building)**: 
  - Hour-by-hour consumption
  - Includes detailed end-use load breakdown(e.g., cooling, lighting, plug loads, refrigerator, dryer, etc.), about 5,000 files total (one per building)
  
  **3. Meta Data (CSV)**: Human-readable descriptions of all variables across datasets.
  
  **4. Weather Data ((1) CSV per county)**: Hourly temperature and humidity linked to homes using county codes (~50 county files in total)

  ### Data Integration Process
  - Linked energy usage with weather timeseries using timestamps and county codes.
  - Merged combined dataset with static home characteristics via building IDs.

## Methodology and Analysis

**Data Preparation**
  - Loaded 5,000+ parquet energy files and merged with static house metadata.
  - Pulled county-level weather files and synchronized hourly timestamps.
  - Cleaned missing fields, handled system anomalies, validated timestamps.
  - Produced a unified hourly dataset for July energy usage across all homes.

**Exploratory Data Analysis (EDA)**

  Key activities included:
  - Calculating total city-level energy consumption
  - Distribution analyses of cooling systems (Central AC, Heat Pumps, Room AC)
  - Identifying cooling inefficiency via SEER/EER ratings
  - End-use breakdown (cooling, plug loads, lighting, appliances)
  - Temperature vs. consumption correlation
  - Regression visualization (scatterplots, trendlines)

### **Model and Results** 

**Selected Model Type:** Linear Regression 

*Performance*
- R² = 0.8704
- P-value < 2.2e-16
- Features used: Cooling load, plug loads, lighting load, temperature, hour-of-day

*Model Interpretation*
- Cooling is the strongest predictor of total consumption.
- Plug loads and lighting contribute but are less impactful.
- Temperature and time of day amplify cooling demand.

**Climate Scenario Analysis**

Forecasting Future Peak Demand: Created a modified weather dataset with July temperatures increased by +5°F to evaluate hotter-summer impacts.

Model-driven predictions evaluated:
- Peak hourly demand across cities
- Peak demand by HVAC type
- Peak demand by efficiency groups (e.g., SEER ≤ 13 vs. SEER ≥ 15)

**Energy Demand Reduction Strategy**
- **Primary Recommendation:** Upgrade inefficient cooling systems, especially Central AC SEER 13 and below (35% of homes).
- **Modeling Approach:** Simulated shifting SEER 13 systems to SEER 15 or to Heat Pumps.Predicted peak reduction, where a significant drop in cooling load and overall consumption was observed.

## Key Insights

Cooling is the dominant driver of summer electricity consumption
- Cooling accounts for ~43% of total July energy use—the largest single category.
- Cities with the highest cooling load had the highest total energy consumption.

Cooling inefficiency is widespread
- 58% of systems are inefficient by modern HVAC standards
- 35% of homes use Central AC with SEER 13, a major opportunity for upgrading
- Heat pumps represent 22% of homes and are typically more efficient

Temperature strongly amplifies consumption
- A clear positive correlation exists between: Outdoor temperature, Cooling load, Total electricity usage

Modeling indicates significant grid strain under +5°F conditions
- Higher hourly peaks
- More pronounced load spikes in late afternoon
- Disproportionate impact on homes with inefficient systems

Upgrading cooling equipment offers the largest reduction potential
- Upgrading SEER 13 → SEER 15 yields substantial savings
- Even greater reductions with heat pump adoption

## How to Run the Code
Prerequisites
- R 4.0+
- Required libraries: readr, dplyr, purrr, httr, lubridate, stringr, tidyverse, data.table, ggplot2, tidyr, and knitr
