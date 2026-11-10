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
    - name: total_housing_units
      dtype: int64
    - name: owner_occupied
      dtype: int64
    - name: renter_occupied
      dtype: int64
    - name: pct_renter
      dtype: float64
    - name: annual_rent
      dtype: int64
    - name: rent_to_income_ratio
      dtype: float64
    - name: affordability_category
      dtype: string
    - name: hours_at_min_wage_for_rent
      dtype: float64
    - name: weeks_at_min_wage_for_rent
      dtype: float64
  splits:
    - name: train
      num_examples: 3222
---

# US Housing Affordability Crisis by County

3,222 US counties with rent burden analysis, affordability metrics, and minimum wage comparisons.

## What's Inside

- 3,222 records: every US county plus Puerto Rico's 78 municipios
- Rent burden percentages (30% and 50% thresholds)
- Computed affordability metrics
- Minimum wage hours needed for rent
- Census ACS 2022 source data

## Why This Dataset Exists

Raw Census data requires pulling from multiple tables and computing derived metrics. This dataset integrates 4 ACS tables and adds calculated fields:

| Computed Field | Calculation |
|----------------|-------------|
| rent_to_income_ratio | Annual rent / median income, as a percentage |
| affordability_category | Affordable (ratio under 30): 3,192 records. Moderately Burdened (30 and up): 29. Extremely Burdened: 1, and that one is a data error (see Known Issues) |
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

# Drop the 10 counties where the Census suppressed the rent (see Known Issues)
df = df[df['median_gross_rent'] > 0]

# Find the burdened counties
burdened = df[df['affordability_category'] == 'Moderately Burdened']
print(f"Rent takes 30% or more of income: {len(burdened):,}")

# Counties where rent requires 100+ hours at minimum wage
extreme = df[df['hours_at_min_wage_for_rent'] >= 100]
print(f"100+ hours at min wage: {len(extreme):,}")
```

## Known Issues

The Census Bureau writes `-666666666` when it can't publish an estimate. Ten sparsely populated counties have that code in `median_gross_rent`, and Loving County, Texas has it in `median_household_income` too. The code was not filtered out before the derived fields were computed, so `annual_rent`, `rent_to_income_ratio`, `affordability_category` and both minimum-wage fields are meaningless for those ten rows. Drop rows where `median_gross_rent` is negative.

The ten: Alpine County, California; Owsley County, Kentucky; Cameron Parish, Louisiana; Borden, Glasscock, Kenedy, King, Loving and Terrell counties, Texas; Daggett County, Utah.

## License

CC-BY-4.0. The Census data is public domain; the derived fields are mine.

## Distribution

- **Kaggle**: [lucassteuber/us-housing-affordability-crisis](https://www.kaggle.com/datasets/lucassteuber/us-housing-affordability-crisis)
- **HuggingFace**: [lukeslp/us-housing-affordability-crisis](https://huggingface.co/datasets/lukeslp/us-housing-affordability-crisis)
- **GitHub Gist**: [Demo Notebook](https://gist.github.com/lukeslp/02fc9010feb6e8657b6439303037e5f0)

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
