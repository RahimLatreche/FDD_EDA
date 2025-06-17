# Comerica RTU Data Analysis

## Project Overview
This project analyzes rooftop unit (RTU) sensor data from a commercial building to understand cooling demand patterns, sensor relationships, and potential system faults. The analysis is performed in a Jupyter notebook and covers data cleaning, merging, exploratory analysis, time series modeling, and anomaly detection.

## Progress So Far

- **Data Loading & Merging:**
  - Loaded point and metadata CSVs, merged them on unique references, and saved a combined dataset for further analysis.

- **Data Cleaning & Preparation:**
  - Cleaned up columns, standardized units, and converted timestamps to a consistent timezone.
  - Applied robust outlier filtering (MAD-based) to temperature signals.
  - Built an hourly, wide-format table for all numeric signals (°F, %, etc.).

- **Exploratory Analysis:**
  - Performed seasonal decomposition on Cooling Demand to separate trend, seasonality, and residuals.
  - Explored the relationship between Cooling Demand and Outdoor Air Temperature, including lag analysis and linear modeling.
  - Quantified the delay between outdoor temperature changes and cooling demand (found a ~4-hour lag).
  - Calculated the sensitivity: each +1°F in outdoor air (4 hours earlier) increases cooling demand by ~0.5 kW.
  - Found that outdoor air alone explains about 24% of the hour-to-hour variance in cooling demand.

- **Sensor Correlation:**
  - Cross-correlated all numeric/boolean sensors against Cooling Demand.
  - Identified the most influential sensors and their lags (e.g., Discharge Temperature, Occupied Setpoints, Zone Temperature).
  - Summarized findings in clear tables and visualizations.

- **Anomaly Detection & Fault Flagging:**
  - Used model residuals to flag hours with unusually high or low cooling demand.
  - Exported flagged anomalies with context (outdoor temp, HVAC mode, etc.) for further review.
  - Analyzed the distribution of anomalies by HVAC mode and time of day.

## Key Findings

- **Cooling Demand is highly seasonal**, peaking in summer and nearly zero in winter.
- **Outdoor Air Temperature is the main driver** of cooling demand, with a 4-hour lag.
- **Discharge Temperature is a strong, immediate indicator** of cooling effort (inverse correlation at lag 0).
- **Most anomalies are positive residuals** (system over-cooling), often when the system is "Off" or mode is unknown—suggesting possible valve leakage or control issues.
- **Anomaly rate is reasonable** for exploratory work; further tuning can reduce false positives.

## Next Steps

- Analyze the Spark AHU Economizing & Cooling Simultaneously

---

For details, see the `data_analysis.ipynb` notebook in this repository.
