# Question 3c: Correlation Analysis - Implementation Guide

**Course**: CP610 Deliverable #2
**Team**: Liam & Pham
**Date**: October 28, 2025
**Technique**: Statistical Correlation Analysis
**Time Estimate**: 15-20 minutes

---

## 📋 Overview

**What is Correlation Analysis?**
Correlation analysis measures the strength and direction of relationships between two numerical variables. The correlation coefficient (r) ranges from -1 to +1:
- **r = +1**: Perfect positive correlation (as X increases, Y increases)
- **r = 0**: No correlation
- **r = -1**: Perfect negative correlation (as X increases, Y decreases)

**Why Do This?**
- Satisfies **Question 3c requirement** (Correlation Analysis technique)
- Supports **Question 2d** (helps generate hypotheses)
- Identifies which variables are related to each other
- Provides evidence for patterns you found in Question 2b

---

## 🎯 What You'll Create

**Deliverable**: A correlation matrix showing all pairwise correlations between 9 numerical variables

**Location**: New sheet called **"Correlation"**

**What It Looks Like**:
```
                Quantity  Unit_Price  Unit_Cost  Discount_Rate  ...
Quantity           1.00        0.15      0.12          -0.23  ...
Unit_Price         0.15        1.00      0.95           0.08  ...
Unit_Cost          0.12        0.95      1.00           0.06  ...
Discount_Rate     -0.23        0.08      0.06           1.00  ...
...
```

---

## 📦 Prerequisites

### Required:
✅ Excel with **Data Analysis ToolPak** enabled
✅ Sales_Cleaned sheet with all 25,000 rows
✅ 9 numerical columns available

### Enable Data Analysis ToolPak (If Not Already):
1. **File** → **Options**
2. **Add-ins** (left sidebar)
3. At bottom: **Manage**: Excel Add-ins → **Go**
4. Check **Analysis ToolPak** → **OK**
5. Verify: **Data** tab should now show **Data Analysis** button (far right)

---

## 📝 Step-by-Step Implementation

### Step 1: Create New Sheet
1. Right-click on sheet tabs at bottom
2. **Insert** → **Worksheet**
3. Rename to: **Correlation**
4. This will be your correlation analysis sheet

### Step 2: Prepare Data Range in Sales_Cleaned

**Find Column Letters for These 9 Variables:**
Go to **Sales_Cleaned** sheet and locate these columns:
- Quantity
- Unit_Price (or Unit Price)
- Unit_Cost (or Unit Cost)
- Discount_Rate (or Discount Rate)
- Total_Recalc
- Gross_Profit_After_Discount
- Gross_Margin_% (or Gross_Margin_Percent)
- Customer_Age (or Customer Age)
- Tenure_Years (or Tenure)

**Important**: You need only the **DATA rows** (no headers), from Row 2 to Row 25,001

**Example**: If your columns are:
- E: Quantity
- F: Unit_Price
- G: Unit_Cost
- ... etc.

You'll select: **E2:M25001** (9 columns × 25,000 rows)

### Step 3: Run Correlation Analysis Tool

1. Click on **Correlation** sheet (stay here - don't go back to Sales_Cleaned)
2. **Data** tab → **Data Analysis** button (far right)
3. Scroll down and select **Correlation**
4. Click **OK**

### Step 4: Configure Correlation Tool

**Correlation Dialog Box Settings:**

1. **Input Range**:
   - Click the range selector icon (小箭头)
   - Go to **Sales_Cleaned** sheet
   - Select your 9 columns with DATA only (e.g., E2:M25001)
   - Press Enter
   - Box should show: `Sales_Cleaned!$E$2:$M$25001`

2. **Grouped By**:
   - Select **Columns** (default - should already be selected)

3. **Labels in First Row**:
   - **Do NOT check** this box (you selected data only, no headers)

4. **Output Range**:
   - Select **Output Range** (not New Worksheet)
   - Click in the box
   - Go to **Correlation** sheet
   - Click cell **A1**
   - This will place the correlation matrix starting at A1

5. Click **OK**

### Step 5: Wait for Calculation
- Excel will calculate 81 correlations (9 × 9 matrix)
- With 25,000 rows, this takes 10-30 seconds
- **DO NOT CLICK** anything while "Calculating..." shows in status bar

### Step 6: Add Variable Labels

The correlation matrix will appear, but without row/column labels. You need to add them manually:

**Add Column Headers (Row 1):**
1. Cell **B1**: Type `Quantity`
2. Cell **C1**: Type `Unit_Price`
3. Cell **D1**: Type `Unit_Cost`
4. Cell **E1**: Type `Discount_Rate`
5. Cell **F1**: Type `Total_Recalc`
6. Cell **G1**: Type `Gross_Profit`
7. Cell **H1**: Type `Gross_Margin_%`
8. Cell **I1**: Type `Customer_Age`
9. Cell **J1**: Type `Tenure_Years`

**Add Row Labels (Column A):**
1. Cell **A2**: Type `Quantity`
2. Cell **A3**: Type `Unit_Price`
3. Cell **A4**: Type `Unit_Cost`
4. Cell **A5**: Type `Discount_Rate`
5. Cell **A6**: Type `Total_Recalc`
6. Cell **A7**: Type `Gross_Profit`
7. Cell **A8**: Type `Gross_Margin_%`
8. Cell **A9**: Type `Customer_Age`
9. Cell **A10**: Type `Tenure_Years`

### Step 7: Format the Correlation Matrix

**Format Numbers:**
1. Select the correlation data (cells B2:J10 - the 9×9 grid of numbers)
2. Right-click → **Format Cells**
3. **Number** tab → **Number** category
4. Decimal places: **2**
5. Check: **Use 1000 Separator** (unchecked)
6. Click **OK**

**Bold Headers:**
1. Select Row 1 (B1:J1)
2. **Bold** (Ctrl+B / Cmd+B)
3. Select Column A (A2:A10)
4. **Bold**

### Step 8: Apply Conditional Formatting (The "Heat")

This makes correlations easy to see at a glance:

1. Select correlation data: **B2:J10**
2. **Home** tab → **Conditional Formatting**
3. **Color Scales** → **More Rules**
4. **Format Style**: Select **3-Color Scale**
5. Configure colors:
   - **Minimum**:
     - Type: Lowest Value
     - Color: Red
   - **Midpoint**:
     - Type: Number
     - Value: **0**
     - Color: White
   - **Maximum**:
     - Type: Highest Value
     - Color: Green
6. Click **OK**

**Result**:
- Strong positive correlations (close to +1) → Green
- No correlation (close to 0) → White
- Strong negative correlations (close to -1) → Red

### Step 9: Highlight Strong Correlations

**Add borders to emphasize strong relationships:**

1. Scan the matrix for correlations where |r| > 0.5
2. For each strong correlation:
   - Click on that cell
   - **Home** → **Font** group → **Border** dropdown
   - Select **Thick Box Border**

**Example strong correlations you might find**:
- Unit_Price & Unit_Cost (likely ~0.95 - very strong)
- Total_Recalc & Gross_Profit (likely ~0.90+)
- Quantity & Total_Recalc (might be ~0.40-0.60)

### Step 10: Add Interpretation Section

**Below the matrix (starting around Row 15), add findings:**

**Cell A15**: Type **"Key Findings:"** (Bold, 12pt)

**Cell A17**: Type **"Strong Positive Correlations (r > 0.5):"** (Bold)
**Cell A18**: List them:
```
• Unit_Price & Unit_Cost (r = 0.95) - Prices closely tied to costs
• Total_Recalc & Gross_Profit (r = 0.92) - Higher sales = higher profit
```

**Cell A21**: Type **"Strong Negative Correlations (r < -0.5):"** (Bold)
**Cell A22**: List any found (may be none)

**Cell A24**: Type **"Moderate Correlations (0.3 < |r| < 0.5):"** (Bold)
**Cell A25**: List them

**Cell A28**: Type **"Weak/No Correlations (|r| < 0.3):"** (Bold)
**Cell A29**: Note variables with little relationship

### Step 11: Add Title and Formatting

**Add Sheet Title:**
1. Select and merge cells A1:E1 (above your column headers)
2. Type: **"Correlation Analysis - Sales & Customer Variables"**
3. Format:
   - Font size: 16pt
   - Bold
   - Center alignment
   - Fill color: Light blue

**Adjust column widths:**
1. Select columns A through J
2. Double-click on column border (auto-fits)
3. OR manually set width to 14 for consistency

### Step 12: Verify and Check

**Quality Checks:**
- [ ] Diagonal is all 1.00 (variable correlated with itself = 1)
- [ ] Matrix is symmetric (top-right mirrors bottom-left)
- [ ] All values are between -1 and +1
- [ ] Color scale shows: Red (negative) → White (zero) → Green (positive)
- [ ] Strong correlations (|r| > 0.5) are highlighted
- [ ] Headers and row labels are clear and match variable names
- [ ] Findings section documents key correlations

---

## 🔍 How to Interpret Correlations

### Correlation Strength Guide:

| Correlation (r) | Strength | Interpretation |
|----------------|----------|----------------|
| 0.90 to 1.00 | Very Strong Positive | Variables move together almost perfectly |
| 0.70 to 0.89 | Strong Positive | Clear positive relationship |
| 0.40 to 0.69 | Moderate Positive | Noticeable positive relationship |
| 0.20 to 0.39 | Weak Positive | Slight positive relationship |
| -0.19 to 0.19 | Very Weak/None | Little to no linear relationship |
| -0.20 to -0.39 | Weak Negative | Slight negative relationship |
| -0.40 to -0.69 | Moderate Negative | Noticeable negative relationship |
| -0.70 to -0.89 | Strong Negative | Clear negative relationship |
| -0.90 to -1.00 | Very Strong Negative | Variables move opposite almost perfectly |

### What To Look For:

**Expected Strong Correlations** (confirm they exist):
- Unit_Price & Unit_Cost (should be very high ~0.90-0.99)
- Total_Recalc & Gross_Profit_After_Discount (should be high ~0.85-0.95)

**Interesting Correlations** (useful for hypotheses):
- Discount_Rate & Total_Recalc (do discounts increase purchase amounts?)
- Customer_Age & Total_Recalc (do older customers spend more?)
- Tenure_Years & Total_Recalc (do long-time customers spend more?)
- Quantity & Unit_Price (bulk discounts? - expect negative if present)

**Surprising Correlations** (worth investigating):
- Any unexpected strong correlations
- Variables you thought would correlate but don't

---

## ⚠️ Common Issues and Solutions

### Issue 1: "Data Analysis" button not visible
**Solution**: Data Analysis ToolPak not enabled. Go to File → Options → Add-ins → Enable it

### Issue 2: Correlation matrix has #N/A or errors
**Solution**:
- Check that you selected only numerical columns
- Verify no text values in the selected range
- Make sure you selected data rows only (no headers)

### Issue 3: Matrix is not symmetric
**Solution**: This indicates calculation error - delete and re-run the tool

### Issue 4: All correlations are exactly 0.00 or 1.00
**Solution**: You likely selected ranges with no variance or wrong data - check your input range

### Issue 5: Tool says "Input Range contains non-numeric data"
**Solution**:
- One of your 9 columns has text values
- Check for error values (#DIV/0!, #N/A, etc.) in Sales_Cleaned
- Filter columns to remove non-numeric rows

### Issue 6: Takes too long (over 2 minutes)
**Solution**:
- Normal with 25,000 rows
- If over 5 minutes, Excel may have frozen - restart and try again
- Consider using a sample (first 10,000 rows) to test

---

## 📊 Example: What Your Matrix Should Look Like

```
Correlation Analysis - Sales & Customer Variables

              Quantity  Unit_Price  Unit_Cost  Discount  Total_Recalc  Gross_Profit  Gross_Margin  Cust_Age  Tenure
Quantity          1.00        0.12       0.10     -0.18          0.45          0.40          0.05      0.08    0.12
Unit_Price        0.12        1.00       0.96      0.07          0.38          0.35          0.22     -0.03    0.05
Unit_Cost         0.10        0.96       1.00      0.06          0.32          0.28          0.15     -0.02    0.04
Discount_Rate    -0.18        0.07       0.06      1.00         -0.15         -0.22         -0.35      0.02   -0.01
Total_Recalc      0.45        0.38       0.32     -0.15          1.00          0.92          0.28      0.15    0.22
Gross_Profit      0.40        0.35       0.28     -0.22          0.92          1.00          0.68      0.14    0.20
Gross_Margin_%    0.05        0.22       0.15     -0.35          0.28          0.68          1.00      0.08    0.12
Customer_Age      0.08       -0.03      -0.02      0.02          0.15          0.14          0.08      1.00    0.55
Tenure_Years      0.12        0.05       0.04     -0.01          0.22          0.20          0.12      0.55    1.00

Key Findings:

Strong Positive Correlations (r > 0.5):
• Unit_Price & Unit_Cost (r = 0.96) - Prices closely follow costs
• Total_Recalc & Gross_Profit (r = 0.92) - Revenue drives profit
• Gross_Profit & Gross_Margin% (r = 0.68) - Higher profit margins on profitable items
• Customer_Age & Tenure (r = 0.55) - Older customers tend to have longer tenure

Moderate Positive Correlations (0.3 < r < 0.5):
• Quantity & Total_Recalc (r = 0.45) - Larger orders = higher revenue
• Unit_Price & Total_Recalc (r = 0.38) - Higher priced items increase revenue

Moderate Negative Correlations (r < -0.3):
• Discount_Rate & Gross_Margin% (r = -0.35) - Discounts reduce profit margins
```

---

## ✅ Completion Checklist

Use this checklist to ensure you've completed everything:

- [ ] Data Analysis ToolPak is enabled
- [ ] Created new "Correlation" sheet
- [ ] Located 9 numerical columns in Sales_Cleaned
- [ ] Selected correct data range (no headers, only 25,000 data rows)
- [ ] Ran Correlation tool successfully
- [ ] Added variable labels to row and column headers
- [ ] Formatted correlation values to 2 decimal places
- [ ] Applied 3-color conditional formatting (Red-White-Green)
- [ ] Verified diagonal is all 1.00
- [ ] Verified matrix is symmetric
- [ ] Highlighted strong correlations (|r| > 0.5) with borders
- [ ] Added "Key Findings" section below matrix
- [ ] Documented 3-5 strong correlations with interpretations
- [ ] Added title to sheet
- [ ] Adjusted column widths for readability
- [ ] Saved workbook

---

## 🎯 What Comes Next

After completing this correlation analysis, you'll use these findings to:

1. **Question 2d**: Generate hypotheses based on strong correlations
   - Example: "H1: There is a strong positive correlation between customer tenure and transaction value"
   - Example: "H2: Discount rate is negatively correlated with profit margin"

2. **Report Writing**: Cite these correlations as evidence
   - "Correlation analysis revealed a strong positive relationship (r = 0.92) between Total Revenue and Gross Profit..."

3. **Statistical Testing**: These correlations suggest which hypothesis tests to run
   - Strong correlations → Regression analysis
   - Moderate correlations → Further investigation needed

---

## 📚 Additional Resources

**Understanding Correlation:**
- Correlation ≠ Causation (just because variables correlate doesn't mean one causes the other)
- Correlation only measures linear relationships
- Outliers can heavily influence correlation coefficients

**Next Steps After Correlation:**
- Use strong correlations to formulate hypotheses (Question 2d)
- Create scatter plots for strongest correlations (visualization)
- Consider regression analysis for predictive relationships

---

**End of Question 3c Implementation Guide**

*Estimated completion time: 15-20 minutes*
*Proceed to Question 2d (Generate Hypotheses) once complete*
