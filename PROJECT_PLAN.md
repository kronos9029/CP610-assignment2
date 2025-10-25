# CP610 Project Deliverable #2 - Analysis Plan

## Project Overview
This document outlines the comprehensive plan for analyzing the sales and customer data for CP610 Deliverable #2.

---

## Data Sources
- **Sales Data**: `Sales_v4.csv` (2.47 MB, ~50,000+ transactions)
- **Customer Data**: `Customers_v4.csv` (62.8 KB)
- **Analysis Workbook**: `CP610_D2_Liam_n_Pham.xlsx`

---

## Analysis Phases

### Phase 1: Data Understanding & Preparation ✅ COMPLETED
**Objective**: Load, explore, and clean the datasets

**Status**: ✅ Cleaning completed
**Documentation**: See `CLEANING_STRATEGY.md` for detailed methodology
**Scripts**:
- `cleaning/customer_cleaning.ipynb` - Customer data cleaning
- `cleaning/sale_cleaning.ipynb` - Sales data cleaning

**Cleaned Data Output**:
- `output_data/Customers_cleaned.csv` - Cleaned customer data
- `output_data/Sales_cleaned.csv` - Cleaned sales data with unique Transaction IDs
- `output_data/Customer_Quality_Report.txt` - Customer data quality report
- `output_data/Sales_Quality_Report.txt` - Sales data quality report

#### Key Achievements:
1. **Load Data** ✅
   - Imported Sales_v4.csv (25,000 transactions)
   - Imported Customers_v4.csv (~1,000 customers)
   - Examined data structure and schemas

2. **Data Profiling** ✅
   - Checked data types and dimensions
   - Identified missing values
   - Detected 334 duplicate Transaction IDs
   - Examined data distributions
   - Identified outliers and anomalies

3. **Data Quality Assessment** ✅
   - Validated date ranges (found future dates)
   - Checked for inconsistent formatting
   - Verified referential integrity between Sales and Customers
   - Documented data quality issues comprehensively

4. **Data Cleaning** ✅
   - **Critical Issue Resolved**: 339 duplicate Transaction IDs made unique using Transaction_ID + Date composite key
   - Composite key format: `TXN_XXXXXX_YYYYMMDD` (e.g., `TXN_490235_20240125`)
   - Semantically meaningful: reflects business reality (Transaction IDs unique within each date)
   - 100% uniqueness achieved naturally without artificial suffixes
   - Handled missing values (median imputation for age)
   - Removed duplicate Customer IDs
   - Standardized formats (dates converted to datetime, text fields trimmed)
   - Addressed outliers (removed invalid ages/tenure)
   - Validated mathematical consistency (recalculated totals where needed)
   - Added feature engineering (date components, profit metrics)
   - Created data quality flags for transparency

---

### Phase 2: Exploratory Data Analysis (EDA)

#### 2.1 Sales Analysis
**Objective**: Understand sales patterns and trends

##### Analyses to Perform:
1. **Temporal Analysis**
   - Sales trends over time (daily, weekly, monthly, yearly)
   - Seasonality patterns
   - Year-over-year growth rates
   - Peak sales periods identification

2. **Product Analysis**
   - Top-selling products/categories
   - Product performance comparison
   - Revenue contribution by product
   - Product mix analysis

3. **Transaction Analysis**
   - Average order value (AOV)
   - Transaction frequency distribution
   - Order size distribution
   - Transaction value segments

4. **Regional/Geographic Analysis** (if applicable)
   - Sales by region/location
   - Geographic performance comparison
   - Regional trends

#### 2.2 Customer Analysis
**Objective**: Understand customer behavior and characteristics

##### Analyses to Perform:
1. **Customer Demographics**
   - Age distribution
   - Gender breakdown
   - Geographic distribution
   - Customer segment profiles

2. **Customer Behavior**
   - Purchase frequency analysis
   - Customer lifetime value (CLV)
   - RFM Analysis (Recency, Frequency, Monetary)
   - Customer retention metrics

3. **Customer Segmentation**
   - High-value vs. low-value customers
   - Active vs. inactive customers
   - Customer cohort analysis
   - Behavioral segments

#### 2.3 Integrated Sales-Customer Analysis
1. **Customer Purchase Patterns**
   - Products preferred by customer segments
   - Purchase patterns by demographics
   - Cross-selling opportunities

2. **Customer Journey**
   - First purchase analysis
   - Repeat purchase behavior
   - Customer churn analysis

---

### Phase 3: Statistical Analysis

#### 3.1 Descriptive Statistics
- Summary statistics for key metrics
- Central tendency measures (mean, median, mode)
- Dispersion measures (standard deviation, variance, range)
- Distribution characteristics

#### 3.2 Correlation Analysis
- Relationship between variables
- Correlation matrices
- Identify key drivers of sales

#### 3.3 Hypothesis Testing (if applicable)
- Compare groups (e.g., customer segments)
- Test for statistical significance
- A/B test analysis (if applicable)

---

### Phase 4: Advanced Analytics

#### 4.1 Predictive Modeling
**Potential Models**:
1. **Sales Forecasting**
   - Time series forecasting (ARIMA, Prophet, etc.)
   - Predict future sales trends
   - Seasonal decomposition

2. **Customer Churn Prediction**
   - Identify at-risk customers
   - Logistic regression or classification models

3. **Customer Lifetime Value Prediction**
   - Predict future customer value
   - Regression models

#### 4.2 Clustering Analysis
- Customer segmentation using K-Means, hierarchical clustering
- Product clustering
- Market basket analysis (association rules)

#### 4.3 Anomaly Detection
- Identify unusual transactions
- Detect fraud patterns (if applicable)
- Outlier analysis

---

### Phase 5: Business Intelligence & Insights

#### 5.1 Key Performance Indicators (KPIs)
Define and calculate:
- Total Revenue
- Revenue Growth Rate
- Average Order Value (AOV)
- Customer Acquisition Cost (if data available)
- Customer Retention Rate
- Customer Churn Rate
- Customer Lifetime Value (CLV)
- Purchase Frequency
- Product Performance Metrics

#### 5.2 Actionable Insights
Extract business insights:
1. **Revenue Optimization**
   - Identify high-margin products
   - Optimize pricing strategies
   - Promotional effectiveness

2. **Customer Retention**
   - Identify retention drivers
   - Target high-value customer segments
   - Reduce churn

3. **Marketing Optimization**
   - Target customer segments
   - Personalization opportunities
   - Campaign effectiveness

4. **Operational Efficiency**
   - Inventory optimization
   - Resource allocation
   - Process improvements

---

### Phase 6: Visualization & Reporting

#### 6.1 Visualization Strategy
**Charts and Graphs**:
1. **Time Series Plots**
   - Sales trends over time
   - Seasonal patterns

2. **Bar Charts**
   - Top products
   - Customer segments
   - Regional comparisons

3. **Pie Charts**
   - Revenue composition
   - Customer demographics

4. **Heatmaps**
   - Correlation matrices
   - Sales by day/hour

5. **Scatter Plots**
   - Relationship visualizations
   - Customer segmentation

6. **Box Plots**
   - Distribution comparisons
   - Outlier visualization

7. **Histograms**
   - Data distributions
   - Frequency analysis

#### 6.2 Dashboard Creation
- Interactive dashboard (if using tools like Tableau/Power BI)
- Executive summary dashboard
- Detailed analytical views

#### 6.3 Report Structure
1. **Executive Summary**
   - Key findings
   - Strategic recommendations
   - High-level insights

2. **Methodology**
   - Data sources
   - Analytical approaches
   - Assumptions and limitations

3. **Detailed Analysis**
   - Sales analysis findings
   - Customer analysis findings
   - Statistical results
   - Predictive model results

4. **Visualizations**
   - All key charts and graphs
   - Supporting tables

5. **Recommendations**
   - Actionable business recommendations
   - Strategic initiatives
   - Next steps

6. **Appendices**
   - Technical details
   - Additional data tables
   - Code/methodology details

---

## Tools & Technologies

### Primary Tools:
- **Python**: pandas, numpy, scikit-learn, matplotlib, seaborn
- **Excel**: CP610_D2_Liam_n_Pham.xlsx for analysis and documentation
- **Statistical Analysis**: scipy, statsmodels
- **Visualization**: matplotlib, seaborn, plotly (optional)

### Optional Tools:
- Jupyter Notebooks for exploratory analysis
- Tableau/Power BI for dashboards (if applicable)

---

## Deliverables Checklist

### Must Have:
- [ ] Cleaned and processed datasets
- [ ] Comprehensive EDA report
- [ ] Statistical analysis results
- [ ] Key visualizations (minimum 10-15 charts)
- [ ] Business insights and recommendations
- [ ] Final Excel workbook with all analysis
- [ ] Executive summary document

### Nice to Have:
- [ ] Predictive models (forecasting, churn prediction)
- [ ] Interactive dashboard
- [ ] Customer segmentation model
- [ ] Automated reporting scripts

---

## Timeline & Milestones

### Week 1: Data Preparation & EDA
- Days 1-2: Data loading, profiling, and cleaning
- Days 3-5: Exploratory data analysis
- Day 6-7: Initial visualizations and insights

### Week 2: Advanced Analysis & Modeling
- Days 1-3: Statistical analysis and hypothesis testing
- Days 4-5: Predictive modeling (if applicable)
- Days 6-7: Clustering and segmentation

### Week 3: Insights & Reporting
- Days 1-3: Extract business insights
- Days 4-5: Create visualizations and dashboards
- Days 6-7: Write final report and documentation

---

## Risk Mitigation

### Potential Challenges:
1. **Data Quality Issues**
   - **Mitigation**: Thorough data profiling and validation
   - Document all assumptions and data limitations

2. **Missing Data**
   - **Mitigation**: Use appropriate imputation techniques
   - Consider sensitivity analysis

3. **Computational Constraints**
   - **Mitigation**: Optimize code, use sampling if needed
   - Consider cloud computing resources

4. **Time Constraints**
   - **Mitigation**: Prioritize must-have deliverables
   - Use efficient coding practices

---

## Success Criteria

The project will be considered successful if:
1. ✓ All data quality issues are identified and addressed
2. ✓ Comprehensive analysis covers sales, customers, and integrated views
3. ✓ Minimum 10-15 high-quality visualizations
4. ✓ At least 5 actionable business insights identified
5. ✓ Clear, professional report delivered
6. ✓ All analysis reproducible and documented

---

## Notes & Assumptions

### Key Assumptions:
- Data represents actual business transactions
- Currency is consistent across all transactions
- Customer IDs are unique and consistent
- Date ranges are valid and complete

### Questions to Resolve:
- What is the business context (industry, company size)?
- Are there specific business questions to answer?
- What is the target audience for the report?
- Are there specific KPIs the business tracks?

---

## Contact & Collaboration

**Project Team**: Liam & Pham
**Course**: CP610
**Deliverable**: #2

---

*Last Updated: October 24, 2025*
