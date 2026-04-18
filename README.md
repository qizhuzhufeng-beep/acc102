# Did Rising Inflation Erode Real Purchasing Power in the United States?

## 1. Question

This project studies whether rising inflation was associated with weaker real purchasing power in the United States. The central idea is straightforward: if consumer prices rise faster than wages, households may be able to buy less with their income even when nominal pay is increasing.

The project does not attempt to identify a causal effect. Instead, it provides a descriptive comparison between inflation, nominal wage growth, and a simple measure of real wage pressure.

## 2. Data Source

The project uses monthly macroeconomic data from the Federal Reserve Bank of St. Louis FRED database. The four series are:

- `CPIAUCSL`: Consumer Price Index for All Urban Consumers
- `CES0500000003`: Average Hourly Earnings of All Employees, Total Private
- `UNRATE`: Unemployment Rate
- `USREC`: NBER recession indicator

These series are public and widely used in introductory macroeconomic analysis. In this repository, the raw files are stored in `data/raw/` with metadata columns so that each file remains traceable.

## 3. Method

The workflow is intentionally simple and appropriate for an undergraduate economics assignment.

1. Download the raw monthly series from FRED.
2. Merge the four series by `DATE`.
3. Convert the value columns to numeric format.
4. Compute:
   - `CPI_YOY = pct_change(12) * 100`
   - `WAGE_YOY = pct_change(12) * 100`
   - `REAL_WAGE_PRESSURE = WAGE_YOY - CPI_YOY`
5. Export a clean dataset and three figures.

`REAL_WAGE_PRESSURE` is the main summary measure. When it is negative, nominal wages are growing more slowly than consumer prices.

## 4. Main Findings

The clean dataset suggests three broad patterns.

- Inflation and wage growth do not always move together.
- In some periods, especially when inflation rises quickly, wage growth does not fully keep pace.
- When `REAL_WAGE_PRESSURE` falls below zero, this is consistent with weaker real purchasing power.

These findings should be interpreted as descriptive evidence rather than proof of a causal relationship. Many other factors, such as taxes, hours worked, transfers, and differences across households, also affect purchasing power.

## 5. Repository Structure

```text
README.md
requirements.txt
config/
  fred_series.json
src/
  fetch_fred_data.py
  build_dataset.py
  make_figures.py
notebooks/
  NOTEBOOK_Main_20260418.ipynb
logs/
  UPDATE_LOG.md
backup/
  20260418/
data/
  raw/
  clean/
figures/
```

## 6. How to Run

1. Install dependencies:

```bash
pip install -r requirements.txt
```

2. Download raw FRED data:

```bash
python src/fetch_fred_data.py
```

3. Build the clean dataset:

```bash
python src/build_dataset.py
```

4. Export figures:

```bash
python src/make_figures.py
```

5. Open the notebook:

```bash
jupyter notebook notebooks/NOTEBOOK_Main_20260418.ipynb
```

## 7. Limitations

This project has several limitations.

- It is descriptive and does not establish causality.
- Average hourly earnings do not capture all forms of household income.
- CPI is an aggregate price index and may not reflect the experience of every household.
- Some data points may be revised over time in FRED.
- Differences in release timing can create temporary missing values in monthly macroeconomic series.

## 8. AI Disclosure

AI tools were used to support the drafting of code, notebook text, and project documentation. The project design, variable selection, interpretation, and final review were supervised and checked by the author. All outputs should be treated as part of a student-led academic workflow rather than as automatically verified results.
