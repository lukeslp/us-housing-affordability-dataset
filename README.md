---
license: cc-by-4.0
task_categories:
  - tabular-classification
  - tabular-regression
language:
  - en
tags:
  - housing
  - affordability
  - rent-burden
  - census
  - county-level
  - economics
  - inequality
  - minimum-wage
  - us-data
pretty_name: US Housing Affordability Crisis by County
size_categories:
  - 1K<n<10K
dataset_info:
  features:
    - name: fips
      dtype: string
    - name: county_name
      dtype: string
    - name: total_renters
      dtype: int64
    - name: pct_rent_burdened_30plus
      dtype: float64
    - name: pct_rent_burdened_50plus
      dtype: float64
    - name: median_gross_rent
      dtype: int64
    - name: median_household_income
      dtype: int64
    - name: rent_to_income_ratio
      dtype: float64
    - name: affordability_category
      dtype: string
    - name: hours_at_min_wage_for_rent
      dtype: float64
  splits:
    - name: train
      num_examples: 3222
---

# US Housing Affordability Crisis by County

3,222 US counties with rent burden analysis, affordability metrics, and minimum wage comparisons.

## What's Inside

- 3,222 county records (all US counties with renter data)
- Rent burden percentages (30% and 50% thresholds)
- Computed affordability metrics
- Minimum wage hours needed for rent
- Census ACS 2022 source data

## Why This Dataset Exists

Raw Census data requires pulling from multiple tables and computing derived metrics. This dataset integrates 4 ACS tables and adds calculated fields:

| Computed Field | Calculation |
|----------------|-------------|
| rent_to_income_ratio | Annual rent / median income |
| affordability_category | Affordable (<30%), Burdened (30-50%), Severe (>50%) |
| hours_at_min_wage_for_rent | Monthly rent / $7.25 federal minimum |
| weeks_at_min_wage_for_rent | Full-time weeks needed |

## Data Sources

| Metric | Census Table |
|--------|--------------|
| Rent burden | B25070 |
| Median rent | B25064 |
| Median income | B19013 |
| Housing tenure | B25003 |

## Usage

```python
import pandas as pd

df = pd.read_csv('housing_crisis_merged.csv')
print(f"Total counties: {len(df):,}")

# Find most burdened counties
severe = df[df['affordability_category'] == 'Severe Burden']
print(f"Severely burdened: {len(severe):,}")

# Counties where rent requires 100+ hours at minimum wage
extreme = df[df['hours_at_min_wage_for_rent'] >= 100]
print(f"100+ hours at min wage: {len(extreme):,}")
```

## License

CC-BY-4.0 (Census data is public domain; derived calculations by Luke Steuber)

## Distribution

- **Kaggle**: [lucassteuber/us-housing-affordability-crisis](https://www.kaggle.com/datasets/lucassteuber/us-housing-affordability-crisis)
- **HuggingFace**: [lukeslp/us-housing-affordability-crisis](https://huggingface.co/datasets/lukeslp/us-housing-affordability-crisis)
- **GitHub Gist**: [Demo Notebook](https://gist.github.com/lukeslp/02fc9010feb6e8657b6439303037e5f0)

## Author

Luke Steuber | luke@lukesteuber.com | @lukesteuber.com (Bluesky)

## Structured Data (JSON-LD)

```json
{
  "@context": "https://schema.org",
  "@type": "Dataset",
  "name": "US Housing Affordability Crisis by County",
  "description": "3,222 US counties with rent burden analysis, affordability metrics, and minimum wage comparisons. Derived from Census ACS 2022 data.",
  "url": "https://www.kaggle.com/datasets/lucassteuber/us-housing-affordability-crisis",
  "sameAs": "https://huggingface.co/datasets/lukeslp/us-housing-affordability-crisis",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Person",
    "name": "Luke Steuber",
    "url": "https://lukesteuber.com"
  },
  "keywords": ["housing", "affordability", "rent burden", "census", "economics", "inequality", "minimum wage"],
  "temporalCoverage": "2022",
  "spatialCoverage": {
    "@type": "Place",
    "name": "United States"
  },
  "distribution": [
    {
      "@type": "DataDownload",
      "encodingFormat": "text/csv",
      "contentUrl": "https://www.kaggle.com/datasets/lucassteuber/us-housing-affordability-crisis"
    }
  ]
}
```
