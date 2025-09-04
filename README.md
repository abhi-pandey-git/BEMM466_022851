# Monte Carlo Simulation for Construction SME Risk Analysis

## Overview
This repository contains a Python script for running a Monte Carlo Simulation (MCS) to model cost and schedule risks in UK construction projects for small and medium-sized enterprises (SMEs). The simulation uses publicly available secondary data from sources like the Office for National Statistics (ONS) and National Audit Office (NAO) to derive risk parameters. It generates probabilistic forecasts, visualizations, and scenario analyses to help SMEs quantify uncertainties and improve decision-making.

The script is part of a MSc Business Analytics dissertation project (BEMM466) at the University of Exeter, focusing on applying business analytics to project risk management.

## Purpose
- Simulate project durations and costs under uncertainty using triangular, lognormal, and normal distributions.
- Incorporate correlated risks between duration and cost drivers.
- Produce outputs like probability distributions, sensitivity analyses, and scenario comparisons (e.g., high inflation, high labour shortage).
- Demonstrate MCS as a tool for transparent forecasting compared to deterministic methods.

This addresses research questions on primary risks, MCS implementation with public data, forecast transparency, and tool challenges/benefits (Python-focused, with literature-based Excel comparisons).

## Requirements
- Python 3.12+ (tested on 3.12.3)
- Libraries: Install via `pip install numpy pandas matplotlib scipy seaborn`
  - numpy: For numerical operations and random sampling.
  - pandas: For data loading and manipulation.
  - matplotlib & seaborn: For visualizations.
  - scipy: For statistical distributions (triang, norm, lognorm, pearsonr).
- No additional installations needed; script uses built-in REPL environment.

Note: No internet access required; all data is local.

## Data Files
The script loads volatility proxies from the following public datasets (download from ONS/NAO websites and place in the same directory):
- `series-310725.csv`: ONS UK Job Vacancies (Construction) for labour risk.
- `bulletindataset9.xlsx`: ONS Construction Output Price Indices (OPI) for cost volatility.
- `Construction Industry Structure 2024.xlsx`: ONS industry structure for weights.
- `Government_Major_Projects_Portofolio_AR_Data_March_2024.xlsx`: NAO GMPP for variance benchmarks.
- `bulletindataset7.xlsx`: ONS New Orders for changes.
- `output-in-the-construction-industry-time-series-v26.xlsx`: ONS Output Time Series for changes.
- `earn03jul2025.xls`: ONS Average Earnings for growth.
- `Construction_building_materials_-_tables_February_2025.xlsx`: ONS Building Materials for changes.

These are aggregated public data; no personal/sensitive info. Ethical note: Used for low-risk secondary analysis per BPS/UEBS guidelines.

## How to Run
1. Ensure all data files are in the working directory.
2. Run the script: `python mcs_construction_risk.py`
   - It loads data, aggregates risks, runs simulations (100,000 iterations), generates summaries, and saves outputs.
3. Outputs:
   - Console: Aggregated risks, summaries, percentiles, correlations.
   - CSV: `mcs_results.csv` (full simulation data).
   - PNGs: Visuals like histograms (`distributions_hist.png`), CDFs (`cdfs.png`), scatter (`scatter_duration_cost.png`), pie (`pie_cost_breakdown.png`), boxplots (`boxplot_results.png`), violins (`violin_distributions.png`), heatmap (`correlation_heatmap.png`), overrun curve (`cumulative_overrun_line.png`), tornado (`sensitivity_tornado.png`), scenario KDE (`scenario_costs_kde.png`).

## Assumptions and Limitations
- Distributions: Triangular for durations (bounded optimism/pessimism), lognormal for materials (right-skew), normal for labour noise.
- Correlations: Target ρ=0.60 (literature-based), attenuated empirically to r≈0.36 due to noise.
- Data: Aggregated proxies may mask SME-specifics; no real-time updates.
- Model: Additive tasks (no critical path dependencies); hardcoded params (e.g., sigma_dur=0.20).
- Ethical: Low-risk public data; no GenAI in core analysis.

For details, see dissertation report. Reproducible with seed=42.

## License
MIT License. Free to use/modify with attribution.

## Author
Abhishek Pandey (MSc Business Analytics, University of Exeter)  
Contact: [your email or GitHub profile]  
Supervisor: Dr Thomas Birtch  

Last updated: September 4, 2025
