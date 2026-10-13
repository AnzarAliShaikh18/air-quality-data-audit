Air Quality Under the Microscope

An exploratory audit of historical air-quality measurements from 12 monitoring stations across Beijing. This project examines PM2.5 data quality and patterns that would matter before using the dataset in a future prediction task.

## Research Question

How do missing measurements and PM2.5 patterns differ between Beijing's monitoring stations, and what data-quality issues should be addressed before using these observations to train a prediction model?

This is an exploratory analysis. It does not train a model or establish causes of air pollution.

## Dataset

- **Name:** Beijing Multi-Site Air Quality Data
- **Source:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/501/beijing)
- **Coverage:** 12 monitoring stations, with hourly observations from **March 1, 2013 through February 28, 2017**
- **Scale in this notebook:** 420,768 station-hour records and 18 source columns
- **Download:** [Original dataset page at UCI](https://archive.ics.uci.edu/dataset/501/beijing)

Download the dataset from UCI and extract the 12 station CSV files into `data/raw/`. Raw CSV files are intentionally not tracked in Git; see [`data/README.md`](data/README.md) for the data placement note.

## Tools


- Pythons
- Jupyter Notebook
- pandas and NumPy for data loading and analysis
- Matplotlib for charts

## Repository Structure

```text
.
├── analysis.ipynb                         # Exploratory data audit
├── requirements.txt                       # Python dependencies
├── data/
│   ├── README.md                          # Dataset download and placement
│   └── raw/                               # Place the 12 source station CSVs here (not tracked)
├── mean_pm2.5_by_calendar_month.png       # Calendar-month comparison
├── mean_pm2.5_by_monitoring_station.png    # Mean PM2.5 by station
├── mean_vs_median_pm2.5_by_station.png     # Mean and median by station
├── missing_pm2.5_by_station.png            # Missing PM2.5 share by station
└── monthly_mean_pm2.5_across_beijing.png   # Monthly mean time series
```

## Analysis

The notebook loads all CSV files found directly in `data/raw/`, combines them into one table, and explores:

- Dataset dimensions, columns, and station coverage
- Missing values across variables and missing PM2.5 values by station
- PM2.5 summary statistics overall and by station
- Mean and median PM2.5 by station
- Monthly mean PM2.5 over time and by calendar month

The notebook uses the year, month, day, and hour fields to create timestamps for the time-series summaries.

## Key Findings

Based on the results saved in the notebook:

- The combined data contains **420,768 records** from **12 stations** across the four-year date range.
- PM2.5 has **8,739 missing values**, about **2.08%** of all records. Missingness varies by station: Huairou is highest at about **2.72%**, while Wanliu is lowest at about **1.09%**.
- Recorded PM2.5 values are right-skewed: the overall mean is about **79.79**, above the median of **55**. The maximum recorded value is **999**, so extreme values merit review before modeling.
- Station-level mean PM2.5 ranges from about **65.99** at Dingling to **86.19** at Dongsi. These are descriptive comparisons; the notebook does not assess whether station differences are statistically significant or explain their causes.
- Calendar-month means vary, from about **53.47** in August to **104.58** in December. These summaries combine observations across years and stations and should not be interpreted as causal or year-specific conclusions.

Concentration values are reported as present in the source data; the notebook does not perform unit validation or data correction.

## Limitations

- The analysis is descriptive and does not test causal explanations or train or evaluate a prediction model.
- Missing observations are summarized but not imputed; their timing and possible causes are not investigated.
- The high maximum PM2.5 reading and other potential outliers are not validated against source documentation or external measurements.
- Monthly and station averages can conceal hourly variation, year-to-year differences, and differences in measurement coverage.
- No uncertainty estimates or formal significance tests are calculated.
- Results depend on the downloaded source files and the notebook's current preprocessing choices.

## How to Run

1. Clone this repository and open its folder.
2. Create and activate a Python environment. For example, with `venv`:

   ```bash
   python -m venv .venv
   ```

   Activate it with `source .venv/bin/activate` on macOS/Linux, or `.venv\\Scripts\\Activate.ps1` in PowerShell.
3. Install dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```
4. Download the [Beijing Multi-Site Air Quality dataset from UCI](https://archive.ics.uci.edu/dataset/501/beijing).
5. Extract the **12 station CSV files** directly into `data/raw/`. The notebook expects those CSVs in that folder.
6. Open `analysis.ipynb` in Jupyter Notebook or JupyterLab.
7. Restart the kernel and run all cells.

## Future Work

- Inspect when missing values occur and whether missingness differs by station, season, or hour.
- Review extreme readings and confirm expected units and valid ranges using dataset documentation.
- Compare trends by station and year, and quantify uncertainty in summary comparisons.
- Document data validation and preprocessing decisions before building a prediction baseline.
- If a model is developed, use time-aware validation and clearly document its target, features, and evaluation limits.