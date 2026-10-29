## Business problem


Used car dealers need inventory and asking prices that match what buyers pay in the secondary market. This project analyzes the course **used car listings dataset** (~426K Craigslist-style rows) to identify which features move price up or down, following the **CRISP-DM** process.

**Audience for this report:** dealership owners and inventory managers (non-technical).


## Analysis notebook


Interactive code, charts, and regression modeling:


**[notebooks/used_cars_pricing_analysis.ipynb](notebooks/used_cars_pricing_analysis.ipynb)**


Run the notebook from the notebooks/ folder (or set the kernel working directory so ../data/vehicles.csv resolves). The dataset is kept locally under data/ because of file size.

## Summary of findings


### What drives higher prices


1. **Newer model years** — Strong positive relationship with listing price (correlation ≈ **0.61**). Median price is about **$32.9K** for vehicles **0–3 years** old vs. about **$8.0K** for **8+ years** (2022 snapshot).
2. **Lower odometer readings** — Higher mileage aligns with lower prices (correlation ≈ **-0.60**). Use age and mileage together when sourcing and pricing.
3. **Better condition ratings** — Listings reported as **new**, **good**, or **like new** show higher median prices than **fair** or **salvage** condition.
4. **Clean title status** — **Clean-title** vehicles price above **salvage** and many **rebuilt** titles; salvage acquisitions need large margins to be worthwhile.
5. **Brand and segment** — Manufacturer, fuel type, drive type, and body type shift median price even at similar age and mileage (e.g., trucks/diesel vs. economy sedans).


### Data quality


**426,881** raw listings; after filtering unrealistic prices/years and requiring core fields for modeling, **~149K** rows remain for exploration and regression.
Many optional columns (VIN, paint, size) are often missing; analysis focuses on consistently populated attributes.
### Modeling results


**Models:** Linear Regression, Ridge, and Lasso with one-hot encoded categories and scaled numeric features.
**Validation:** 3-fold cross-validation; **grid search** on Ridge/Lasso alpha.
**Metric:** **MAE (mean absolute error in dollars)** — interpretable for dealers (“typical error of about $X when predicting listing price”).
**Performance (50K-row modeling sample):** Hold-out **MAE ≈ $4,812**; **R² ≈ 0.71** — useful for benchmarking, not a substitute for inspection and local comps.
---


## Recommendations (action items)


1. **Prioritize 3–6-year, lower-mileage, clean-title units** in the mix that already show the strongest median prices.
2. **Set lot prices using age–mileage–segment benchmarks** from the model and EDA rather than flat markups.
3. **Avoid heavy salvage/poor-condition stock** unless acquisition cost reflects the persistent discount in the data.
4. **Highlight mileage, title, and condition in ads** — these separate higher-priced comps in the listings.
5. **Re-run the notebook each quarter** with fresh data as market conditions change.


---


## Project layout


Module11/
├── README.md
├── notebooks/
│   └── used_cars_pricing_analysis.ipynb
├── data/
│   └── vehicles.csv
└── .gitignore


## Author
Jyothsna