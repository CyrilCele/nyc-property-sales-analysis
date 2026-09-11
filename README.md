# NYC Property Sales Analysis: 2024–2025

## Overview

This project analyzes residential property sales across New York City's five boroughs using annual property sales data published by the New York City Department of Finance.

The analysis covers 2024 and 2025 and combines ten borough-level source files into a single analytical dataset. The project focuses on professional data cleaning, multi-file integration, exploratory data analysis, and evidence-based interpretation of residential property market patterns.

## Research Question

**How do property size, location, and property characteristics relate to residential sale prices across New York City's five boroughs, and how did these patterns differ between 2024 and 2025?**

Supporting questions include:

* How do residential sale-price distributions differ across the five boroughs?
* What relationship exists between property size and sale price?
* Does the relationship between property size and sale price differ by borough?
* How does price per square foot vary across boroughs and neighborhoods?
* How do sale prices differ across residential property categories?
* How did observed residential property sales differ between 2024 and 2025?

## Data

The project uses annualized property sales data published by the **New York City Department of Finance**.

Ten source files are used:

| Year | Boroughs                                          |
| ---- | ------------------------------------------------- |
| 2024 | Manhattan, Bronx, Brooklyn, Queens, Staten Island |
| 2025 | Manhattan, Bronx, Brooklyn, Queens, Staten Island |

Each borough file is cleaned and validated independently before the datasets are combined for analysis.

Raw and processed data files are not committed to this repository. Instructions for obtaining and preparing the data will be documented as the project develops.

## Methodology

The project follows a structured exploratory data science workflow:

1. Inspect the structure and quality of each source file.
2. Standardize schemas, column names, and data types.
3. Identify and address missing, invalid, and duplicate observations.
4. Preserve borough and year provenance for every record.
5. Combine the cleaned borough datasets into a unified dataset.
6. Validate the integrity of the combined data.
7. Perform descriptive and group-level statistical analysis.
8. Examine sale-price distributions and property-size relationships.
9. Compare patterns across boroughs, neighborhoods, property categories, and years.
10. Communicate findings with appropriate visualizations and statistical summaries.

The analysis is observational. Relationships identified in the data are interpreted as associations rather than causal effects.

## Project Structure

```text
nyc-property-sales-analysis/
├── data/
│   ├── raw/
│   │   ├── 2024/
│   │   └── 2025/
│   └── processed/
├── docs/
├── notebooks/
├── reports/
│   └── figures/
├── src/
├── .gitignore
├── .python-version
├── pyproject.toml
└── README.md
```

The repository structure will expand only when additional files have a clear role in the project.

## Planned Notebooks

| Notebook                             | Purpose                                                                                             |
| ------------------------------------ | --------------------------------------------------------------------------------------------------- |
| `01_data_understanding.ipynb`        | Inspect source files, schemas, data types, missing values, duplicates, and initial quality issues   |
| `02_data_cleaning_integration.ipynb` | Clean individual files, standardize schemas, combine the datasets, and validate the integrated data |
| `03_exploratory_data_analysis.ipynb` | Analyze property prices, size, location, property characteristics, and year-over-year patterns      |

## Tools

The project is developed in Python using a `uv`-managed virtual environment.

Core tools will include:

* Python
* pandas
* NumPy
* Matplotlib
* Jupyter
* openpyxl

Additional dependencies will be introduced only when they are required by the analysis.

## Reproducibility

The project uses `uv` for Python environment and dependency management.

After cloning the repository:

```bash
uv sync
```

The raw data must then be downloaded from the official NYC Department of Finance source and placed in the appropriate directories under `data/raw/`.

Detailed data preparation instructions will be added after the source files have been downloaded and inspected.

## Data Source

New York City Department of Finance
Annualized Property Sales Data

https://www.nyc.gov/site/finance/property/property-annualized-sales-update.page

## Status

**In development.**

The current phase focuses on project setup and acquisition of the ten 2024–2025 borough-level source files.
