
# Monte Carlo Simulation for Construction SME Risk (Cost & Schedule)

[![Python 3.8+](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/downloads/) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains a Python script that performs Monte Carlo simulations to assess cost overruns and schedule delays in small-to-medium enterprise (SME) construction projects. The model aggregates volatility proxies from various UK construction industry datasets to parameterize risks, incorporating labor shortages, material price fluctuations, and correlated uncertainties. It generates probabilistic forecasts, sensitivity analyses, and scenario comparisons to support risk management decisions.

The simulation is designed for SME-scale projects (e.g., baseline ~12 months, ~£460k), but parameters can be customized for broader applications. Outputs include distributions, correlations, tornado charts, and CSVs for further analysis.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Data Sources](#data-sources)
- [Configuration Options](#configuration-options)
- [Outputs](#outputs)
- [Examples](#examples)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgments](#acknowledgments)

## Overview
Construction projects, especially for SMEs, often face uncertainties leading to overruns. This script uses Monte Carlo methods to:
- Derive risk parameters (e.g., labor shortage CV, cost volatility) from real datasets.
- Model task durations (triangular distributions) and costs (lognormal multipliers with correlations).
- Simulate coupled duration-cost scenarios, including overheads and time-based labor scaling.
- Produce summaries, visualizations, and sensitivity insights for contingency planning.
- Explore scenarios like high inflation or labor shortages.

The approach emphasizes data-driven inputs from sources like ONS, BIS, and GMPP reports, making it grounded in UK construction trends.

## Features
- **Data Aggregation:** Parses Excel/CSV files to compute aggregated risks (e.g., vacancy CV for labor, OPI std for costs).
- **Probabilistic Modeling:** Triangular durations, lognormal multipliers, correlated shocks (Pearson rho), and shared factors.
- **Simulation Engine:** Runs 100,000+ iterations for durations, materials, labor, and overheads.
- **Analyses:** Percentiles, overruns, correlations, tornado sensitivity, and scenario comparisons.
- **Visualizations:** Histograms, CDFs, scatters, pie charts, box/violin plots, heatmaps, and KDEs (saved as PNGs).
- **Outputs:** CSVs (results, summaries), console stats, and scenario forecasts.

## Requirements
- Python 3.8+
- Libraries (install via `pip install -r requirements.txt`):
  - numpy
  - pandas
  - matplotlib
  - seaborn
  - scipy
  - openpyxl (for Excel parsing)

The code handles file parsing robustly but assumes standard formats.

## Installation
1. Clone the repository:
   ```
   git clone https://github.com/yourusername/monte-carlo-construction-sme-risk.git
   cd monte-carlo-construction-sme-risk
   ```
2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
   (Create `requirements.txt` with the listed libraries if not included.)

3. Place data files in the root directory (see [Data Sources](#data-sources)).

## Usage
1. Ensure all required data files are in the project root.
2. Run the script:
   ```
   python monte_carlo_sme_risk.py
   ```
3. The script will:
   - Load and aggregate risks from files.
   - Compute deterministic baseline.
   - Run simulations.
   - Print summaries (e.g., P50/P95, overruns, correlations).
   - Save CSVs and plots.
   - Execute scenario analyses (baseline, high inflation, high labor shortage).

Customize tasks, parameters, or scenarios by editing the script (e.g., `tasks` list, `rho=0.60`).

## Data Sources
The script processes the following files (place in root; some may be truncated in prompts but assume full datasets):
- `series-310725.csv`: UK job vacancies (construction) for labor risk.
- `bulletindataset9.xlsx`: Construction Output Price Indices (OPIs) for cost changes.
- `Construction Industry Structure 2024.xlsx`: Sector weights for structure CV.
- `Government_Major_Projects_Portofolio_AR_Data_March_2024.xlsx`: GMPP variances for project risks.
- `bulletindataset7.xlsx`: New orders changes for demand volatility.
- `output-in-the-construction-industry-time-series-v26.xlsx`: Output changes for industry fluctuations.
- `earn03jul2025.xls`: Earnings growth for labor cost risks.
- `Construction_building_materials_-_tables_February_2025.xlsx`: Material price changes.

Sources: ONS (Office for National Statistics), BIS (Department for Business, Innovation & Skills), and IPA (Infrastructure and Projects Authority). If files are missing, the script uses defaults or skips.

## Configuration Options
Edit variables in the script:
- `TRI_MIN/MODE/MAX`: Triangular duration ratios (default: 0.80/1.00/1.50 + risk).
- `sigma_dur/sigma_mat/lab_noise_cv`: Std devs for multipliers/noise.
- `rho`: Correlation between duration and cost shocks (default: 0.60).
- `lab_time_share`: Share of labor scaling with time (default: 0.60).
- `overhead_per_month`: Fixed overheads (£k/month, default: 5.0).
- `n_sim`: Simulations (default: 100,000).
- `tasks`: List of dicts with task names, base durations/materials/labors.

For scenarios, adjust multipliers in `run_scenario()` calls.

## Outputs
- **CSVs:** `mcs_results.csv` (full sim data: durations, costs, components).
- **Console Summary:** Aggregated risks, baselines, percentiles, overruns, correlations, scenario results.
- **Plots (PNG):** 
  - `distributions_hist.png`: Histograms of duration/cost.
  - `cdfs.png`: Cumulative distribution functions.
  - `scatter_duration_cost.png`: Scatter with correlation.
  - `pie_cost_breakdown.png`: Average component shares.
  - `hist_cost_changes.png`: Input cost % changes (placeholder).
  - `boxplot_results.png`: Box plots.
  - `violin_distributions.png`: Violin plots.
  - `correlation_heatmap.png`: Component correlations.
  - `cumulative_overrun_line.png`: Overrun risk curves.
  - `sensitivity_tornado.png`: Sensitivity to shocks.
  - `scenario_costs_kde.png`: KDEs for scenarios.

## Examples
- **Baseline Run:** Outputs P50 duration ~12-15 months, cost ~£500-600k (depending on risks).
- **High Inflation Scenario:** Increases cost volatility (multiplier=1.15), shifting distributions right.
- **Customization:** Add tasks or adjust `rho=0.8` for stronger coupling; re-run for updated plots.

## Contributing
Contributions are welcome! Fork the repo, make changes, and submit a pull request.
- Report issues: Open a GitHub issue with details.
- Enhancements: E.g., add more distributions (PERT), CPM integration, or optimization.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments
- Inspired by construction risk literature (e.g., Flyvbjerg on overruns).
- Data: ONS, BIS, IPA – thanks to UK public sources.
- Libraries: NumPy, Pandas, Matplotlib, Seaborn, SciPy for efficient simulations.

Contact: Abhishek Pandey (ap1204@exeter.ac.uk)
