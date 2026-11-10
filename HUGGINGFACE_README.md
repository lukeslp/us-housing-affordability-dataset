---
license: cc-by-4.0
task_categories:
  - feature-extraction
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
  - n<1K
---

# US Housing Affordability Crisis by County

3,222 US counties: rent burden, income ratios, minimum wage hours needed

3,222 US counties with rent burden analysis, affordability calculations, and minimum wage comparisons derived from Census ACS 2022 data.

## Dataset Structure

See `demo_notebook.ipynb` for data exploration examples.

## Usage

```python
from datasets import load_dataset

# Load the dataset
dataset = load_dataset("lukeslp/us-housing-affordability-crisis")

# Or load from local files
import json
with open('data.json') as f:
    data = json.load(f)
```

## Citation

```bibtex
@dataset{us_housing_affordability_crisis_2026,
  title = {US Housing Affordability Crisis by County},
  author = {Steuber, Luke},
  year = {2026},
  url = {https://huggingface.co/datasets/lukeslp/us-housing-affordability-crisis}
}
```


## Missing values

The Census Bureau publishes no median gross rent for ten sparsely populated counties, and no median household income for one of them (Loving County, Texas). Those cells are empty, and so are the fields computed from them: `annual_rent`, `rent_to_income_ratio`, `affordability_category`, `hours_at_min_wage_for_rent` and `weeks_at_min_wage_for_rent`. Before November 10, 2026 they held the Census placeholder `-666666666` and values computed from it.

## Distribution

- **GitHub**: [lukeslp/us-housing-affordability-crisis](https://github.com/lukeslp/us-housing-affordability-crisis)
- **Kaggle**: [lucassteuber/us-housing-affordability-crisis](https://www.kaggle.com/datasets/lucassteuber/us-housing-affordability-crisis)

## Author

**Luke Steuber**
- Website: [lukesteuber.com](https://lukesteuber.com)
- Bluesky: [@lukesteuber.com](https://bsky.app/profile/lukesteuber.com)
- Email: luke@lukesteuber.com

## License

CC-BY-4.0
