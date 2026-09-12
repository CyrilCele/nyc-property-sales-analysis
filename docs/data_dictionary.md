# Data Dictionary

This document describes the variables in the cleaned and integrated analytical dataset produced by `02_data_cleaning_integration.ipynb`.

The final dataset contains **163,311 rows and 29 columns**. Source fields originate from the New York City Department of Finance annualized property sales workbooks, while derived fields were created during data cleaning and integration.

## Source Fields

| Column                           | Description                                                                                                     |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `borough`                        | NYC borough in which the property is located. Borough codes from the source files were mapped to borough names. |
| `neighborhood`                   | Neighborhood assigned to the property in the NYC Department of Finance data.                                    |
| `building_class_category`        | Descriptive building-class category associated with the transaction.                                            |
| `tax_class_at_present`           | Property tax class at the time represented by the source record.                                                |
| `block`                          | Tax block identifier. Treated as an identifier rather than a numeric measurement.                               |
| `lot`                            | Tax lot identifier within the block. Treated as an identifier rather than a numeric measurement.                |
| `building_class_at_present`      | Building-class code describing the property's present classification.                                           |
| `address`                        | Street address recorded for the property.                                                                       |
| `apartment_number`               | Apartment or unit identifier where available.                                                                   |
| `zip_code`                       | Property ZIP code. Treated as an identifier rather than a numeric measurement.                                  |
| `residential_units`              | Number of residential units recorded for the property.                                                          |
| `commercial_units`               | Number of commercial units recorded for the property.                                                           |
| `total_units`                    | Total number of units recorded for the property.                                                                |
| `land_square_feet`               | Recorded land area in square feet.                                                                              |
| `gross_square_feet`              | Recorded gross building area in square feet.                                                                    |
| `year_built`                     | Recorded year the property was built. One clearly invalid value of `190` was set to missing during cleaning.    |
| `tax_class_at_time_of_sale`      | Property tax class recorded at the time of sale.                                                                |
| `building_class_at_time_of_sale` | Building-class code recorded at the time of sale.                                                               |
| `sale_price`                     | Recorded transaction price in US dollars.                                                                       |
| `sale_date`                      | Recorded date of the property transaction.                                                                      |

The original `EASE-MENT` field was removed because it was entirely missing across all ten source files.

## Provenance Fields

| Column           | Description                                                                  |
| ---------------- | ---------------------------------------------------------------------------- |
| `source_year`    | Year of the source workbook from which the record originated: 2024 or 2025.  |
| `source_borough` | Borough represented by the source workbook from which the record originated. |

These fields preserve source-file provenance after the ten borough-level datasets are combined.

## Derived Analytical Fields

| Column                       | Description                                                                                                                                                                                             |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `building_category_code`     | Two-digit category code extracted from `building_class_category`.                                                                                                                                       |
| `is_residential`             | Boolean indicator identifying records belonging to the residential building categories selected for this project.                                                                                       |
| `has_positive_sale_price`    | Boolean indicator showing whether `sale_price` is greater than zero.                                                                                                                                    |
| `is_residential_market_sale` | Boolean indicator used in the notebooks for residential records with a positive recorded sale price. The name does **not** imply that the transaction has been verified as an arm's-length market sale. |
| `has_valid_gross_sqft`       | Boolean indicator showing whether usable positive gross building-area information is available.                                                                                                         |
| `is_size_analysis_eligible`  | Boolean indicator identifying residential positive-price records with usable gross square footage for size-based analysis.                                                                              |
| `price_per_sqft`             | Recorded sale price divided by gross square feet for size-eligible records.                                                                                                                             |

## Residential Building Categories

The residential analytical definition includes the following building-category codes:

| Code | Category                       |
| ---- | ------------------------------ |
| `01` | One Family Dwellings           |
| `02` | Two Family Dwellings           |
| `03` | Three Family Dwellings         |
| `04` | Tax Class 1 Condos             |
| `07` | Rentals - Walkup Apartments    |
| `08` | Rentals - Elevator Apartments  |
| `09` | Coops - Walkup Apartments      |
| `10` | Coops - Elevator Apartments    |
| `12` | Condos - Walkup Apartments     |
| `13` | Condos - Elevator Apartments   |
| `14` | Rentals - 4-10 Unit            |
| `15` | Condos - 2-10 Unit Residential |
| `17` | Condo Coops                    |

Commercial, institutional, vacant-land, explicitly mixed-use, and other non-residential categories are excluded from the project's residential analytical population.

## Analytical Populations

The notebooks use different subsets depending on the research question:

| Population                       | Records | Purpose                                                                                                     |
| -------------------------------- | ------: | ----------------------------------------------------------------------------------------------------------- |
| Integrated dataset               | 163,311 | Complete cleaned dataset across all ten source workbooks                                                    |
| Residential records              | 149,087 | Records belonging to the selected residential categories                                                    |
| Residential positive-price sales |  97,849 | Sale-price, transaction-volume, year, borough, and property-category analysis                               |
| Initial size-eligible sales      |  45,111 | Residential positive-price records with usable gross square footage                                         |
| Final size-analysis records      |  45,110 | Size-eligible records after excluding one isolated 1-square-foot observation                                |
| Market-oriented size subset      |  42,730 | Size and price-per-square-foot analysis after additionally excluding recorded sale prices of $1,000 or less |

The final size-based subset is an analytical population designed to reduce the influence of clearly nominal transaction values. It should **not** be interpreted as a set of independently verified arm's-length market transactions.

## Important Data Limitations

Gross square footage is largely unavailable for condo and co-op transactions. Building-area coverage is especially limited in Manhattan, so size and price-per-square-foot analyses are not representative of the complete residential market.

Recorded sale prices can also include nominal, related-party, package, or otherwise non-standard transactions. Large values were not removed simply because they were extreme unless there was specific evidence of a data-quality problem.
