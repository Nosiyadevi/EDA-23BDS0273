# Exploratory Data Analysis (EDA): Assessments 1 to 9
 
| | |
|---|---|
| **Student** | Nosiyadevi |
| **Register No.** | 23BDS0273 |
| **Language** | Python (Jupyter Notebook) |
| **Dataset** | `indo_rct.csv` (602 rows x 34 columns) |
| **Demo video** | [Watch the project demonstration](https://drive.google.com/file/d/1aWG7m5zyTK3zcmMaA9tlcGq8gFpEW2dj/view?usp=drive_link) |
 
## About the project
 
This repository holds a complete EDA workflow covering nine assessments, built around the **indo_rct** dataset: a randomized clinical trial of indomethacin for preventing post-ERCP pancreatitis. The notebook is written so that columns are detected automatically (numeric vs. categorical), and every result shown is the actual output of the run.
 
The dataset has 4 trial sites (`1_UM`, `2_IU`, `3_UK`, `4_Case`), patient details (`age`, `gender`, `risk`), the treatment arm (`rx`: placebo vs. indomethacin), and many yes/no procedure and outcome indicators such as `outcome`, `sod`, `pep`, `recpanc`, `prophystent` and `pdstent`.
 
## Repository contents
 
| File | Description |
|---|---|
| `23BDS0273_EDA_Assessments_1_to_9_Python.ipynb` | Notebook with all code (add if available) |
| `23BDS0273_EDA_Final_Submission.pdf` | Final printed report with output (58 pages) |
| `README.md` | This file |
 
## Libraries used
 
`numpy`, `pandas`, `matplotlib`, `seaborn`, `scipy`, `scikit-learn`, `statsmodels`
 
## Assessment summary
 
### Assessment 1: DataFrame operations and data transformation
- Created three product DataFrames (10 records each).
- Appended rows with `concat`, joined side by side, and performed **inner, left, right and full outer joins** on `ProductID`.
- Transformed a 10-value vector (first value 273, from the register number 0273) using **min-max (0 to 1)**, rescaling to **[-1, 1]** and **[-3, 3]**, **z-score** and **decimal scaling**.
### Assessment 2: Data import, cleaning and basic statistics
- Loaded the dataset from a URL: **602 rows, 34 columns**.
- Inspected head/tail, data types, summary statistics and missing values.
- Only one column has missing data: **`bleed` has 575 missing values (95.51%)**. Dropping all rows with missing values would leave just 27 rows.
- Demonstrated mean/median/mode imputation, forward/backward/constant fill, duplicate check (0 duplicates), column renaming and a derived column.
### Assessment 3: Data cleaning and univariate analysis
- Removed `bleed` (more than 70% missing), giving a cleaned shape of **(602, 33)**.
- Converted text columns to categorical type and checked outliers with the IQR rule (0 outliers in `rownames`).
- Plots: boxplot, histogram with density, density, dot plot, bar, pie, percentage bar, lollipop and faceted histograms.
- **Site distribution:** 2_IU 413 (68.6%), 1_UM 164 (27.2%), 3_UK 22 (3.7%), 4_Case 3 (0.5%).
### Assessment 4: Bivariate analysis
- **Site by gender** contingency table with stacked and grouped bars. Females are the majority at every site (e.g. 345 vs 68 at 2_IU).
- Scatter, line and correlation heatmap for numeric pairs. `rownames` and `id` are strongly correlated (about 0.90), while `age` and `risk` are weakly negatively correlated (-0.22).
- Numeric by category: density, box, violin and combined violin + box plots.
### Assessment 5: Multivariate analysis
- Three- and four-variable scatter plots (colour, marker shape, point size), bubble plot, facet wrap and facet grid.
- Pairs plot of numeric variables and a parallel coordinates plot with standardized values.
### Assessment 6: Time-series analysis (AirPassengers)
- Loaded the monthly AirPassengers series: **144 observations, 1949-01 to 1960-12**.
- Multiplicative seasonal decomposition (trend, seasonal, residual), ACF and PACF plots.
- Fitted **ARIMA(2,1,2)** (AIC 1353.35) and produced a **12-month forecast** for 1961 with 95% confidence intervals (for example, 1961-01: about 440 passengers).
- Note: a non-seasonal ARIMA is used to follow the assessment; a seasonal model (SARIMA) would fit this data better.
### Assessment 7: One, two and n-dimensional analysis
- Summary statistics table (mean, median, range, variance, SD, IQR, skewness, kurtosis).
- Frequency and relative frequency tables, pie and bar charts, binned histogram and boxplot.
- Contingency table with row and column percentages, grouped statistics by site (mean `rownames` per site: 2_IU 371.0, 1_UM 82.5, 3_UK 588.5, 4_Case 601.0).
- **Pearson correlation = 0.897, Spearman = 1.0** for `rownames` vs `id`, regression line, correlation matrix and scatterplot matrix.
### Assessment 8: K-Means and hierarchical clustering
- Standardized numeric features (`rownames`, `id`, `age`, `risk`).
- K-Means with k=2 (cluster sizes **164 and 438**), elbow plot for k=1 to 10, then k=3.
- Hierarchical clustering with **Ward linkage**, dendrogram, and 3-cluster result (sizes **164, 300, 138**).
### Assessment 9: Principal Component Analysis (PCA)
- PCA on four standardized numeric variables.
| Component | Explained variance | Cumulative |
|---|---|---|
| PC1 | 49.18% | 49.18% |
| PC2 | 28.84% | 78.02% |
| PC3 | 19.43% | 97.45% |
| PC4 | 2.55% | 100% |
 
- Scree plot (y-axis limit 0 to 60), PC1 vs PC2 score plot and a biplot with variable loading arrows. The first two components capture about **78%** of the variance.
## Key observations
 
1. `bleed` is almost entirely empty (95.5%), so it was dropped rather than imputed.
2. Patients are heavily concentrated at one site (2_IU, 68.6%), and females make up most of the sample (476 of 602).
3. `rownames` and `id` are ordering/identifier columns, so their correlations reflect row order and not real relationships. They would normally be excluded from clustering and PCA.
4. Clustering and PCA separate patients mainly by site, which follows from `rownames` and `id` being included.
5. The ARIMA forecast follows the upward trend but ignores seasonality, so SARIMA is recommended for monthly passenger data.
## How to run
 
```bash
git clone https://github.com/Nosiyadevi/EDA-23BDS0273.git
cd EDA-23BDS0273
pip install numpy pandas matplotlib seaborn scipy scikit-learn statsmodels jupyter
jupyter notebook 23BDS0273_EDA_Assessments_1_to_9_Python.ipynb
```
 
The notebook downloads the dataset and the AirPassengers CSV from public URLs, so an internet connection is needed.
 
## Interpretation notes
 
- An outlier flagged by the IQR rule is not automatically an error.
- Correlation shows association, not causation.
- Cluster labels are group IDs, not rankings.
- ARIMA forecasts are estimates and carry uncertainty.
---
**Author:** Nosiyadevi | 23BDS0273
