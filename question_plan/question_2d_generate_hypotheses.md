# Question 2d: Generate Hypotheses for Further Investigation

**Course**: CP610 Deliverable #2
**Team**: Liam & Pham
**Date**: October 28, 2025
**Requirement**: Generate hypotheses based on EDA findings
**Techniques Used**: Question 3c (Correlation Analysis) + Question 3d (Hypothesis Workflow)
**Time Estimate**: 25-35 minutes total

---

## 📋 Overview

**What is Question 2d?**
Question 2d asks you to **generate hypotheses for further investigation** based on all the patterns, trends, relationships, and anomalies you discovered during your Exploratory Data Analysis (Questions 2a, 2b, 2c).

**Why is This Important?**
- Bridges the gap between **EDA** (what you found) and **Statistical Analysis** (what to test next)
- Demonstrates critical thinking and analytical reasoning
- Shows you can formulate testable research questions from data patterns
- Required for final report (questions.md line 23: "What hypotheses you think are worth investigating")

**Key Principle**: Good hypotheses are:
1. **Evidence-Based**: Supported by patterns you observed in EDA
2. **Testable**: Can be tested with statistical methods
3. **Specific**: Clear about variables and expected relationships
4. **Actionable**: Lead to business insights if confirmed

---

## 🎯 What You'll Deliver

**Question 2d requires TWO techniques from Question 3:**

### **1. Question 3c: Correlation Analysis** (15-20 min)
- **What**: Create correlation matrix showing relationships between 9 numerical variables
- **Where**: New sheet called "Correlation"
- **Output**: 9×9 correlation matrix with color formatting

### **2. Question 3d: Hypothesis Workflow** (10-15 min)
- **What**: Write 6-8 testable hypotheses based on EDA findings
- **Where**: "Insights" sheet
- **Output**: Structured table of hypotheses with evidence and tests

**Together, these satisfy Question 2d's requirement to generate hypotheses for further investigation.**

---

## 📦 Prerequisites

Before starting Question 2d, you must have completed:

✅ **Question 2a**: Data structure and quality assessment (DONE)
✅ **Question 2b**: Identified patterns, trends, and relationships (charts created)
✅ **Question 2c**: Detected outliers and anomalies (outlier analysis done)
✅ **Question 3a**: Descriptive statistics (Stats sheet complete)
✅ **Question 3b**: Visualization (Charts created)

**Why?** You need the evidence from these questions to formulate your hypotheses.

---

## 📝 Two-Part Implementation

### **PART 1: Correlation Analysis (Question 3c)** ⏱️ 15-20 minutes

This provides evidence for numerical relationships.

**See detailed guide**: `question_3c_correlation_analysis.md`

**Quick Steps:**
1. Create new sheet: **Correlation**
2. Enable Data Analysis ToolPak (if not enabled)
3. Select 9 numerical columns from Sales_Cleaned (Quantity, Unit_Price, Unit_Cost, Discount_Rate, Total_Recalc, Gross_Profit_After_Discount, Gross_Margin_%, Customer_Age, Tenure_Years)
4. **Data** → **Data Analysis** → **Correlation**
5. Output to Correlation sheet starting at A1
6. Add variable labels (row and column headers)
7. Format as 2 decimals
8. Apply 3-color conditional formatting (Red-White-Green)
9. Highlight strong correlations (|r| > 0.5)
10. Document key findings below matrix

**Output Example:**
```
Correlation Matrix:
                Quantity  Unit_Price  Unit_Cost  Discount  Total_Recalc  ...
Quantity           1.00        0.12       0.10     -0.18          0.45  ...
Unit_Price         0.12        1.00       0.96      0.07          0.38  ...
Unit_Cost          0.10        0.96       1.00      0.06          0.32  ...
Discount_Rate     -0.18        0.07       0.06      1.00         -0.15  ...
Total_Recalc       0.45        0.38       0.32     -0.15          1.00  ...

Key Findings:
• Strong positive: Unit_Price & Unit_Cost (r = 0.96)
• Strong positive: Total_Recalc & Gross_Profit (r = 0.92)
• Moderate positive: Quantity & Total_Recalc (r = 0.45)
```

---

### **PART 2: Generate Hypotheses (Question 3d)** ⏱️ 10-15 minutes

This formulates testable statements based on all EDA evidence.

**See detailed guide**: `question_3d_hypothesis_workflow.md`

**Quick Steps:**
1. Create or navigate to **Insights** sheet
2. Set up hypothesis table with 6 columns:
   - #, Hypothesis Statement, Variables Involved, Suggested Test, Supporting Evidence, Expected Outcome
3. Review ALL your EDA findings:
   - Charts (Question 2b) - what patterns did you see?
   - Outliers (Question 2c) - any concentrated in specific groups?
   - Correlation matrix (Question 3c) - strong relationships?
   - Descriptive stats (Question 3a) - large differences in means?
4. Write 6-8 hypotheses covering:
   - 2-3 about customer segments (membership, age, tenure)
   - 2-3 about operations (location, payment, category, region)
   - 1-2 about correlations (numerical relationships)
   - 1 about time trends (seasonality)
5. Format table professionally (borders, wrap text, shading)
6. Add notes section explaining testing approach
7. Create evidence map linking hypotheses to EDA sources

**Output Example:**

| # | Hypothesis Statement | Variables | Test | Evidence | Expected Outcome |
|---|---------------------|-----------|------|----------|------------------|
| 1 | Platinum members have significantly higher average transaction values than Standard members | Membership_Level, Total_Recalc | t-test or ANOVA | Chart 7: Platinum avg = $185 vs Standard = $95. Stats: Platinum mean = $185 (SD=$45), Standard mean = $95 (SD=$32) | Platinum mean significantly higher (p < 0.05) |
| 2 | Online purchases receive higher discount rates than in-store | Location, Discount_Rate | t-test | Stats: Online avg discount = X%, In-store = Y%. Chart 4 shows channel differences | Online discount significantly higher (p < 0.05) |
| 3 | Sales exhibit seasonal patterns with Q4 peak | Month, Total_Recalc | ANOVA, Time series | Chart 1: Nov-Dec peak. Q4 avg = $XXX vs other quarters = $YYY | Q4 significantly higher (p < 0.05) |
| ... | ... | ... | ... | ... | ... |

---

## 🔄 Workflow: How These Parts Connect

### Step 1: Complete Question 3c (Correlation)
- Run correlation analysis
- Identify strong correlations (|r| > 0.5)
- Note surprising correlations

**Example Finding**: "Unit_Price & Unit_Cost have very strong positive correlation (r = 0.96)"

### Step 2: Review ALL EDA Evidence
- **From 2b (Charts)**: What patterns did you see?
  - Chart 7: Platinum members spend more
  - Chart 1: November-December sales peak
  - Chart 3: Regional differences in sales
  - Chart 12: Customer age distribution skewed younger

- **From 2c (Outliers)**: Where are outliers concentrated?
  - High-value transactions mostly from Platinum members
  - Outlier quantities in specific product categories

- **From 3c (Correlation)**: What relationships exist?
  - Strong: Unit_Price & Unit_Cost (r = 0.96)
  - Moderate: Quantity & Total_Recalc (r = 0.45)
  - Weak negative: Discount_Rate & Gross_Margin (r = -0.35)

- **From 3a (Stats)**: What are the numbers?
  - Platinum: mean transaction = $185, SD = $45
  - Standard: mean transaction = $95, SD = $32
  - Online: 60% of transactions
  - Q4: 35% of annual revenue

### Step 3: Formulate Hypotheses (Question 3d)
Use evidence from Step 2 to write testable hypotheses.

**Example**: Based on Chart 7 + Descriptive Stats showing Platinum mean = $185 vs Standard = $95, write hypothesis:
- **H1**: "Platinum members have significantly higher average transaction values than Standard members"
- **Test**: Independent samples t-test
- **Evidence**: Chart 7, Stats sheet means
- **Expected**: Platinum mean > Standard mean, p < 0.05

### Step 4: Document in Insights Sheet
Create structured table with all hypotheses and their evidence sources.

---

## 📊 Hypothesis Categories to Cover

Make sure your 6-8 hypotheses cover different aspects of the data:

### Category 1: Customer Segmentation (2-3 hypotheses)
**Variables**: Membership Level, Customer Age, Tenure
**Examples**:
- Platinum vs Standard spending
- Age groups and category preferences
- Tenure correlation with transaction value

### Category 2: Operations & Channels (2-3 hypotheses)
**Variables**: Location (Online/In-store), Payment Method, Region, Category
**Examples**:
- Online vs in-store discount rates
- Payment method preferences by channel
- Product category and regional associations
- Category performance differences

### Category 3: Numerical Relationships (1-2 hypotheses)
**Variables**: Quantity, Unit_Price, Discount_Rate, Total_Recalc, Gross_Margin_%
**Examples**:
- Quantity and price relationship (bulk discounts?)
- Discount rate impact on profit margins
- Tenure correlation with spending

### Category 4: Time Trends (1 hypothesis)
**Variables**: Month, Quarter, Year, Total_Recalc
**Examples**:
- Seasonal sales patterns (Q4 peak)
- Year-over-year growth trend
- Monthly variability

---

## ✅ Completion Checklist

### Part 1: Correlation Analysis (Question 3c)
- [ ] Created "Correlation" sheet
- [ ] Data Analysis ToolPak enabled
- [ ] Selected 9 numerical columns from Sales_Cleaned
- [ ] Ran Correlation tool successfully
- [ ] Added row and column labels (variable names)
- [ ] Formatted correlations to 2 decimal places
- [ ] Applied 3-color conditional formatting (Red-White-Green)
- [ ] Highlighted strong correlations (|r| > 0.5)
- [ ] Verified diagonal is 1.00 and matrix is symmetric
- [ ] Documented key findings below matrix (3-5 bullet points)

### Part 2: Hypothesis Generation (Question 3d)
- [ ] Created or navigated to "Insights" sheet
- [ ] Set up hypothesis table with 6 columns
- [ ] Reviewed all EDA findings (2b, 2c, 3a, 3c)
- [ ] Wrote 6-8 testable hypotheses:
  - [ ] 2-3 about customer segments
  - [ ] 2-3 about operations/channels
  - [ ] 1-2 about numerical relationships
  - [ ] 1 about time trends
- [ ] Each hypothesis includes:
  - [ ] Specific statement
  - [ ] Variables identified
  - [ ] Appropriate statistical test
  - [ ] Supporting evidence cited (Chart #, Stats, Correlation)
  - [ ] Expected outcome predicted
- [ ] Formatted table professionally (borders, wrap text)
- [ ] Added notes section below table
- [ ] Created evidence map linking hypotheses to sources

### Integration Check
- [ ] Hypotheses reference correlation findings
- [ ] Hypotheses cite chart numbers from Question 2b
- [ ] Hypotheses mention outlier patterns from Question 2c
- [ ] Hypotheses use descriptive stats from Question 3a
- [ ] All evidence sources are documented
- [ ] Saved workbook

---

## 📝 Example: Complete Hypothesis Development Process

Let's trace one hypothesis from EDA finding to final formulation:

### Step 1: Observe Pattern (Question 2b)
**Chart 7**: Average Transaction Value by Membership Level
- Shows: Platinum = $185, Gold = $145, Silver = $115, Bronze = $102, Standard = $95
- Pattern: Clear increasing trend with membership tier

### Step 2: Check Statistics (Question 3a)
**Stats Sheet**: Descriptive stats for Platinum and Standard
- Platinum: mean = $185.32, SD = $45.20, n = 2,350
- Standard: mean = $95.18, SD = $32.10, n = 8,200
- Difference: $90.14 (95% higher!)

### Step 3: Check for Confounding Variables (Question 3c)
**Correlation Matrix**: Is membership correlated with other factors?
- Membership not directly in correlation matrix (categorical)
- But can check if customer age or tenure might explain spending differences
- Customer_Age & Total_Recalc: r = 0.15 (weak) - age not main driver
- Tenure & Total_Recalc: r = 0.22 (weak) - tenure not main driver
- Conclusion: Membership itself likely drives spending difference

### Step 4: Formulate Hypothesis
| # | Hypothesis Statement | Variables | Test | Evidence | Expected Outcome |
|---|---------------------|-----------|------|----------|------------------|
| 1 | Platinum members have significantly higher average transaction values than Standard members | **Independent Variable**: Membership_Level (categorical: Platinum, Gold, Silver, Bronze, Standard)<br>**Dependent Variable**: Total_Recalc (numerical) | **Primary Test**: One-way ANOVA (comparing all 5 levels)<br>**Post-hoc**: Tukey HSD<br>**Simpler Alternative**: Independent samples t-test (Platinum vs Standard only) | **Chart 7**: Platinum avg = $185, Standard avg = $95 (95% difference)<br>**Stats Sheet**: Platinum mean = $185.32 (SD = $45.20, n = 2,350), Standard mean = $95.18 (SD = $32.10, n = 8,200)<br>**Chart 6**: Shows distribution of membership levels | **Expected**: Platinum members will have statistically significantly higher mean transaction value than Standard members (p < 0.05). Large effect size anticipated (Cohen's d > 0.8). **Business Implication**: Premium membership strongly drives higher spending; invest in Platinum member retention and encourage upgrades from Standard to higher tiers. |

---

## 🎯 Quality Standards

Your hypotheses will be evaluated on:

### Specificity ✅
- ❌ BAD: "Customers are different"
- ✅ GOOD: "Platinum members have significantly higher average transaction values ($185) than Standard members ($95)"

### Testability ✅
- ❌ BAD: "Sales are good in some regions"
- ✅ GOOD: "Region North has significantly higher average sales than Region South (testable with t-test)"

### Evidence-Based ✅
- ❌ BAD: No evidence cited
- ✅ GOOD: Cites Chart 7, Stats sheet means and SDs, sample sizes

### Measurability ✅
- ❌ BAD: "Better" or "worse" (subjective)
- ✅ GOOD: "Higher average transaction value" (quantifiable with dollars)

### Appropriate Test ✅
- ❌ BAD: Suggests t-test for categorical outcome
- ✅ GOOD: t-test for comparing means, Chi-square for categorical associations, Correlation for numerical relationships

---

## ⚠️ Common Mistakes to Avoid

### Mistake 1: Hypotheses Not Based on Your Data
❌ Writing generic hypotheses (like examples online) without checking if pattern exists in YOUR data
✅ Only write hypotheses for patterns YOU actually observed in YOUR charts/stats

### Mistake 2: Vague Statements
❌ "There is a relationship between variables"
✅ "Variable X is positively correlated with Variable Y (r > 0.3, p < 0.05)"

### Mistake 3: Wrong Statistical Test
❌ Using t-test to compare 5 groups (should be ANOVA)
❌ Using correlation for categorical variables (should be Chi-square)
✅ Match test to variable types (see reference table in guides)

### Mistake 4: No Evidence Cited
❌ Just stating hypothesis with no supporting evidence
✅ Every hypothesis cites specific charts, stats, or correlations

### Mistake 5: Not Predicting Outcome
❌ Stopping at "we will test if groups differ"
✅ "Group A is expected to have higher mean than Group B (p < 0.05)"

---

## 📚 Deliverable Requirements Mapping

This section addresses multiple deliverable requirements:

**From questions.md:**

**Line 7**: "2d. Generate hypotheses for further investigation"
- ✅ Satisfied by creating Insights sheet with 6-8 hypotheses

**Line 12**: "3c. Correlation Analysis"
- ✅ Satisfied by creating Correlation sheet with correlation matrix

**Line 13**: "3d. Hypothesis Workflow"
- ✅ Satisfied by documenting hypothesis generation process in structured table

**Line 23**: "What hypotheses you think are worth investigating during the Statistical Analysis step"
- ✅ Report will include hypothesis table showing which hypotheses warrant further testing
- ✅ Each hypothesis specifies the statistical test needed

---

## 🔄 Integration with Report Writing

When writing your final report, use this structure:

### Report Section: "Hypotheses Generated (Question 2d)"

**Introduction Paragraph**:
"Based on exploratory data analysis of 25,000 sales transactions and 1,000 customers, we identified several patterns worth further statistical investigation. Using correlation analysis (Question 3c technique) and hypothesis workflow methodology (Question 3d technique), we formulated eight testable hypotheses. These hypotheses address customer segmentation patterns, operational differences, time trends, and numerical relationships observed during EDA."

**Subsection 1: Correlation Analysis Results**:
"Correlation analysis of nine numerical variables revealed several significant relationships. The strongest positive correlation was between Unit_Price and Unit_Cost (r = 0.96, p < 0.001), indicating prices closely track underlying costs. A moderate positive correlation exists between Quantity and Total_Recalc (r = 0.45, p < 0.001), suggesting larger orders generate higher revenue. Notably, Discount_Rate shows a negative correlation with Gross_Margin_% (r = -0.35, p < 0.01), implying discounts reduce profitability."

**Subsection 2: Formulated Hypotheses**:
Present your hypothesis table, then explain each briefly:

"**Hypothesis 1 (Customer Segmentation)**: Based on Chart 7 and descriptive statistics, we hypothesize that Platinum members have significantly higher average transaction values ($185.32 ± $45.20) compared to Standard members ($95.18 ± $32.10). This will be tested using an independent samples t-test or one-way ANOVA. If confirmed, this suggests premium membership programs successfully drive higher spending behavior..."

[Continue for each hypothesis]

**Subsection 3: Justification**:
"These eight hypotheses were selected based on: (1) strong visual patterns in charts, (2) large effect sizes in descriptive statistics, (3) significant correlations, and (4) business relevance. Each hypothesis is testable with appropriate statistical methods and would provide actionable insights if confirmed."

---

## 🎯 Success Criteria

You've successfully completed Question 2d if:

✅ **Correlation sheet exists** with proper 9×9 matrix, color formatting, key findings documented

✅ **Insights sheet exists** with hypothesis table containing 6-8 well-formulated hypotheses

✅ **All hypotheses are**:
- Specific (clear variables and groups)
- Testable (appropriate statistical test identified)
- Evidence-based (cites charts, stats, correlations)
- Measurable (uses quantifiable terms)
- Diverse (covers segments, operations, correlations, trends)

✅ **Evidence is traceable**: Can find the chart/stat/correlation referenced for each hypothesis

✅ **Professional formatting**: Tables are formatted with borders, headers, appropriate column widths

✅ **Integration is clear**: Hypotheses clearly flow from EDA findings (2a, 2b, 2c, 3a, 3c)

---

## ⏭️ What Comes Next

### Immediate Next Steps:
1. **Complete PowerBI Dashboard** (Question 4 from questions.md)
2. **Write Final Report** explaining all your work
3. **Package Deliverables** (Excel workbook, PowerBI file, PDF, Report)

### If You Were to Continue with Statistical Testing:
1. Run the specified tests for each hypothesis
2. Document results (test statistic, p-value, effect size, confidence intervals)
3. Accept or reject null hypothesis for each
4. Interpret business implications
5. Make recommendations based on confirmed hypotheses

### For Your Report:
- Include hypothesis table in "Question 2d" section
- Explain how each hypothesis was derived from EDA
- Cite specific evidence sources (Chart numbers, Stats sheet, Correlation results)
- Discuss why these hypotheses are worth investigating
- Explain expected business value if hypotheses are confirmed

---

**End of Question 2d Implementation Guide**

*Total Time: 25-35 minutes (15-20 for 3c + 10-15 for 3d)*
*Complete AFTER Questions 2a, 2b, 2c, 3a, 3b*
*This is the final analytical step before PowerBI dashboard and report writing*

---

## 📁 Related Files

- **Detailed Guide for Part 1**: `question_3c_correlation_analysis.md`
- **Detailed Guide for Part 2**: `question_3d_hypothesis_workflow.md`
- **Chart Creation Guide**: `../chart_implementation_details.md`
- **Overall Project Plan**: `../project_excel_plan.md`
