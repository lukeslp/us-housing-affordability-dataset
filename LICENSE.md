# License Information

## Source Data

**U.S. Census Bureau American Community Survey (ACS) 2022**

All Census data is in the **public domain** as a U.S. Government work.

Tables used:
- B25070: Gross Rent as Percentage of Household Income
- B25064: Median Gross Rent
- B19013: Median Household Income
- B25003: Tenure (Owner/Renter Occupied)

## Derived Calculations

The following fields are computed from source data:
- `rent_to_income_ratio`: Annual rent / median household income
- `affordability_category`: Classification based on 30% and 50% thresholds
- `hours_at_min_wage_for_rent`: Monthly rent / $7.25 federal minimum wage
- `weeks_at_min_wage_for_rent`: Hours converted to full-time weeks

## Combined Dataset

This compiled dataset is released under **CC-BY-4.0**.

When using this dataset, please cite:

```
Steuber, L. (2026). US Housing Affordability Crisis by County [Dataset].
Kaggle. https://www.kaggle.com/datasets/lucassteuber/us-housing-affordability-crisis
```
