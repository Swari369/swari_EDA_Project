# King County House Sales — Exploratory Data Analysis

## Project Overview

This project performs a comprehensive Exploratory Data Analysis (EDA) on the King County House Sales dataset. The goal is to uncover key patterns and insights that drive residential property prices in King County, Washington — with a focus on helping property stakeholders make data-driven decisions around **location**, **renovation**, and **timing** of home sales.

---

## Dataset

- **Source:** King County House Sales dataset (`data/eda.csv`)
- **Records:** 21,597 properties
- **Features:** 21 columns covering physical attributes, location, condition, and sale information

### Key Columns

| Column | Description |
|---|---|
| `price` | Sale price of the property |
| `bedrooms` | Number of bedrooms |
| `bathrooms` | Number of bathrooms |
| `sqft_living` | Interior square footage |
| `sqft_lot` | Lot area in square feet |
| `floors` | Number of floors |
| `waterfront` | Whether the property has a waterfront view |
| `view` | Quality of the view (0–4) |
| `condition` | Overall condition rating (1–5) |
| `grade` | Construction and design quality (1–13) |
| `yr_built` | Year the property was built |
| `yr_renovated` | Year of last renovation (0 if never renovated) |
| `zipcode` | ZIP code of the property |
| `lat` / `long` | Geographic coordinates |
| `sqft_living15` | Average living area of the 15 nearest neighbours |
| `date` | Date of sale |

---

## Project Structure

```
.
├── data/
│   └── eda.csv                  # King County dataset
├── Final_Project.ipynb          # Main EDA notebook
└── README.md                    # Project documentation
```

---

## Libraries Used

```python
numpy
pandas
matplotlib
seaborn
scipy
missingno
```

---

## Methodology

### 1. Data Loading & Initial Inspection
- Loaded the dataset using `pandas` and examined its shape, dtypes, and first few rows.
- Confirmed **no duplicate records** in the dataset (21,597 unique entries).
- Converted the `date` column from string to `datetime` format for time-based analysis.

### 2. Missing Value Analysis
- Identified missing values in four columns:
  - `waterfront` — 2,391 missing → filled with `0` (assumed no waterfront)
  - `view` — 63 missing → filled with the **mode**
  - `sqft_basement` — 452 missing → filled with `0`
  - `yr_renovated` — 3,848 missing → filled with `0` (never renovated)
- Visualised missing data using `missingno` matrix and bar charts.

### 3. Outlier Detection & Cleaning
- Found a property listed with **33 bedrooms** but only 1,620 sqft of living space — clearly a data entry error.
- Corrected the value to **3 bedrooms** after comparing against similar-sized properties.

### 4. Feature Engineering
New columns were derived to support deeper analysis:

| Feature | Description |
|---|---|
| `month` / `month_name` | Month of sale extracted from `date` |
| `dist_from_center` | Euclidean distance from the geographic median center (47.57°N, -122.23°W) |
| `is_central` | `True` if property is within 0.1 degrees of the center |
| `is_expensive` | `True` if price exceeds the 75th percentile ($645,000) |
| `is_renovated` | `True` if `yr_renovated > 0` |
| `price_per_sqft` | Price divided by `sqft_living` |
| `season` | Categorised as Spring, Winter, or Other based on sale month |
| `dist_to_target` | Distance from a specific investor target location |

---

## Key Findings

### Location & Price
- The geographic center of the dataset falls near **ZIP code 98040**.
- Properties closer to the center command a significantly **higher price per square foot**.
- A Pearson correlation test confirmed a **negative relationship** between distance from center and price/sqft — the further from the center, the lower the value.

### Renovation Impact (Central Properties)
- Among central properties, **renovated homes sell at a higher average price** than non-renovated ones.
- This validates the hypothesis that renovation adds measurable value, especially in high-demand central areas.

### High-Grade Properties
- 1,635 properties have a `grade > 9`, representing premium construction quality.
- These properties are predominantly **expensive** (`is_expensive = True`) and concentrated in central ZIP codes.

### Seasonal Pricing — The "Golden Window"
- Sale prices peak in **Spring (March–May)**, which is identified as the **Golden Window** for sellers.
- Spring average price: **~$553,000**
- Winter average price: **~$520,000**
- The **Spring Premium** is approximately **$33,000 (~6.3% higher)** compared to winter sales.
- **Recommendation:** Complete renovations by February and list properties in Spring to maximise returns.

---

## Actionable Insights Summary

| Insight | Recommendation |
|---|---|
| Central properties have higher $/sqft | Prioritise purchasing near ZIP 98040 |
| Renovated central homes sell higher | Invest in renovation before selling |
| Spring prices are ~6% higher than winter | List properties between March and May |
| Grade > 9 correlates with premium pricing | Target high-grade properties for investment |

---

## How to Run

1. Clone the repository and navigate to the project folder.
2. Ensure the dataset is placed at `data/eda.csv`.
3. Install the required libraries:
   ```bash
   pip install numpy pandas matplotlib seaborn scipy missingno
   ```
4. Open and run the notebook:
   ```bash
   jupyter notebook Final_Project.ipynb
   ```

---

## Author

**Swari**
EDA Final Project — King County House Sales Dataset
