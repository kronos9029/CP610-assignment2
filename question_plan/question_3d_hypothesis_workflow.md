# Question 3d: Hypothesis Workflow - Implementation Guide

**Course**: CP610 Deliverable #2
**Team**: Liam & Pham
**Date**: October 28, 2025
**Technique**: Hypothesis Formulation and Documentation
**Time Estimate**: 10-15 minutes

---

## 📋 Overview

**What is Hypothesis Workflow?**
The hypothesis workflow is the process of:
1. Observing patterns in data (from EDA)
2. Formulating testable statements about relationships
3. Specifying how to test those statements
4. Predicting expected outcomes

**Why Do This?**
- Satisfies **Question 3d requirement** (Hypothesis Workflow technique)
- Directly supports **Question 2d** (Generate hypotheses for further investigation)
- Bridges EDA (what you found) to Statistical Analysis (what to test next)
- Demonstrates scientific thinking and analytical rigor

**Key Principle**: Hypotheses should be:
- **Specific**: Clear about which variables are involved
- **Testable**: Can be tested with statistical methods
- **Based on Evidence**: Supported by your EDA findings
- **Measurable**: Involves quantifiable variables

---

## 🎯 What You'll Create

**Deliverable**: A structured table of 6-8 testable hypotheses

**Location**: **Insights** sheet (create if doesn't exist, or add section to existing)

**Table Structure**:
| # | Hypothesis Statement | Variables Involved | Suggested Statistical Test | Supporting Evidence | Expected Outcome |
|---|---------------------|-------------------|---------------------------|--------------------|--------------------|

---

## 📦 Prerequisites

Before writing hypotheses, you should have completed:
- ✅ **Question 2b**: Charts showing patterns, trends, relationships
- ✅ **Question 2c**: Outlier detection and anomaly identification
- ✅ **Question 3c**: Correlation analysis matrix
- ✅ **Question 3a**: Descriptive statistics (mean, median, std dev, etc.)

**Why?** Your hypotheses should be based on patterns you've already observed in the data, not random guesses.

---

## 📝 Step-by-Step Implementation

### Step 1: Create or Navigate to Insights Sheet

**Option A - Insights Sheet Doesn't Exist Yet:**
1. Right-click sheet tabs → **Insert** → **Worksheet**
2. Rename to: **Insights**
3. This will document all your findings

**Option B - Insights Sheet Already Exists:**
1. Click on **Insights** tab
2. Scroll to find empty space for hypothesis section
3. Suggest starting at Row 50 or below existing content

### Step 2: Create Hypothesis Table Structure

**Set up table starting at Row 1 (or Row 50 if Insights exists):**

**Row 1 - Title:**
- Merge cells A1:F1
- Type: **"Hypothesis Generation - Question 2d & 3d"**
- Format: Bold, 16pt, Center, Fill with light blue

**Row 3 - Subtitle:**
- Cell A3: Type: **"Testable Hypotheses for Statistical Analysis"**
- Format: Bold, 12pt

**Row 5 - Table Headers:**
Type these headers across the row:
- **A5**: `#` (Hypothesis number)
- **B5**: `Hypothesis Statement`
- **C5**: `Variables Involved`
- **D5**: `Suggested Statistical Test`
- **E5**: `Supporting Evidence (from EDA)`
- **F5**: `Expected Outcome`

**Format Headers:**
1. Select A5:F5
2. **Bold** them
3. **Background fill**: Light gray
4. **Border**: All borders, medium weight
5. **Text wrap**: Enable (Home → Alignment → Wrap Text)
6. Adjust row height: ~30

**Adjust Column Widths:**
- Column A: 5 (narrow)
- Column B: 45 (widest - for hypothesis statement)
- Column C: 20
- Column D: 20
- Column E: 30
- Column F: 20

### Step 3: Review Your EDA Findings

**Before writing hypotheses**, gather evidence from your completed work:

**From Question 2b (Charts & Patterns)**:
- Which product categories had highest revenue?
- Did any customer segments spend significantly more?
- Were there time-based trends (monthly, seasonal)?
- Online vs in-store differences?
- Payment method preferences?
- Age group spending patterns?

**From Question 3c (Correlation Matrix)**:
- Which variables had strong positive correlations (r > 0.5)?
- Which had strong negative correlations (r < -0.5)?
- Any surprising correlations?

**From Question 2c (Outliers)**:
- Were outliers concentrated in specific categories/regions?
- Did certain customer types have extreme behavior?

**From Question 3a (Descriptive Stats)**:
- Large differences in means between groups?
- High variability in certain variables?

### Step 4: Write 6-8 Hypotheses

Use the template below to create 6-8 hypotheses. Mix different types:
- 2-3 about **customer segments** (membership, age, tenure)
- 2-3 about **operations** (location, payment, category)
- 1-2 about **correlations** (relationships between numerical variables)
- 1 about **time trends** (seasonality, growth)

**Template for Each Hypothesis:**

**Row 6 (Hypothesis 1):**
- **A6**: `1`
- **B6**: `[Group A] has significantly [higher/lower] [metric] than [Group B]`
- **C6**: `[Independent Variable], [Dependent Variable]`
- **D6**: `[t-test / ANOVA / Chi-square / Regression]`
- **E6**: `[Chart #X shows..., Descriptive stats show..., Correlation r = ...]`
- **F6**: `[Group A] will have [higher/lower] [metric] (p < 0.05)`

Repeat for rows 7-13 (Hypotheses 2-8)

### Step 5: Example Hypotheses (Customize to Your Data)

Here are 8 example hypotheses. **Adapt these based on YOUR actual findings:**

---

**Hypothesis 1: Customer Segment Spending**
- **#**: 1
- **Statement**: Platinum members have significantly higher average transaction values than Standard members
- **Variables**: Membership_Level (categorical), Total_Recalc (numerical)
- **Test**: Independent samples t-test (or One-way ANOVA if comparing all membership levels)
- **Evidence**: Chart 7 shows Platinum avg = $XXX vs Standard avg = $YYY (50% higher). Descriptive stats: Platinum mean = $XXX (SD = $XX), Standard mean = $YYY (SD = $YY)
- **Expected**: Platinum will have statistically significantly higher mean transaction value (p < 0.05)

---

**Hypothesis 2: Location and Discounts**
- **#**: 2
- **Statement**: Online purchases receive higher discount rates than in-store purchases
- **Variables**: Location (categorical: Online/In-store), Discount_Rate (numerical)
- **Test**: Independent samples t-test
- **Evidence**: Descriptive stats show Online avg discount = X%, In-store avg = Y%. Chart 4 shows Online has more transactions, possibly due to promotional discounts
- **Expected**: Online discount rate will be significantly higher than in-store (p < 0.05)

---

**Hypothesis 3: Seasonal Sales Pattern**
- **#**: 3
- **Statement**: Sales exhibit seasonal patterns with significantly higher revenue in Q4 (October-December) compared to other quarters
- **Variables**: Month (categorical), Total_Recalc (numerical)
- **Test**: One-way ANOVA or time series decomposition
- **Evidence**: Chart 1 (Monthly Sales Trend) shows peak in November-December. Q4 average = $XXX vs Q1-Q3 average = $YYY
- **Expected**: Q4 sales will be significantly higher than Q1, Q2, Q3 (p < 0.05)

---

**Hypothesis 4: Tenure and Loyalty**
- **#**: 4
- **Statement**: Customer tenure is positively correlated with average transaction value
- **Variables**: Tenure_Years (numerical), Total_Recalc (numerical)
- **Test**: Pearson correlation coefficient, Simple linear regression
- **Evidence**: Correlation matrix shows r = 0.XX between Tenure and Total_Recalc. Longer-tenured customers may be more loyal and spend more
- **Expected**: Positive correlation (r > 0.3, p < 0.05); Regression: Transaction Value = β₀ + β₁(Tenure), β₁ > 0

---

**Hypothesis 5: Product Category and Region**
- **#**: 5
- **Statement**: Certain product categories are more popular in specific regions (association between Category and Region)
- **Variables**: Category (categorical), Region (categorical)
- **Test**: Chi-square test of independence
- **Evidence**: Chart 15 (Heatmap) shows Category X dominates Region Y, while Category Z dominates Region W. Suggests regional preferences
- **Expected**: Significant association between Category and Region (χ² test, p < 0.05)

---

**Hypothesis 6: Age and Category Preference**
- **#**: 6
- **Statement**: Customer age is related to product category preference, with younger customers (< 35) preferring Category A more than older customers (≥ 35)
- **Variables**: Customer_Age (numerical/categorical), Category (categorical)
- **Test**: Chi-square test (if age grouped) or Logistic regression
- **Evidence**: Descriptive analysis shows Category A has lower average customer age. Need to test if difference is significant
- **Expected**: Significant association; younger customers will show higher preference for Category A (p < 0.05)

---

**Hypothesis 7: Quantity and Price Relationship**
- **#**: 7
- **Statement**: There is a negative correlation between quantity purchased and unit price (evidence of bulk purchasing or bulk discounts)
- **Variables**: Quantity (numerical), Unit_Price (numerical)
- **Test**: Pearson correlation, Simple linear regression
- **Evidence**: Correlation matrix shows r = -0.XX (negative). Suggests customers buy more when prices are lower, or bulk orders get discounted
- **Expected**: Negative correlation (r < -0.2, p < 0.05); Regression slope β₁ < 0

---

**Hypothesis 8: Payment Method by Channel**
- **#**: 8
- **Statement**: Payment method preference differs significantly between Online and In-store purchases
- **Variables**: Location (categorical: Online/In-store), Payment_Method (categorical: Credit, Debit, Cash, PayPal)
- **Test**: Chi-square test of independence
- **Evidence**: Chart 5 shows Credit Card is most popular overall. In-store likely uses more Cash, Online uses more PayPal/Credit. Cross-tabulation needed to test
- **Expected**: Significant association; Online will favor Credit/PayPal, In-store will favor Cash (χ² test, p < 0.05)

---

### Step 6: Format the Table

**Apply Borders:**
1. Select entire table (A5:F13, including headers and all hypotheses)
2. **Home** → **Borders** → **All Borders**

**Text Wrapping:**
1. Select B6:F13 (all hypothesis data cells)
2. **Home** → **Alignment** → **Wrap Text**
3. Adjust row heights as needed (30-40 height per row)

**Alternate Row Shading (Optional):**
1. Select A6:F6, A8:F8, A10:F10, A12:F12 (even rows)
2. Fill with very light gray (makes table easier to read)

### Step 7: Add Explanatory Notes Below Table

**Below the table (e.g., Row 15):**

**Cell A15**: Type **"Notes on Hypothesis Testing:"** (Bold, 11pt)

**Cell A16**: Type these notes:
```
• All hypotheses are based on patterns observed during EDA (Questions 2a-2c)
• Statistical significance threshold: α = 0.05 (95% confidence level)
• Tests assume normal distribution and independence of observations (verify during analysis)
• For t-tests: Will check equal variances assumption using Levene's test
• For Chi-square: Will ensure expected frequencies > 5 in all cells
• Correlation coefficients: r > 0.3 = moderate, r > 0.5 = strong
• Further statistical analysis required to confirm these hypotheses
```

### Step 8: Add Connection to Other Work

**Cell A25**: Type **"Evidence Sources:"** (Bold, 11pt)

**Cell A26**: Type:
```
• Question 2b: Patterns identified in Charts 1-15
• Question 3a: Descriptive statistics (mean, median, SD) from Stats sheet
• Question 3c: Correlation matrix showing variable relationships
• Question 2c: Outlier analysis identifying extreme values
```

**Cell A32**: Type **"Next Steps:"** (Bold, 11pt)

**Cell A33**: Type:
```
1. Run statistical tests for each hypothesis using Data Analysis ToolPak or statistical software
2. Document results (test statistic, p-value, effect size) for each hypothesis
3. Accept or reject null hypothesis based on p < 0.05 threshold
4. Interpret business implications of results
5. Include in final report as evidence-based recommendations
```

### Step 9: Link Hypotheses to EDA Findings

**Add a second table showing evidence sources:**

**Row 40 - Title:**
- Type: **"Hypothesis Evidence Map"**
- Format: Bold, 14pt

**Row 42 - Table:**
| Hypothesis # | Supporting Chart(s) | Supporting Stats | Correlation Evidence |
|-------------|-------------------|------------------|---------------------|
| 1 | Chart 7 | Stats sheet: Membership stats | - |
| 2 | Chart 4 | Stats sheet: Location table | - |
| 3 | Chart 1, Chart 11 | Pivots: Monthly/Yearly aggregations | - |
| 4 | Chart 14 (if scatter) | Stats sheet: Tenure stats | Correlation: r = X.XX |
| 5 | Chart 15 (Heatmap), Chart 3 | Pivot: Category × Region | - |
| 6 | Chart 12, Chart 2 | Stats sheet: Age distribution | - |
| 7 | - | Stats sheet: Quantity, Price | Correlation: r = -X.XX |
| 8 | Chart 5 | Stats sheet: Payment Method table | - |

This table helps readers find the evidence for each hypothesis.

### Step 10: Quality Check

**Review each hypothesis:**
- [ ] Is it specific (names exact variables)?
- [ ] Is it testable (specifies a statistical test)?
- [ ] Is it based on evidence (cites charts/stats)?
- [ ] Is it measurable (uses quantifiable variables)?
- [ ] Does it predict an outcome?
- [ ] Is it realistic (based on actual data patterns)?

**Review overall set:**
- [ ] 6-8 hypotheses total
- [ ] Mix of hypothesis types (segments, correlations, associations, trends)
- [ ] All variables exist in your dataset
- [ ] Evidence clearly cited (Chart #, Stats sheet, Correlation)
- [ ] Statistical tests are appropriate for variable types
- [ ] Table is formatted professionally

---

## 📊 Hypothesis Types and Tests Reference

### Type 1: Comparing Group Means
**Example**: "Group A has higher average than Group B"
**Variables**: 1 categorical (groups), 1 numerical (metric)
**Tests**:
- 2 groups → Independent samples t-test
- 3+ groups → One-way ANOVA
**Evidence**: Bar charts, descriptive statistics (means, SDs)

### Type 2: Correlation Between Numbers
**Example**: "Variable X is correlated with Variable Y"
**Variables**: 2 numerical variables
**Tests**:
- Pearson correlation coefficient
- Simple linear regression
**Evidence**: Scatter plots, correlation matrix

### Type 3: Association Between Categories
**Example**: "Category A is associated with Category B"
**Variables**: 2 categorical variables
**Tests**:
- Chi-square test of independence
**Evidence**: Cross-tabulation pivot tables, heatmaps

### Type 4: Trend Over Time
**Example**: "Sales are increasing over time"
**Variables**: Time (ordered), Metric (numerical)
**Tests**:
- Time series analysis
- Linear regression with time as predictor
**Evidence**: Line charts, yearly comparisons

### Type 5: Proportion Differences
**Example**: "Proportion of A is higher in Group 1 than Group 2"
**Variables**: 1 categorical outcome, 1 categorical group
**Tests**:
- Two-proportion z-test
- Chi-square test
**Evidence**: Percentage comparisons, frequency tables

---

## ✅ Completion Checklist

- [ ] Created or navigated to Insights sheet
- [ ] Set up hypothesis table with 6 columns
- [ ] Wrote 6-8 specific, testable hypotheses
- [ ] Each hypothesis includes:
  - [ ] Clear statement
  - [ ] Variables identified
  - [ ] Appropriate statistical test specified
  - [ ] Supporting evidence cited (charts, stats, correlations)
  - [ ] Expected outcome predicted
- [ ] Formatted table with borders and text wrapping
- [ ] Added notes on hypothesis testing below table
- [ ] Created evidence map linking hypotheses to EDA findings
- [ ] Quality checked all hypotheses (specific, testable, evidence-based)
- [ ] Saved workbook

---

## 💡 Tips for Writing Good Hypotheses

### DO:
✅ Base hypotheses on patterns you've **actually observed** in your EDA
✅ Be **specific** about which variables and groups
✅ Use **quantifiable** terms (higher, lower, correlated, associated)
✅ Specify **direction** when possible (positive correlation, Group A > Group B)
✅ Cite **evidence** from your charts and statistics
✅ Match **test to variable types** (t-test for means, chi-square for categories, etc.)

### DON'T:
❌ Write vague hypotheses ("Something affects something")
❌ Hypothesize about variables not in your dataset
❌ Make hypotheses with no supporting evidence
❌ Use subjective terms ("better," "worse" without defining them)
❌ Suggest inappropriate tests (can't use t-test on categorical variable)
❌ Forget to predict expected outcomes

### Example of BAD vs GOOD Hypothesis:

**❌ BAD**: "There is a relationship between customers and sales"
- Too vague (which customers? which aspect of sales?)
- No specific variables
- No statistical test
- No evidence cited

**✅ GOOD**: "Platinum members have significantly higher average transaction values than Standard members"
- Specific groups (Platinum vs Standard)
- Clear variables (Membership_Level, Total_Recalc)
- Testable with t-test
- Based on Chart 7 and descriptive stats showing Platinum mean = $XXX vs Standard mean = $YYY

---

## 🎯 What Comes Next

After completing this hypothesis workflow:

1. **For Your Report** (Deliverable Requirement):
   - Include hypothesis table in your written report
   - Explain rationale for each hypothesis
   - Cite the EDA evidence that led to each hypothesis
   - This addresses questions.md line 23: "What hypotheses you think are worth investigating"

2. **For Future Statistical Analysis**:
   - These hypotheses become your testing agenda
   - Run the specified statistical tests
   - Document results (accept/reject, p-values, effect sizes)
   - Draw business conclusions

3. **Integration with Other Questions**:
   - Question 2d requirement: ✅ Complete (hypotheses generated)
   - Question 3d requirement: ✅ Complete (hypothesis workflow demonstrated)
   - Links to Question 2b: Uses patterns/trends as evidence
   - Links to Question 3c: Uses correlation findings as evidence

---

## 📚 Example: Complete Hypothesis Entry

Here's one complete example showing all required components:

| # | Hypothesis Statement | Variables Involved | Suggested Statistical Test | Supporting Evidence | Expected Outcome |
|---|---------------------|-------------------|---------------------------|--------------------|--------------------|
| 1 | Platinum members have significantly higher average transaction values than Standard members | **Independent Variable**: Membership_Level (categorical: Platinum, Gold, Silver, Bronze, Standard)<br>**Dependent Variable**: Total_Recalc (numerical, continuous, in $) | **Test**: One-way ANOVA (comparing 5 groups)<br>**Post-hoc**: Tukey HSD if significant<br>**Alternative**: Independent samples t-test (if comparing only Platinum vs Standard) | **Chart 7**: Shows Platinum avg transaction = $185 vs Standard avg = $95 (95% higher)<br>**Stats Sheet**: Platinum mean = $185.32 (SD = $45.20, n = 2,350), Standard mean = $95.18 (SD = $32.10, n = 8,200)<br>**Chart 6**: Shows Platinum is smallest segment (10% of customers) but may contribute disproportionate revenue | **Expected**: Platinum members will have statistically significantly higher mean transaction value than Standard members (p < 0.05). Effect size expected to be large (Cohen's d > 0.8). Business implication: Premium membership drives higher spending; should invest in Platinum retention programs. |

---

**End of Question 3d Implementation Guide**

*Estimated completion time: 10-15 minutes*
*Complete this AFTER Questions 2b, 2c, and 3c*
*This is the final step for Question 2 (EDA) and Question 3 (Techniques)*
