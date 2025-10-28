# Excel EDA Plan - CP610 Deliverable #2

**Project**: Sales & Customer Data Analysis
**Team**: Liam & Pham
**Date**: October 27, 2025
**Last Updated**: October 27, 2025

---

## 📋 Deliverable Requirements Overview

This plan is structured to address the specific requirements from CP610 Deliverable #2:

### **Question 2: EDA Workflow (What to Do)**
a. Understand data structure and quality ✅ **COMPLETED**
b. Identify patterns, trends, and relationships ⏭️ **CURRENT FOCUS**
c. Detect outliers and anomalies 📋 **PENDING**
d. Generate hypotheses for further investigation 📋 **PENDING**

### **Question 3: Techniques to Use (How to Do It)**
a. Descriptive Statistics 🔄 **ONGOING** (used throughout)
b. Visualization ⏭️ **IN PROGRESS**
c. Correlation Analysis 📋 **PENDING**
d. Hypothesis Workflow 📋 **PENDING**

---

## 📊 Sheet Responsibilities & Question Mapping

This table shows which Excel sheets address which deliverable questions:

| Sheet Name | Purpose | Addresses Question | Status | Notes |
|------------|---------|-------------------|--------|-------|
| **README** | Documentation & metadata | Setup | ✅ Complete | Dataset overview |
| **Customers_Raw** | Original customer data | Data source | ✅ Complete | 1,001 customers |
| **Sales_Raw** | Original sales data | Data source | ✅ Complete | 25,001 transactions |
| **Checks** | Sales data validation | Q2a (structure/quality) | ✅ Complete | Quality metrics |
| **Customer Checks** | Customer validation | Q2a (structure/quality) | ✅ Complete | Validation rules |
| **Initial EDA Sales** | Sales with validation flags | Q2a (structure/quality) | ✅ Complete | 26 columns |
| **Initial EDA Customers** | Customers with flags | Q2a (structure/quality) | ✅ Complete | 16 columns |
| **Sales_Cleaned** | Master analysis dataset | Q2a (prepared data) | ✅ Complete | 31 columns, merged data |
| **Stats** | Descriptive statistics | Q3a (for Q2a, used in Q2c) | ✅ Complete | Numerical stats, correlation matrix, categorical analysis |
| **Pivots_Top10** | Top performers analysis | Q2b (patterns/trends) | ⏭️ **TO DO** | Revenue leaders |
| **Pivots** | Comprehensive aggregations | Q2b (patterns/trends) | ⏭️ **TO DO** | Multi-dimensional |
| **Charts** | All visualizations | Q2b (visualization), Q2c (box plots) | ⏭️ **TO DO** | Q3b technique |
| **Correlation** | Correlation matrix | Q2d (relationships), Q3c | 📋 Pending | To be created |
| **Insights** | Documented findings | Q2b, Q2c, Q2d (all findings) | 📋 Pending | To be created |

---

## ✅ Question 2a: Understand Data Structure & Quality (COMPLETED)

**Technique Used**: Question 3a (Descriptive Statistics)

### Completed Work:
- ✅ Data validation sheets (Checks, Customer Checks)
- ✅ Initial EDA with validation flags (Initial EDA Sales, Initial EDA Customers)
- ✅ Data cleaning and integration (Sales_Cleaned with merged customer data)
- ✅ Comprehensive descriptive statistics (Stats sheet)

### Sheets Involved:
- **Checks**: Sales data quality checks
- **Customer Checks**: Customer data quality checks
- **Initial EDA Sales**: Sales data with 26 columns including validation flags
- **Initial EDA Customers**: Customer data with 16 columns including validation flags
- **Sales_Cleaned**: Master dataset (31 columns) with composite Transaction Key and joined customer data
- **Stats**: Numerical descriptive statistics (mean, median, mode, std dev, quartiles, etc.)

### Key Achievements:
- Identified and resolved 339 duplicate Transaction IDs using composite key
- Validated data quality and documented issues
- Calculated baseline statistics for all numerical variables
- Prepared clean, analysis-ready dataset

**Status**: ✅ **COMPLETE** - Ready to move to Question 2b

---

## ⏭️ Question 2b: Identify Patterns, Trends, and Relationships (CURRENT FOCUS)

**Techniques Used**:
- **Question 3b (Visualization)** - PRIMARY technique
- **Question 3a (Descriptive Statistics)** - For categorical variable summaries

### Goal:
Use pivot tables and charts to reveal patterns, trends, and relationships in the data. Document all findings.

### Sheets Involved:
- **Pivots_Top10**: Top performers (products, customers, categories)
- **Pivots**: Multi-dimensional analysis (regions, time, segments)
- **Charts**: All visualizations (15+ charts)
- **Stats**: Add categorical frequency tables (extension of Q3a)

---

## Task 2b.1: Create Pivot Tables

### Sheet: Pivots_Top10

**Pivot 1: Top 10 Products by Revenue**
- Data Source: Sales_Cleaned table (filter Valid records only)
- Row Labels: Item
- Values: Sum of Total_Recalc
- Sort: Descending by Total_Recalc
- Filter: Top 10 items
- Additional Column: Count of transactions per item

**Pivot 2: Top 10 Customers by Revenue**
- Data Source: Sales_Cleaned table
- Row Labels: Customer ID
- Values: Sum of Total_Recalc, Count of Transaction ID
- Sort: Descending by Total_Recalc
- Filter: Top 10 customers
- Additional Columns: Membership Level, Region

**Pivot 3: Top 10 Categories by Revenue**
- Data Source: Sales_Cleaned table
- Row Labels: Category
- Values: Sum of Total_Recalc, Sum of Gross_Profit_After_Discount
- Sort: Descending by Total_Recalc
- Calculate: Gross Margin % per category

---

#### Sheet: Pivots

**Pivot 4: Sales by Region and Membership Level**
- Rows: Region
- Columns: Membership Level
- Values: Sum of Total_Recalc
- Show: % of Grand Total

**Pivot 5: Sales by Category and Location**
- Rows: Category
- Columns: Location (In-store vs Online)
- Values: Sum of Total_Recalc, Count of transactions
- Show: % of Row Total

**Pivot 6: Sales by Payment Method**
- Rows: Payment Method
- Values:
  - Sum of Total_Recalc
  - Count of transactions
  - Average of Total_Recalc
- Sort: Descending by Sum of Total_Recalc

**Pivot 7: Monthly Sales Summary**
- Rows: Year, Month
- Values:
  - Sum of Total_Recalc
  - Count of Transaction ID
  - Average of Total_Recalc
  - Sum of Gross_Profit_After_Discount
- Group by: Year and Month

**Pivot 8: Sales by Category and Region**
- Rows: Category
- Columns: Region
- Values: Sum of Total_Recalc
- Show: Heatmap formatting (conditional formatting)

**Pivot 9: Customer Demographics Summary**
- Data Source: Initial EDA Customers table
- Rows: Membership Level
- Values:
  - Count of Customer ID
  - Average Customer Age
  - Average Tenure (Years)
- Group Age into bins: 18-30, 31-40, 41-50, 51-60, 61+

**Pivot 10: Discount Analysis**
- Data Source: Sales_Cleaned table
- Rows: Category
- Columns: Discount_Zero_Flag (Yes/No)
- Values:
  - Count of transactions
  - Average Discount_Rate
  - Sum of Total_Recalc

---

## Task 2b.2: Create Visualizations (Question 3b Technique)

### Sheet: Charts

**Chart 1: Sales Trend Over Time (Line Chart)**
- Data: Monthly sales from Pivot 7
- X-axis: Month-Year
- Y-axis: Sum of Total_Recalc
- Type: Line chart with markers
- Title: "Monthly Sales Trend (2023-2025)"

**Chart 2: Total Revenue by Category (Bar Chart)**
- Data: Sum of Total_Recalc by Category
- Type: Horizontal bar chart
- Sort: Descending
- Title: "Total Revenue by Product Category"
- Show: Data labels

**Chart 3: Sales by Region (Pie Chart)**
- Data: Sum of Total_Recalc by Region
- Type: Pie chart
- Show: Percentage labels
- Title: "Revenue Distribution by Region"

**Chart 4: Online vs In-Store Sales (Column Chart)**
- Data: Sum of Total_Recalc by Location
- Type: Clustered column chart
- Show: Value labels
- Title: "Sales Comparison: Online vs In-Store"

**Chart 5: Payment Method Distribution (Bar Chart)**
- Data: Count of transactions by Payment Method
- Type: Horizontal bar chart
- Title: "Transaction Count by Payment Method"
- Show: Percentage of total

**Chart 6: Customer Distribution by Membership Level (Column Chart)**
- Data: Count of customers by Membership Level
- Type: Column chart with data labels
- Title: "Customer Distribution by Membership Level"

**Chart 7: Average Transaction Value by Membership Level (Column Chart)**
- Data: Average Total_Recalc by Membership Level
- Type: Column chart
- Show: Value labels formatted as currency
- Title: "Average Transaction Value by Membership Level"

**Chart 8: Quantity Distribution (Histogram)**
- Data: Sales_Cleaned[Quantity]
- Type: Histogram (use Data Analysis Toolpak)
- Bins: 10 bins (0-13.4 each)
- Title: "Distribution of Quantity per Transaction"
- X-axis: Quantity bins
- Y-axis: Frequency

**Chart 9: Total Revenue Distribution (Histogram)**
- Data: Sales_Cleaned[Total_Recalc]
- Type: Histogram
- Bins: Use Excel's auto-binning or 15-20 bins
- Title: "Distribution of Transaction Values"
- X-axis: Revenue bins
- Y-axis: Frequency

**Chart 10: Gross Profit by Category (Column Chart)**
- Data: Sum of Gross_Profit_After_Discount by Category
- Type: Column chart
- Sort: Descending
- Title: "Total Gross Profit by Category"
- Show: Data labels

**Chart 11: Sales by Year (Column Chart)**
- Data: Sum of Total_Recalc by Year
- Type: Column chart
- Show: Year-over-year growth % on top of bars
- Title: "Annual Sales Performance"

**Chart 12: Customer Age Distribution (Histogram)**
- Data: Initial EDA Customers[Customer Age]
- Type: Histogram
- Bins: 10 bins (age ranges)
- Title: "Customer Age Distribution"
- X-axis: Age bins
- Y-axis: Number of customers

**Chart 13: Box Plot - Transaction Values by Region**
- Data: Sales_Cleaned[Total_Recalc] grouped by Region
- Type: Box and Whisker plot (Insert > Insert Statistic Chart > Box and Whisker)
- Title: "Transaction Value Distribution by Region"
- Shows: Median, quartiles, outliers

**Chart 14: Scatter Plot - Quantity vs Total Revenue**
- Data: Sales_Cleaned[Quantity] vs Sales_Cleaned[Total_Recalc]
- Type: Scatter plot
- Add: Trendline with R² value
- Title: "Relationship: Quantity vs Transaction Value"
- X-axis: Quantity
- Y-axis: Total Revenue

**Chart 15: Heatmap - Sales by Category and Region**
- Data: From Pivot 8 (Category × Region)
- Type: Use conditional formatting with color scales
- Title: "Sales Heatmap: Category × Region"
- Colors: Green (high) to Red (low)

---

## 📊 CHART PROGRESS TRACKER

### Current Status Summary
- **Total Charts Planned**: 15
- **Completed**: 1 (7%)
- **Missing**: 14 (93%)
- **Current Chart in Workbook**: Scatter plot - "Relationship between Discount Rate and Gross Margin %" (similar to Chart 14 concept)

### Complete Chart Status Table

| # | Chart Name | Type | Status | Priority | Data Ready? | Notes |
|---|-----------|------|--------|----------|-------------|-------|
| 1 | Monthly Sales Trend | Line | ❌ Missing | Medium | No | Needs Pivot 7 (monthly aggregation) + date fix |
| 2 | Top 10 Products by Revenue | Bar | ❌ Missing | **HIGH** | ✅ YES | Data in Stats rows 60-72 - QUICK WIN |
| 3 | Sales by Region | Pie | ❌ Missing | Medium | No | Needs pivot table first |
| 4 | Online vs In-Store Sales | Column | ❌ Missing | **HIGH** | ✅ YES | Use Stats Location table - QUICK WIN |
| 5 | Payment Method Distribution | Bar | ❌ Missing | **HIGH** | ✅ YES | Data in Stats rows 53-58 - QUICK WIN |
| 6 | Customer by Membership Level | Column | ❌ Missing | Medium | No | Needs pivot table first |
| 7 | Avg Transaction by Membership | Column | ❌ Missing | Medium | No | Needs pivot table first |
| 8 | Quantity Distribution | Histogram | ❌ Missing | Low | ✅ YES | Direct from Sales_Cleaned[Quantity] |
| 9 | Total Revenue Distribution | Histogram | ❌ Missing | Low | ✅ YES | Direct from Sales_Cleaned[Total_Recalc] |
| 10 | Gross Profit by Category | Column | ❌ Missing | Medium | No | Needs pivot table first |
| 11 | Sales by Year | Column | ❌ Missing | Medium | No | Needs pivot table first |
| 12 | Customer Age Distribution | Histogram | ❌ Missing | **HIGH** | ✅ YES | Direct from Sales_Cleaned[Customer Age] - QUICK WIN |
| 13 | Box Plot - Transaction by Region | Box Plot | ❌ Missing | Low | ✅ YES | Direct from Sales_Cleaned, advanced chart |
| 14 | Scatter - Quantity vs Revenue | Scatter | ⚠️ Similar | Medium | ✅ YES | Have Discount vs Margin instead |
| 15 | Heatmap - Category × Region | Heatmap | ❌ Missing | Low | No | Needs Pivot 8 + conditional formatting |

### Priority Groups

#### 🔥 HIGH PRIORITY - Quick Wins (4 charts, ~20-30 minutes total)
**Data Already Prepared - No Pivots Needed**
1. **Chart 2**: Top 10 Products (Stats rows 60-72) - 5 min
2. **Chart 4**: Online vs In-Store (Stats Location table) - 3 min
3. **Chart 5**: Payment Method Distribution (Stats rows 53-58) - 5 min
4. **Chart 12**: Customer Age Histogram (Sales_Cleaned) - 5 min

**Recommended Order**: Complete these 4 first for quick progress!

#### ⚙️ MEDIUM PRIORITY - Need Pivots First (7 charts, ~45-60 minutes)
**Require Pivot Tables Before Charting**
- Chart 1: Monthly Sales Trend (needs Pivot 7 + date helper column)
- Chart 3: Sales by Region (needs regional pivot)
- Chart 6: Customer by Membership (needs membership pivot)
- Chart 7: Avg Transaction by Membership (needs membership pivot)
- Chart 10: Gross Profit by Category (needs category pivot)
- Chart 11: Sales by Year (needs yearly pivot)
- Chart 14: Scatter - Quantity vs Revenue (direct data, but lower priority)

#### 🎨 LOW PRIORITY - Complex Formatting (4 charts, ~30-40 minutes)
**Require Special Techniques or Advanced Features**
- Chart 8: Quantity Histogram (need to set bin width)
- Chart 9: Revenue Histogram (need to set bin width)
- Chart 13: Box Plot by Region (requires Box & Whisker chart type)
- Chart 15: Heatmap (requires Pivot 8 + conditional formatting)

### Deliverable Question Mapping

**Charts for Question 2b (Patterns, Trends, Relationships):**
- Charts 1-7, 10-11, 14-15

**Charts for Question 2c (Outliers & Anomalies):**
- Charts 8, 9, 13 (distributions and box plots)

**All Charts Support Question 3b (Visualization Technique)**

### Recommended Workflow

**Phase 1: Quick Wins (Do Now)** ⏱️ 20-30 min
1. Chart 12: Customer Age Histogram
2. Chart 2: Top 10 Products Bar Chart
3. Chart 5: Payment Method Bar Chart
4. Chart 4: Online vs In-Store Column Chart

**Phase 2: Create Missing Pivots** ⏱️ 30-40 min
- Create Pivots 1-10 from Task 2b.1
- This enables all Medium Priority charts

**Phase 3: Medium Priority Charts** ⏱️ 45-60 min
- Charts 1, 3, 6, 7, 10, 11

**Phase 4: Advanced Charts** ⏱️ 30-40 min
- Charts 8, 9, 13, 15

**Total Estimated Time**: 2.5 - 3 hours to complete all charts

---

## Task 2b.3: Add Categorical Descriptive Statistics (Question 3a Extension)

### Sheet: Stats (Add below existing Payment Method table)

Create frequency tables following the same pattern as your Payment Method table (rows 53-58).

---

#### **Table 1: Location Distribution**

**Layout** (Start at Row 65, Column C):
```
Row 65:  [blank] [blank] Location Distribution
Row 66:  [blank] [blank] Location        Count         % of Total
Row 67:  [blank] [blank] Online          [formula]     [formula]
Row 68:  [blank] [blank] In-store        [formula]     [formula]
Row 69:  [blank] [blank] Total           [formula]
```

**Formulas:**
- **D67** (Online count): `=COUNTIF(Sales_Cleaned[Location],"Online")`
- **D68** (In-store count): `=COUNTIF(Sales_Cleaned[Location],"In-store")`
- **D69** (Total): `=SUM(D67:D68)`
- **E67** (Online %): `=D67/$D$69` (format as percentage, 2 decimals)
- **E68** (In-store %): `=D68/$D$69` (format as percentage, 2 decimals)

---

#### **Table 2: Item Distribution (Top 10 by Frequency)**

**Recommended Approach:** Use Pivot Table directly in Stats sheet

**Steps:**
1. Select Sales_Cleaned table
2. Insert → Pivot Table → Existing Worksheet → Location: Stats!C72
3. Configure:
   - Rows: Item
   - Values: Count of Item
   - Add second value: Count of Item → Show Values As → "% of Grand Total"
4. Sort: Descending by Count
5. Filter: Show Top 10 only
6. Title the section: "Item Distribution (Top 10 by Frequency)"

**Alternative - Manual Method:**
- First create temporary pivot to identify top 10 items by count
- Copy item names to Stats sheet (starting C74)
- Use `=COUNTIF(Sales_Cleaned[Item],C74)` for counts
- Use `=D74/25000` for percentages
- Delete temporary pivot

---

#### **Table 3: Category Distribution**

**Layout** (Start at Row 87, Column C):
```
Row 87:  [blank] [blank] Category Distribution
Row 88:  [blank] [blank] Category        Count         % of Total
Row 89:  [blank] [blank] Electronics     [formula]     [formula]
Row 90:  [blank] [blank] Furniture       [formula]     [formula]
Row 91:  [blank] [blank] [Category 3]    [formula]     [formula]
...
Row XX:  [blank] [blank] Total           [formula]
```

**Steps:**
1. First identify unique categories from Sales_Cleaned sheet (Column: Category)
2. List each unique category manually in Column C
3. Use formulas:
   - **D89** (First category count): `=COUNTIF(Sales_Cleaned[Category],C89)`
   - Copy formula down for all categories
   - **Last row** (Total): `=SUM(D89:D[last_row])`
   - **E89** (Percentage): `=D89/$D$[total_row]` (format as percentage)
   - Copy formula down for all categories

**Verification:**
- All count totals should equal 25,000
- All percentages should sum to 100%

---

#### **Formula Pattern Summary**

All three tables follow this pattern:

| Purpose | Formula Template | Example |
|---------|------------------|---------|
| Count | `=COUNTIF(Sales_Cleaned[Column_Name], Cell_With_Value)` | `=COUNTIF(Sales_Cleaned[Location],"Online")` |
| Total | `=SUM(range_of_counts)` | `=SUM(D67:D68)` |
| Percentage | `=count_cell/$total_cell$` | `=D67/$D$69` |

**Key Tips:**
- Use $ for absolute reference on total cell (e.g., `$D$69`)
- Format percentage cells: Right-click → Format Cells → Percentage → 2 decimals
- Keep consistent spacing (2-3 blank rows between tables)
- Align all tables in Column C for visual consistency

---

**Purpose**: Extend Question 3a (Descriptive Statistics) to include categorical variables, supporting Question 2b pattern identification.

**Note**: Payment Method analysis is already complete (rows 53-58). Focus on adding Location, Item (by frequency), and Category distributions using the same formula pattern above.

---

## Task 2b.4: Document Patterns & Insights

### Sheet: Create New Sheet "Insights"

**Purpose**: Document all patterns, trends, and relationships discovered through pivots and charts.

**Format:**
| Pattern/Insight | Evidence | Statistical Support | Business Implication |
|----------------|----------|---------------------|---------------------|

**Areas to Document:**

1. **Top Performers**
   - Which product category generates most revenue?
   - Which region has highest sales?
   - Which membership level spends most?

2. **Trends**
   - Is revenue growing or declining over time?
   - Are there seasonal patterns?
   - Which months have peak sales?

3. **Customer Behavior**
   - Do Platinum members have higher average transaction values?
   - Which age groups spend more?
   - Do customers with longer tenure buy more?

4. **Operational Insights**
   - Online vs In-store preference?
   - Most popular payment methods?
   - Which categories have highest profit margins?

**Status**: Document findings as you complete pivots and charts

---

## 📋 Question 2c: Detect Outliers and Anomalies (NEXT AFTER 2b)

**Techniques Used**:
- **Question 3a (Descriptive Statistics)** - IQR method using Stats sheet quartiles
- **Question 3b (Visualization)** - Box plots to visualize outliers

### Goal:
Identify unusual data points, extreme values, and anomalies in the dataset.

### Sheets Involved:
- **Stats**: Add outlier detection calculations using existing Q1, Q3, IQR
- **Charts**: Box plots to visualize distributions and outliers
- **Insights**: Document anomalies found

---

## Task 2c.1: Calculate Outlier Bounds

### Sheet: Stats (Add Outlier Analysis Section)

**For each numerical variable, calculate:**
- Q1 (25th percentile): =QUARTILE.INC(range, 1) - **Already calculated in Stats sheet!**
- Q3 (75th percentile): =QUARTILE.INC(range, 3) - **Already calculated in Stats sheet!**
- IQR (Interquartile Range): Q3 - Q1
- Lower Bound: Q1 - 1.5 × IQR
- Upper Bound: Q3 + 1.5 × IQR
- Count of Outliers Below: COUNTIF(range, "<" & Lower Bound)
- Count of Outliers Above: COUNTIF(range, ">" & Upper Bound)
- Total Outliers: Sum of both

**Variables to analyze:**
- Quantity
- Total_Recalc
- Gross_Profit_After_Discount
- Unit Price
- Customer Age

---

## Task 2c.2: Visualize Outliers with Box Plots

### Sheet: Charts (Box plots are part of Q3b Visualization technique)

**Create box plots for:**
- Transaction values by Region (Chart 13 - already planned in Task 2b.2)
- Transaction values by Category (new)
- Quantity distribution (new)
- Customer Age by Membership Level (new)

Box plots show: Median, Q1, Q3, whiskers (1.5×IQR), and outlier points beyond whiskers.

---

## Task 2c.3: Document Anomalies Found

### Sheet: Insights (Add "Outliers & Anomalies" section)

**Document findings:**
- Any unusually high/low transactions?
- Customers with extreme purchase behavior?
- Products with unusual pricing?
- Geographic anomalies?
- Data quality issues revealed by outliers?

---

## 📋 Question 2d: Generate Hypotheses for Further Investigation (LAST STEP)

**Techniques Used**:
- **Question 3c (Correlation Analysis)** - Identify variable relationships
- **Question 3d (Hypothesis Workflow)** - Formulate testable statements

### Goal:
Based on patterns discovered in Q2b and outliers found in Q2c, generate testable hypotheses for statistical analysis.

### Sheets Involved:
- **Correlation** (new sheet): Correlation matrix using Data Analysis Toolpak
- **Insights**: Hypothesis table with 6-8 testable statements

---

## Task 2d.1: Correlation Analysis (Question 3c Technique)

### Sheet: Create New Sheet "Correlation"

**Use Data Analysis Toolpak > Correlation:**

**Variables to include:**
- Quantity
- Unit Price
- Unit_Cost
- Discount_Rate
- Total_Recalc
- Gross_Profit_After_Discount
- Gross_Margin_%
- Customer Age
- Tenure (Years)

**Create correlation matrix table** showing all pairwise correlations.

**Apply Conditional Formatting:**
- Color scale: Red (negative correlation) → White (0) → Green (positive correlation)
- Highlight strong correlations (|r| > 0.5) in bold

**Document Key Correlations:**
- Which variables have strong positive correlations?
- Which variables have strong negative correlations?
- Any surprising correlations?

---

## Task 2d.2: Generate Hypotheses (Question 3d Technique)

### Sheet: Insights (Add "Hypotheses" Section)

**Format:**
| # | Hypothesis | Variables | Suggested Test | Expected Outcome |
|---|-----------|-----------|----------------|------------------|

**Sample Hypotheses:**

1. **H1**: Platinum members have significantly higher average transaction values than Standard members
   - Variables: Membership Level, Total_Recalc
   - Test: t-test or ANOVA
   - Check: Compare means from pivot table

2. **H2**: Online purchases receive higher discount rates than In-store purchases
   - Variables: Location, Discount_Rate
   - Test: t-test
   - Check: Average discount by location

3. **H3**: Sales exhibit seasonal patterns with peaks in certain months
   - Variables: Month, Total_Recalc
   - Test: Time series analysis, seasonal decomposition
   - Check: Monthly sales chart

4. **H4**: There is a positive correlation between customer tenure and transaction frequency
   - Variables: Tenure (Years), Transaction Count per Customer
   - Test: Correlation analysis, regression
   - Check: Scatter plot with trendline

5. **H5**: Certain product categories are more popular in specific regions
   - Variables: Category, Region, Transaction Count
   - Test: Chi-square test
   - Check: Cross-tabulation pivot table

6. **H6**: Customer age is related to product category preference
   - Variables: Customer Age, Category
   - Test: ANOVA or Chi-square
   - Check: Pivot table with age groups × categories

7. **H7**: The relationship between quantity purchased and unit price is negative (bulk discounts)
   - Variables: Quantity, Unit Price
   - Test: Correlation, scatter plot
   - Check: Scatter plot with trendline

8. **H8**: Payment method preference differs by location (Online vs In-store)
   - Variables: Location, Payment Method
   - Test: Chi-square test
   - Check: Cross-tabulation

---

## 📝 Execution Checklist (Follow Question Order)

### ✅ Phase 1: Question 2a - Data Structure & Quality (COMPLETED)
- [x] Data validation sheets (Checks, Customer Checks)
- [x] Initial EDA with validation flags
- [x] Data cleaning and integration (Sales_Cleaned)
- [x] Numerical descriptive statistics (Stats sheet)

### ⏭️ Phase 2: Question 2b - Patterns, Trends & Relationships (CURRENT)
**Must Complete:**
- [ ] Task 2b.1: Create all 10 pivot tables (Pivots_Top10 and Pivots sheets)
- [ ] Task 2b.2: Generate 15 charts showing patterns and trends
- [ ] Task 2b.3: Add categorical descriptive statistics to Stats sheet
- [ ] Task 2b.4: Document 5-7 key patterns/insights in Insights sheet

**Professional Requirements:**
- [ ] Format all charts professionally (titles, labels, legends, consistent colors)
- [ ] Add data labels where appropriate
- [ ] Use conditional formatting for heatmaps

### 📋 Phase 3: Question 2c - Detect Outliers & Anomalies (NEXT)
- [ ] Task 2c.1: Calculate outlier bounds using IQR method in Stats sheet
- [ ] Task 2c.2: Create box plots to visualize outliers (Charts sheet)
- [ ] Task 2c.3: Document anomalies found in Insights sheet

### 📋 Phase 4: Question 2d - Generate Hypotheses (LAST)
- [ ] Task 2d.1: Create correlation matrix using Data Analysis Toolpak (Correlation sheet)
- [ ] Task 2d.2: Generate 6-8 testable hypotheses in Insights sheet
- [ ] Document suggested tests and expected outcomes

### 🎯 Final Polish (Nice to Have)
- [ ] Executive summary dashboard page
- [ ] Advanced conditional formatting
- [ ] Additional specialized visualizations
- [ ] Interactive slicers for pivot tables

---

## Excel Techniques to Use

### Data Analysis Toolpak
- **Descriptive Statistics**: Analyze > Data Analysis > Descriptive Statistics
- **Correlation**: Analyze > Data Analysis > Correlation
- **Histogram**: Analyze > Data Analysis > Histogram

### Pivot Tables
- Insert > PivotTable
- Use slicers for interactivity
- Apply value filters (Top 10, etc.)
- Show values as % of Total

### Charts
- Insert > Recommended Charts
- Use combo charts for multiple metrics
- Add trendlines to scatter plots
- Apply chart styles and color schemes

### Conditional Formatting
- Home > Conditional Formatting > Color Scales
- Data bars for quick visual comparison
- Icon sets for status indicators

### Formulas to Use
- `COUNTIF`, `COUNTIFS` for frequency tables
- `AVERAGEIF`, `AVERAGEIFS` for conditional averages
- `SUMIF`, `SUMIFS` for conditional sums
- `QUARTILE.INC`, `QUARTILE.EXC` for quartiles
- `CORREL` for correlation coefficients
- `UNIQUE` for distinct values (if Excel 365)
- `FILTER` for dynamic filtering (if Excel 365)

---

## Tips for Success

1. **Stay Organized**
   - Keep pivot tables on separate sheets
   - Group related charts together
   - Use clear, descriptive names

2. **Professional Formatting**
   - Consistent color scheme across all charts
   - Clear titles and axis labels
   - Data labels where appropriate
   - Legend positioning

3. **Focus on Insights**
   - Don't just create charts - interpret them
   - Document what each chart reveals
   - Look for patterns, trends, anomalies
   - Think about business implications

4. **Quality over Quantity**
   - Better to have 12 excellent charts than 20 mediocre ones
   - Each visualization should tell a story
   - Remove chart junk (unnecessary gridlines, 3D effects)

5. **Check Your Work**
   - Verify pivot table calculations
   - Cross-check statistics with manual calculations
   - Ensure charts display correctly
   - Proofread all labels and titles

---

## Next Steps After Excel Work

Once you complete the Excel EDA:

1. **PowerBI Dashboard** (Requirement)
   - Import cleaned data into PowerBI
   - Create interactive dashboard
   - Include key visualizations
   - Export as .pbix and .pdf

2. **Written Report** (Requirement)
   - Explain visualization choices
   - Document descriptive statistics used
   - Present patterns with evidence
   - List hypotheses for statistical testing
   - Describe data cleaning decisions

3. **Final Package**
   - Excel workbook with all EDA work
   - PowerBI .pbix file
   - PowerBI dashboard .pdf
   - Written report (self-sufficient)
   - Zip and submit

---

## Progress Tracking & Updates

**Last Updated**: October 27, 2025

### Update Log
This section will be automatically updated as you complete tasks or request assistance.

| Date | Activity | Status | Notes |
|------|----------|--------|-------|
| Oct 27, 2025 | Initial plan created | ✅ Complete | Created Excel EDA plan document |
| Oct 27, 2025 | Plan restructured | ✅ Complete | Aligned with Questions 2 & 3 from deliverable |
| Oct 27, 2025 | Sheet responsibilities mapped | ✅ Complete | Added sheet-to-question mapping table |
| Oct 27, 2025 | User clarification session | ✅ Complete | Confirmed Stats sheet complete, currently in Q2b |
| | | | |

---

### Active Assistance Triggers

I will automatically update this file when any of these occur:

1. **Progress Updates** - When you tell me you've completed items from the checklist
2. **Question Answers** - When I help you with Excel formulas, pivot tables, or chart creation
3. **Work Reviews** - When I review sections you've completed and provide feedback
4. **Formula Generation** - When I create specific Excel formulas for your calculations
5. **Documentation Updates** - When I help document your findings or insights

---

### Current Work Session

**Current Phase**: ⏭️ Question 2b - Identify Patterns, Trends & Relationships
**Status**: ✅ Stats sheet reviewed - ready for chart creation
**Completed**:
- Question 2a (Data Structure & Quality) including Stats sheet
- Stats sheet contains: numerical descriptive stats, correlation matrix, categorical analysis (Payment Method)
**Next Task**: Task 2b.2 - Create 4 priority charts
**Recommended Starting Point - QUICK WINS**:
1. ✅ **Chart 2: Top 10 Products Bar Chart** (data ready in Stats sheet rows 60-72!)
2. ✅ **Chart 4: Payment Method by Location** (data ready in Stats sheet rows 53-58!)
3. **Chart 1: Monthly Sales Trend** (need to create pivot first)
4. **Chart 3: Customer Age Histogram** (can create directly from Sales_Cleaned)

**Stats Sheet Notes**:
- ✅ Excellent foundation: numerical stats, correlation matrix (rows 61-70), categorical analysis
- 📝 Optional enhancement: Add Gender, Location, Category frequency tables when time permits
- 📝 For Q2c later: Add outlier bounds section (IQR method)

**DO NOT**:
- Re-do Stats sheet (already complete for Q2a)
- Skip ahead to Q2c or Q2d (follow sequential order)

---

### Quick Reference - Helper Formulas

This section will be populated with specific formulas as you work through the plan.

#### Frequency Tables
```excel
// Count: =COUNTIF(range, criteria)
// Percentage: =count/total*100
// Sum: =SUMIF(range, criteria, sum_range)
```

#### Outlier Detection
```excel
// Q1: =QUARTILE.INC(range, 1)
// Q3: =QUARTILE.INC(range, 3)
// IQR: =Q3-Q1
// Lower: =Q1-1.5*IQR
// Upper: =Q3+1.5*IQR
```

#### Correlation
```excel
// =CORREL(array1, array2)
```

*More formulas will be added as needed during your work session.*

---

**Good luck with your Excel EDA work!**

**Remember**: Let me know whenever you:
- Complete a task (so I can check it off)
- Get stuck on something (so I can help)
- Finish a section (so I can review it)
- Need a formula (so I can generate it)
- Want to document findings (so I can assist)
