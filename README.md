# 📊 Media Mix Modeling (MMM)

## 📌 Objective

The objective of this project is to build a robust Media Mix Model (MMM) that quantifies the impact of various media channels, control variables, and geographic factors on weekly sales. The model aims to inform ROI-driven marketing decisions across both time and regions.

---

## 🧰 Tech Stack

- **Language**: Python 3.12.4
- **Libraries**: `pandas`, `numpy`, `matplotlib`, `seaborn`, `statsmodels`

---

## 🧪 Methodology

### 1. Data Preparation
- 6,240 weekly observations across 40 geographies.
- No missing or duplicated values.
- Extracted `year`, `month`, `quarter`, and `weekofyear` from the `date` column.

### 2. Feature Engineering
- **Geographic Encoding**: Converted `geo` to dummy variables.
- **Seasonality Capture**: Used sine and cosine transformations of the `month` to preserve cyclical patterns.
- **Exclusion of Impressions**: Due to collinearity with spend and lack of strategic meaning.

### 3. Media Transformation
- **Adstock Transformation**: Simulated lagged advertising effect (decay = 0.5).
- **Log Saturation**: Modeled diminishing returns via `np.log1p`.

### 4. Modeling
- Used OLS regression with:
  - Transformed spend (`*_spend_transformed`)
  - Control variables: `population`, `competitor_sales_control`, `sentiment_score_control`
  - Seasonality: `month_sin`, `month_cos`
  - Regional fixed effects (`geo_*` dummies)

---

## 📈 Results

### Model Performance
- **R²**: 0.696
- **Adjusted R²**: 0.694
- **F-statistic**: 295.2
- **Observations**: 6,240

### Statistically Significant Media Channels
- **Positive & Significant**: TV, Print, Search
- **Not Significant**: Social (at global level)

### Control Variables
- `population`: strong, positive effect
- `competitor_sales_control`: negative, significant
- `sentiment_score_control`: weak, negative

---

## 💰 ROI & Contribution Analysis

| Channel | ROI  | Contribution |
|---------|------|--------------|
| TV      | 6.95 | 45,166       |
| Print   | 4.66 | 9,025        |
| Social  | 3.05 | 23,329       |
| Radio   | 2.73 | 13,701       |
| Search  | 0.13 | 1,828        |

- **TV** is the most efficient channel.
- **Print** shows high regional effectiveness (e.g., Geo9 in Q4).
- **Search** has low ROI, indicating overinvestment or inefficiency.

---

## 🧪 Model Validation

- **Ljung–Box test**: No significant autocorrelation (p = 0.118)
- **Breusch–Pagan test**: Heteroskedasticity present (p < 0.001)
- **ACF/PACF**: Residuals show no strong temporal structure

✅ Most linear model assumptions are met.

---

## 🔍 Regional & Temporal Insights

Generated granular ROI/contribution estimates per `(geo, year, month, channel)`:
- Print performs exceptionally in specific periods/geographies.
- Enables precise, local-level budget optimization strategies.

👉 See: `data/ROI_Contribution_geo_year.csv`

---

## 🚀 Future Enhancements

1. **Advanced Modeling**:
   - Bayesian Hierarchical Models
   - Channel-specific adstock tuning
   - Predictive layers with LSTM or GRU

2. **Feature Enrichment**:
   - Weather, event flags, spatial relationships

3. **Deployment**:
   - Streamlit / Power BI dashboards
   - MLflow logging & experiment tracking
   - Modularized ETL and model pipelines

---

## ✅ Business Takeaways

- TV delivers the highest ROI and contribution overall.
- Print outperforms in specific regions and quarters.
- Social is moderately effective in a multichannel context.
- ROI and sales effectiveness vary significantly by region and time, confirming the need for geo-aware strategies.

---

## 🧪 How to Validate the Model?

- Sensitivity checks on coefficients
- Backtesting on past campaigns (e.g., Q4 2022)
- Scenario simulation dashboards
- Controlled geographic budget tests (last resort)

---

## Author

**Rafael Rincón Ramírez**  
Data Scientist
Email: rafael.rincon.ramirez@gmail.com
