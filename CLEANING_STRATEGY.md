# Data Cleaning Strategy - CP610 Deliverable #2

**Project**: Sales & Customer Data Analysis
**Team**: Liam & Pham
**Last Updated**: October 24, 2025

---

## Table of Contents
1. [Overview](#overview)
2. [Data Quality Assessment Summary](#data-quality-assessment-summary)
3. [Customer Data Cleaning Strategy](#customer-data-cleaning-strategy)
4. [Sales Data Cleaning Strategy](#sales-data-cleaning-strategy)
5. [Cleaning Order & Dependencies](#cleaning-order--dependencies)
6. [Output Files](#output-files)
7. [Data Quality Metrics](#data-quality-metrics)

---

## Overview

This document outlines the comprehensive data cleaning strategy for the CP610 Deliverable #2 project. The cleaning process is designed to ensure data quality, consistency, and usability for subsequent analysis phases.

### Datasets
- **Customers_v4.csv**: Customer demographic and membership data (~1,000 customers)
- **Sales_v4.csv**: Transaction data (25,000 transactions)

### Cleaning Philosophy
- **Preserve data**: Minimize data loss through flagging rather than deletion
- **Transparency**: Document all issues and cleaning decisions
- **Auditability**: Maintain original values where possible
- **Consistency**: Ensure referential integrity between datasets

---

## Data Quality Assessment Summary

### Customer Data (Customers_v4.csv)
**Initial Assessment**:
- **Rows**: ~1,000 customers
- **Columns**: 9 (Customer ID, Customer Name, Gender, City, Province/State, Region, Membership Level, Customer Age, Tenure)
- **Key Issues Identified**:
  - ⚠️ Potential duplicate Customer IDs
  - ⚠️ Missing values (TBD - requires full scan)
  - ⚠️ Outlier ages or tenure values
  - ⚠️ Inconsistent categorical values
  - ⚠️ Text formatting issues (whitespace, capitalization)

**Quality Status**: ✅ Generally clean structure, requires validation

---

### Sales Data (Sales_v4.csv)
**Initial Assessment**:
- **Rows**: 25,000 transactions
- **Unique Transaction IDs**: 24,661 (indicating duplicates!)
- **Columns**: 13 (Transaction ID, Customer ID, Location, Payment Method, Category, Item, Quantity, Unit Price, Unit_Cost, Pre_Discount_Total, Discount_Rate, Total Spent, Date)

**Critical Issues Identified**:

#### 🚨 Issue #1: Duplicate Transaction IDs (CRITICAL)
- **Impact**: 339 duplicate Transaction IDs affecting 673 rows
- **Pattern**: 100% partial duplicates (same ID, completely different data)
- **Root Cause**: Transaction IDs are reused across different dates (daily counter reset pattern)
- **Evidence**:
  - Different Customer IDs for same Transaction ID
  - Different dates, items, amounts
  - Different locations and payment methods
  - Same Transaction ID appears on different dates
- **Business Insight**: Transaction IDs are unique **within a date**, not globally
- **Resolution**: **Create composite key using Transaction_ID + Date**

**Example**:
```
TXN_101364:
  Occurrence 1: CUST_0907, 2023-03-28, Cooking Oil Bottle, $50.44, Online
  Occurrence 2: CUST_0296, 2024-09-11, Cooking Oil Bottle, $23.28, In-store
  → Completely different transactions with same ID!
```

#### ⚠️ Issue #2: Future Dates
- **Date Range**: 2023-01-24 to 2025-08-20
- **Problem**: Dates beyond today (2025-10-24) exist in dataset
- **Impact**: Some transactions dated in future (2025-08-XX range)
- **Resolution**: Flag future dates for investigation, adjust if confirmed as errors

#### ⚠️ Issue #3: Referential Integrity
- **Issue**: Some Customer IDs in Sales may not exist in Customer table
- **Resolution**: Flag orphaned transactions, investigate with business

#### ⚠️ Issue #4: Mathematical Inconsistencies
- **Potential Issues**:
  - Pre_Discount_Total ≠ Quantity × Unit Price
  - Total Spent ≠ Pre_Discount_Total × (1 - Discount_Rate)
  - Negative values for quantities, prices, or costs
- **Resolution**: Recalculate derived fields, flag inconsistencies

**Quality Status**: ⚠️ Requires significant cleaning

---

## Customer Data Cleaning Strategy

### Script: `customer_cleaning.ipynb`

### Phase 1: Load & Initial Exploration
**Steps**:
1. Load `datasources/Customers_v4.csv`
2. Display basic info:
   - Shape (rows × columns)
   - Data types
   - Memory usage
3. Show first/last 10 rows
4. Generate summary statistics

**Code Pattern**:
```python
import pandas as pd
import numpy as np

df = pd.read_csv('../datasources/Customers_v4.csv')
print(f"Dataset shape: {df.shape}")
print(df.info())
print(df.head(10))
print(df.describe())
```

---

### Phase 2: Data Quality Assessment

#### 2.1 Missing Values Analysis
```python
# Check for missing values
missing = df.isnull().sum()
missing_pct = (df.isnull().sum() / len(df)) * 100
missing_summary = pd.DataFrame({
    'Missing_Count': missing,
    'Percentage': missing_pct
})
print(missing_summary[missing_summary['Missing_Count'] > 0])
```

**Resolution Rules**:
- **Customer ID**: Cannot be missing → Remove row if missing
- **Customer Name**: Cannot be missing → Remove row if missing
- **Gender**: If missing → Flag, consider "Unknown" category
- **Age/Tenure**: If missing → Use median imputation or flag for removal
- **Categorical fields**: If missing → Flag, consider "Unknown" category

---

#### 2.2 Duplicate Customer IDs
```python
# Check for duplicate Customer IDs
duplicates = df[df.duplicated(subset=['Customer ID'], keep=False)]
print(f"Duplicate Customer IDs: {duplicates['Customer ID'].nunique()}")
```

**Resolution**: Keep first occurrence, remove subsequent duplicates

---

#### 2.3 Data Validation Rules

**Customer Age**:
- **Valid Range**: 18-100 years
- **Action**: Flag ages outside range
```python
# Validate age
df['age_valid'] = df['Customer Age'].between(18, 100)
invalid_ages = df[~df['age_valid']]
```

**Tenure**:
- **Valid Range**: 0-50 years (reasonable customer lifetime)
- **Action**: Flag negative or excessive tenure
```python
# Validate tenure
df['tenure_valid'] = df['Tenure (Years)'].between(0, 50)
invalid_tenure = df[~df['tenure_valid']]
```

**Gender**:
- **Expected Values**: Male, Female (possibly Other/Unknown)
- **Action**: Standardize capitalization, flag unexpected values
```python
# Standardize gender
df['Gender'] = df['Gender'].str.strip().str.title()
unique_genders = df['Gender'].unique()
```

**Membership Level**:
- **Expected Values**: Standard, Gold, Platinum
- **Action**: Standardize capitalization, flag unexpected values
```python
# Standardize membership
df['Membership Level'] = df['Membership Level'].str.strip().str.title()
```

**Region**:
- **Expected Values**: West, Midwest, South, Northeast, Eastern Canada, Western Canada
- **Action**: Standardize, check for typos

---

### Phase 3: Data Cleaning Operations

#### 3.1 Remove Duplicates
```python
# Keep first occurrence of duplicate Customer IDs
df_clean = df.drop_duplicates(subset=['Customer ID'], keep='first')
print(f"Rows removed: {len(df) - len(df_clean)}")
```

#### 3.2 Handle Missing Values
```python
# Apply resolution rules based on assessment
# Example: Remove rows with missing Customer ID or Name
df_clean = df_clean.dropna(subset=['Customer ID', 'Customer Name'])

# Impute missing age with median
df_clean['Customer Age'].fillna(df_clean['Customer Age'].median(), inplace=True)
```

#### 3.3 Standardize Text Fields
```python
# Trim whitespace and standardize capitalization
text_columns = ['Customer Name', 'Gender', 'City', 'Province/State', 'Region', 'Membership Level']
for col in text_columns:
    df_clean[col] = df_clean[col].str.strip()
```

#### 3.4 Fix Invalid Values
```python
# Remove or flag invalid ages
df_clean = df_clean[df_clean['Customer Age'].between(18, 100)]

# Remove or flag invalid tenure
df_clean = df_clean[df_clean['Tenure (Years)'].between(0, 50)]
```

---

### Phase 4: Data Validation
```python
# Verify Customer ID uniqueness
assert df_clean['Customer ID'].is_unique, "Customer IDs not unique!"

# Check for remaining missing values
print(df_clean.isnull().sum())

# Validate data types
print(df_clean.dtypes)
```

---

### Phase 5: Export Cleaned Data
```python
# Create output directory if needed
import os
os.makedirs('../output_data', exist_ok=True)

# Export cleaned data
df_clean.to_csv('../output_data/Customers_cleaned.csv', index=False)
print(f"Cleaned data exported: {len(df_clean)} rows")
```

---

### Phase 6: Generate Data Quality Report
```python
# Create quality report
quality_report = {
    'Original_Rows': len(df),
    'Cleaned_Rows': len(df_clean),
    'Rows_Removed': len(df) - len(df_clean),
    'Duplicate_Customer_IDs': df.duplicated(subset=['Customer ID']).sum(),
    'Missing_Values_Original': df.isnull().sum().sum(),
    'Missing_Values_Cleaned': df_clean.isnull().sum().sum(),
    'Unique_Customers': df_clean['Customer ID'].nunique()
}

print("\n=== CUSTOMER DATA QUALITY REPORT ===")
for key, value in quality_report.items():
    print(f"{key}: {value}")
```

---

## Sales Data Cleaning Strategy

### Script: `sale_cleaning.ipynb`

### Phase 1: Load & Initial Exploration
```python
import pandas as pd
import numpy as np

df = pd.read_csv('../datasources/Sales_v4.csv')
print(f"Dataset shape: {df.shape}")
print(df.info())
print(df.head(10))
print(df.describe())
```

---

### Phase 2: Critical Issue Resolution

#### 2.1 🚨 Handle Duplicate Transaction IDs (COMPOSITE KEY APPROACH)

**Strategy**: Create composite primary key using Transaction_ID + Date

**Why This Works**:
- Analysis shows Transaction IDs are unique **within each date**
- Testing proves: Transaction_ID + Date = 100% uniqueness (25,000/25,000)
- Semantically correct: reflects business reality (daily transaction numbering)
- No artificial suffixes needed

**Implementation**:
```python
# Convert Date to datetime first
df['Date'] = pd.to_datetime(df['Date'])

# Store original Transaction ID for reference
df['Original_Transaction_ID'] = df['Transaction ID'].copy()

# Create date component (YYYYMMDD format)
df['Date_Component'] = df['Date'].dt.strftime('%Y%m%d')

# Create composite Transaction ID
df['Transaction_ID_Date'] = df['Transaction ID'] + '_' + df['Date_Component']

# Replace Transaction ID with composite key
df['Transaction ID'] = df['Transaction_ID_Date'].copy()

# Verify 100% uniqueness
assert df['Transaction ID'].is_unique, "Transaction IDs still not unique!"
print(f"✅ All Transaction IDs are now unique: {df['Transaction ID'].nunique()} unique IDs")
```

**Result**:
- Original: 24,661 unique IDs, 25,000 rows (339 duplicates)
- After: 25,000 unique IDs, 25,000 rows (100% unique)
- Preserved: All transaction data intact
- New format: `TXN_XXXXXX_YYYYMMDD` (e.g., `TXN_490235_20240125`)
- New columns: `Original_Transaction_ID`, `Date_Component`

**Benefits Over Suffix Approach**:
- ✅ Semantically meaningful (date is part of transaction identity)
- ✅ Reflects actual business process (daily transaction numbering)
- ✅ Easy to parse back to original ID and date
- ✅ No artificial _1, _2 suffixes
- ✅ Maintains chronological information in the ID itself

**Documentation for Report**:
```python
# Document duplicate resolution
dup_resolution_report = {
    'Total_Transactions': len(df),
    'Original_Unique_IDs': df['Original_Transaction_ID'].nunique(),
    'Duplicate_IDs_Found': len(df) - df['Original_Transaction_ID'].nunique(),
    'Resolution_Method': 'Transaction_ID + Date Composite Key',
    'Final_Unique_IDs': df['Transaction ID'].nunique(),
    'Uniqueness_Achieved': '100% (Natural Composite Key)'
}
print("\n=== DUPLICATE TRANSACTION ID RESOLUTION ===")
for key, value in dup_resolution_report.items():
    print(f"{key}: {value}")
```

---

#### 2.2 ⚠️ Handle Future Dates

```python
# Convert Date to datetime
df['Date'] = pd.to_datetime(df['Date'])

# Define "today" as reference point
TODAY = pd.Timestamp('2025-10-24')

# Flag future dates
df['has_future_date'] = df['Date'] > TODAY
future_dates_count = df['has_future_date'].sum()
print(f"Transactions with future dates: {future_dates_count}")

# Show future date transactions
print(df[df['has_future_date']][['Transaction ID', 'Date', 'Customer ID', 'Total Spent']])
```

**Resolution Options**:
1. **Flag only**: Keep for business investigation
2. **Adjust**: If pattern found (e.g., year error), correct systematically
3. **Remove**: If confirmed as data errors

**Recommended**: Flag only (preserve data for business decision)

---

#### 2.3 ⚠️ Validate Customer IDs (Referential Integrity)

```python
# Load cleaned customer data
customers = pd.read_csv('../output_data/Customers_cleaned.csv')
valid_customer_ids = customers['Customer ID'].unique()

# Check for orphaned transactions
df['has_invalid_customer'] = ~df['Customer ID'].isin(valid_customer_ids)
invalid_customer_count = df['has_invalid_customer'].sum()
print(f"Transactions with invalid Customer IDs: {invalid_customer_count}")

# Show orphaned transactions
if invalid_customer_count > 0:
    print(df[df['has_invalid_customer']][['Transaction ID', 'Customer ID', 'Date', 'Total Spent']])
```

**Resolution**: Flag for business investigation (customer may have been deleted)

---

#### 2.4 ⚠️ Validate Mathematical Consistency

**Check 1: Pre_Discount_Total = Quantity × Unit Price**
```python
# Calculate expected pre-discount total
df['Expected_Pre_Discount'] = df['Quantity'] * df['Unit Price']
df['Pre_Discount_Error'] = abs(df['Pre_Discount_Total'] - df['Expected_Pre_Discount']) > 0.01

pre_discount_errors = df['Pre_Discount_Error'].sum()
print(f"Pre-discount calculation errors: {pre_discount_errors}")
```

**Check 2: Total Spent = Pre_Discount_Total × (1 - Discount_Rate)**
```python
# Calculate expected total
df['Expected_Total'] = df['Pre_Discount_Total'] * (1 - df['Discount_Rate'])
df['Total_Error'] = abs(df['Total Spent'] - df['Expected_Total']) > 0.01

total_errors = df['Total_Error'].sum()
print(f"Total spent calculation errors: {total_errors}")
```

**Check 3: Negative Values**
```python
# Check for negative values
df['has_negative_qty'] = df['Quantity'] < 0
df['has_negative_price'] = df['Unit Price'] < 0
df['has_negative_cost'] = df['Unit_Cost'] < 0
df['has_negative_total'] = df['Total Spent'] < 0

print(f"Negative quantities: {df['has_negative_qty'].sum()}")
print(f"Negative prices: {df['has_negative_price'].sum()}")
print(f"Negative costs: {df['has_negative_cost'].sum()}")
print(f"Negative totals: {df['has_negative_total'].sum()}")
```

**Check 4: Invalid Discount Rates**
```python
# Check discount rate range
df['invalid_discount'] = ~df['Discount_Rate'].between(0, 1)
print(f"Invalid discount rates: {df['invalid_discount'].sum()}")
```

**Resolution**:
1. Recalculate derived fields if source data is correct
2. Flag inconsistencies for business review
3. Remove rows with critical errors (negative quantities, prices)

---

### Phase 3: Data Cleaning Operations

#### 3.1 Fix Mathematical Errors
```python
# Option 1: Recalculate Pre_Discount_Total (if Quantity and Unit Price are correct)
df.loc[df['Pre_Discount_Error'], 'Pre_Discount_Total'] = df['Expected_Pre_Discount']

# Option 2: Recalculate Total Spent (if Pre_Discount_Total and Discount_Rate are correct)
df.loc[df['Total_Error'], 'Total Spent'] = df['Expected_Total']

# Round to 2 decimal places
df['Pre_Discount_Total'] = df['Pre_Discount_Total'].round(2)
df['Total Spent'] = df['Total Spent'].round(2)
```

#### 3.2 Handle Missing Values
```python
# Check for missing values
missing = df.isnull().sum()
print(missing[missing > 0])

# Apply resolution rules
# Example: Remove rows with missing critical fields
df_clean = df.dropna(subset=['Transaction ID', 'Customer ID', 'Date', 'Total Spent'])
```

#### 3.3 Standardize Categorical Values
```python
# Standardize text fields
df_clean['Location'] = df_clean['Location'].str.strip().str.title()
df_clean['Payment Method'] = df_clean['Payment Method'].str.strip().str.title()
df_clean['Category'] = df_clean['Category'].str.strip().str.title()
df_clean['Item'] = df_clean['Item'].str.strip()
```

#### 3.4 Remove Invalid Transactions
```python
# Remove transactions with negative quantities or prices (if confirmed as errors)
df_clean = df_clean[df_clean['Quantity'] > 0]
df_clean = df_clean[df_clean['Unit Price'] > 0]
df_clean = df_clean[df_clean['Total Spent'] >= 0]
```

---

### Phase 4: Feature Engineering

#### 4.1 Extract Date Components
```python
# Extract date components for analysis
df_clean['Year'] = df_clean['Date'].dt.year
df_clean['Month'] = df_clean['Date'].dt.month
df_clean['Day'] = df_clean['Date'].dt.day
df_clean['Day_of_Week'] = df_clean['Date'].dt.dayofweek  # 0=Monday, 6=Sunday
df_clean['Day_Name'] = df_clean['Date'].dt.day_name()
df_clean['Quarter'] = df_clean['Date'].dt.quarter
df_clean['Week_of_Year'] = df_clean['Date'].dt.isocalendar().week
```

#### 4.2 Calculate Business Metrics
```python
# Calculate profit metrics
df_clean['Profit_Per_Unit'] = df_clean['Unit Price'] - df_clean['Unit_Cost']
df_clean['Total_Profit'] = df_clean['Profit_Per_Unit'] * df_clean['Quantity']
df_clean['Profit_Margin'] = (df_clean['Profit_Per_Unit'] / df_clean['Unit Price']) * 100

# Round to 2 decimal places
df_clean['Total_Profit'] = df_clean['Total_Profit'].round(2)
df_clean['Profit_Margin'] = df_clean['Profit_Margin'].round(2)
```

#### 4.3 Create Data Quality Summary Column
```python
# Create comprehensive data quality flag
def create_quality_flag(row):
    flags = []
    if row.get('has_future_date', False):
        flags.append('FUTURE_DATE')
    if row.get('has_invalid_customer', False):
        flags.append('INVALID_CUSTOMER')
    if row.get('has_suffix', False):
        flags.append('DUPLICATE_ID_RESOLVED')

    return '|'.join(flags) if flags else 'OK'

df_clean['data_quality_flag'] = df_clean.apply(create_quality_flag, axis=1)
```

---

### Phase 5: Data Validation
```python
# Final validation checks
print("\n=== FINAL VALIDATION ===")

# 1. Transaction ID uniqueness
assert df_clean['Transaction ID'].is_unique, "Transaction IDs not unique!"
print(f"✅ Transaction IDs unique: {df_clean['Transaction ID'].nunique()}")

# 2. No missing critical fields
critical_fields = ['Transaction ID', 'Customer ID', 'Date', 'Total Spent']
for field in critical_fields:
    assert df_clean[field].isnull().sum() == 0, f"Missing values in {field}!"
print(f"✅ No missing critical fields")

# 3. Valid data types
assert pd.api.types.is_datetime64_any_dtype(df_clean['Date']), "Date not datetime!"
print(f"✅ Date column is datetime type")

# 4. Positive values
assert (df_clean['Quantity'] > 0).all(), "Negative quantities found!"
assert (df_clean['Unit Price'] > 0).all(), "Negative prices found!"
assert (df_clean['Total Spent'] >= 0).all(), "Negative totals found!"
print(f"✅ All quantities, prices, and totals are positive")

# 5. Valid discount rates
assert df_clean['Discount_Rate'].between(0, 1).all(), "Invalid discount rates!"
print(f"✅ All discount rates between 0 and 1")
```

---

### Phase 6: Export Cleaned Data
```python
# Create output directory
import os
os.makedirs('../output_data', exist_ok=True)

# Export cleaned data
df_clean.to_csv('../output_data/Sales_cleaned.csv', index=False)
print(f"\n✅ Cleaned data exported: {len(df_clean)} transactions")
print(f"Output: output_data/Sales_cleaned.csv")
```

---

### Phase 7: Generate Comprehensive Data Quality Report
```python
# Create detailed quality report
quality_report = {
    'Dataset': 'Sales Data',
    'Original_Rows': len(df),
    'Cleaned_Rows': len(df_clean),
    'Rows_Removed': len(df) - len(df_clean),
    'Percentage_Retained': f"{(len(df_clean) / len(df) * 100):.2f}%",

    '---TRANSACTION_ID_ISSUES---': '',
    'Original_Unique_Transaction_IDs': df['Original_Transaction_ID'].nunique(),
    'Duplicate_Transaction_IDs_Found': df['Original_Transaction_ID'][df['has_suffix']].nunique(),
    'Rows_With_Regenerated_IDs': df['has_suffix'].sum(),
    'Final_Unique_Transaction_IDs': df_clean['Transaction ID'].nunique(),

    '---DATE_ISSUES---': '',
    'Transactions_With_Future_Dates': df['has_future_date'].sum(),
    'Date_Range': f"{df_clean['Date'].min()} to {df_clean['Date'].max()}",

    '---REFERENTIAL_INTEGRITY---': '',
    'Transactions_With_Invalid_Customer_IDs': df['has_invalid_customer'].sum(),

    '---MISSING_VALUES---': '',
    'Missing_Values_Original': df.isnull().sum().sum(),
    'Missing_Values_Cleaned': df_clean.isnull().sum().sum(),

    '---MATHEMATICAL_ERRORS---': '',
    'Pre_Discount_Calculation_Errors': df['Pre_Discount_Error'].sum(),
    'Total_Calculation_Errors': df['Total_Error'].sum(),

    '---VALUE_VALIDATION---': '',
    'Negative_Quantities_Found': df['has_negative_qty'].sum(),
    'Negative_Prices_Found': df['has_negative_price'].sum(),
    'Invalid_Discount_Rates': df['invalid_discount'].sum(),

    '---FINAL_DATASET---': '',
    'Total_Transactions': len(df_clean),
    'Unique_Customers': df_clean['Customer ID'].nunique(),
    'Date_Range_Clean': f"{df_clean['Date'].min()} to {df_clean['Date'].max()}",
    'Total_Revenue': f"${df_clean['Total Spent'].sum():,.2f}",
    'Average_Transaction_Value': f"${df_clean['Total Spent'].mean():.2f}"
}

# Print report
print("\n" + "="*60)
print("SALES DATA QUALITY REPORT")
print("="*60)
for key, value in quality_report.items():
    if key.startswith('---'):
        print(f"\n{value}")
    else:
        print(f"{key}: {value}")
print("="*60)

# Save report to file
with open('../output_data/Sales_Quality_Report.txt', 'w') as f:
    f.write("SALES DATA QUALITY REPORT\n")
    f.write("="*60 + "\n\n")
    for key, value in quality_report.items():
        if key.startswith('---'):
            f.write(f"\n{value}\n")
        else:
            f.write(f"{key}: {value}\n")
```

---

## Cleaning Order & Dependencies

### Sequence of Execution

1. **FIRST: Customer Data Cleaning**
   - Script: `customer_cleaning.ipynb`
   - Output: `output_data/Customers_cleaned.csv`
   - Reason: Sales data references Customer IDs (foreign key)

2. **SECOND: Sales Data Cleaning**
   - Script: `sale_cleaning.ipynb`
   - Input: `output_data/Customers_cleaned.csv` (for validation)
   - Output: `output_data/Sales_cleaned.csv`
   - Reason: Requires cleaned customer data for referential integrity checks

### Dependencies
```
datasources/Customers_v4.csv
         ↓
customer_cleaning.ipynb
         ↓
output_data/Customers_cleaned.csv
         ↓ (used for validation)
sale_cleaning.ipynb ← datasources/Sales_v4.csv
         ↓
output_data/Sales_cleaned.csv
```

---

## Output Files

### Cleaned Data Files
```
repo/
├── datasources/              # Original data (never modified)
│   ├── Customers_v4.csv
│   └── Sales_v4.csv
│
├── output_data/             # Cleaned data (created by scripts)
│   ├── Customers_cleaned.csv
│   ├── Sales_cleaned.csv
│   ├── Sales_Quality_Report.txt
│   └── Customer_Quality_Report.txt
│
└── cleaning/                 # Cleaning scripts
    ├── customer_cleaning.ipynb
    └── sale_cleaning.ipynb
```

### New Columns Added

**Sales_cleaned.csv** (additional columns):
- `Original_Transaction_ID`: Original Transaction ID before uniqueness fix
- `occurrence`: Occurrence number for duplicate Transaction IDs (1, 2, 3, etc.)
- `has_suffix`: Boolean - True if Transaction ID was modified
- `has_future_date`: Boolean - True if date is beyond today
- `has_invalid_customer`: Boolean - True if Customer ID not in customer table
- `Year`, `Month`, `Day`, `Quarter`, `Week_of_Year`: Date components
- `Day_of_Week`: 0=Monday, 6=Sunday
- `Day_Name`: Monday, Tuesday, etc.
- `Profit_Per_Unit`: Unit Price - Unit Cost
- `Total_Profit`: Profit per unit × Quantity
- `Profit_Margin`: (Profit per unit / Unit Price) × 100
- `data_quality_flag`: Summary of data quality issues (OK, FUTURE_DATE, etc.)

---

## Data Quality Metrics

### Key Performance Indicators (KPIs) for Data Quality

1. **Completeness**
   - Missing value percentage: Target < 1%
   - Critical field completeness: Target = 100%

2. **Uniqueness**
   - Customer ID uniqueness: Target = 100%
   - Transaction ID uniqueness: Target = 100% (after cleaning)

3. **Validity**
   - Age within valid range (18-100): Target = 100%
   - Discount rates within 0-1: Target = 100%
   - Positive quantities/prices: Target = 100%

4. **Consistency**
   - Mathematical accuracy: Target = 100%
   - Referential integrity: Target = 100%

5. **Accuracy**
   - Future dates: Target = 0%
   - Orphaned Customer IDs: Target = 0%

---

## Business Recommendations

### Critical Issues Requiring Business Action

1. **Transaction ID Generation System**
   - **Issue**: 334 Transaction IDs were reused for completely different transactions
   - **Impact**: Data integrity compromised, potential reporting errors
   - **Recommendation**:
     - Investigate Transaction ID generation mechanism
     - Implement unique constraint at source system
     - Audit historical data for similar issues

2. **Future Dates in Dataset**
   - **Issue**: Transactions dated beyond current date
   - **Impact**: Potential forecasting/reporting errors
   - **Recommendation**:
     - Investigate date entry/import process
     - Determine if systematic error (e.g., year typo)
     - Implement date validation at source

3. **Customer ID Integrity**
   - **Issue**: Potential orphaned transactions (Customer ID not in customer table)
   - **Impact**: Cannot link transactions to customer demographics
   - **Recommendation**:
     - Investigate missing customers
     - Determine if customers were deleted or data import issue
     - Implement foreign key constraints

---

## Assumptions & Limitations

### Assumptions
1. First occurrence of duplicate Customer ID is the correct record
2. First occurrence of duplicate Transaction ID is the "original" (for numbering)
3. Median imputation is appropriate for missing age values
4. Unit Price and Quantity are more reliable than calculated totals
5. Transactions with negative values are data errors (not returns)

### Limitations
1. Cannot determine root cause of Transaction ID duplication without source system access
2. Cannot confirm if future dates are legitimate future orders or data errors
3. Cannot recover deleted customer records
4. Business rules for data cleaning may require adjustment based on domain knowledge

---

## Next Steps After Cleaning

1. **Data Validation**
   - Review quality reports with stakeholders
   - Confirm cleaning decisions align with business requirements
   - Adjust cleaning rules if needed

2. **Exploratory Data Analysis (EDA)**
   - Proceed to Phase 2 of project plan
   - Analyze sales trends, customer behavior, etc.

3. **Documentation**
   - Update PROJECT_PLAN.md with cleaning results
   - Include cleaning metrics in final report
   - Document any business decisions made

4. **Version Control**
   - Commit cleaned data and scripts
   - Tag as "v1.0-cleaned-data"
   - Maintain original data in datasources/ folder

---

## Contact & Questions

**Project Team**: Liam & Pham
**Course**: CP610
**Deliverable**: #2

For questions about cleaning decisions or business rules, consult project documentation or course instructor.

---

*This cleaning strategy ensures high-quality, analysis-ready data while maintaining transparency and auditability of all cleaning decisions.*
