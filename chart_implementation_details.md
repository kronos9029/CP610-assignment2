# Chart Implementation Details - Step-by-Step Guide

**Project**: CP610 Deliverable #2 - Sales & Customer Analysis
**Team**: Liam & Pham
**Date**: October 28, 2025

---

## 📋 Overview

This document provides detailed, step-by-step instructions for creating all 15 charts in the Excel workbook. Each chart includes:
- Data source location
- Complete creation steps
- Formatting requirements
- Time estimate
- Tips and common issues

---

## Chart 1: Monthly Sales Trend (Line Chart)

**Type**: Line Chart with Markers
**Purpose**: Show sales trends over time (Question 2b - Trends)
**Time Estimate**: 8-10 minutes
**Priority**: Medium
**Status**: ❌ Missing

### Prerequisites:
- ⚠️ **IMPORTANT**: Date field issue must be fixed first
- Need to create helper column for Month-Year
- Need to create Pivot Table for monthly aggregation

### Step 1: Fix Date Format Issue (MUST DO FIRST)
**Problem**: Date column in Sales_Cleaned is stored as text, preventing pivot grouping

**Solution - Add Helper Column:**
1. Go to **Sales_Cleaned** sheet
2. Click on column header after last column (Column AF or AG)
3. Type header: `Month_Year`
4. In cell below header (Row 2): `=TEXT(D2,"mmm-yyyy")`
   - Replace `D2` with your actual Date column reference
5. Press Enter
6. Double-click fill handle to copy formula down all 25,000 rows
7. Result: Shows "Jan-2023", "Feb-2023", etc.

### Step 2: Create Pivot Table for Monthly Data
1. Click anywhere in Sales_Cleaned table
2. **Insert** tab → **PivotTable**
3. Settings:
   - Table/Range: Sales_Cleaned (should auto-select)
   - New Worksheet: Select this option
   - Click **OK**
4. Rename new sheet to: **Pivot_Monthly**

### Step 3: Configure Pivot Table
**Drag fields to areas:**
- **Rows**: Month_Year (the helper column you created)
- **Values**: Total_Recalc (will show as "Sum of Total_Recalc")

**Sort chronologically:**
1. Click dropdown arrow on "Row Labels"
2. **More Sort Options**
3. Select **Ascending (A to Z)**
4. Click **OK**

### Step 4: Create Line Chart
1. Click anywhere in the pivot table
2. **Insert** tab → **Charts** group → **Line** → **Line with Markers**
3. Chart will appear on pivot sheet

### Step 5: Move Chart to Charts Sheet
1. Click on chart border to select entire chart
2. **Cut** (Ctrl+X or Cmd+X)
3. Go to **Charts** sheet
4. Click cell where you want chart (suggest **A5**)
5. **Paste** (Ctrl+V or Cmd+V)

### Step 6: Format Chart
**Chart Title:**
1. Click chart title
2. Type: `Monthly Sales Trend (2023-2025)`

**Axis Titles:**
1. **Chart Design** tab → **Add Chart Element** → **Axis Titles**
2. **Primary Horizontal**: Click and type `Month-Year`
3. **Primary Vertical**: Click and type `Total Revenue ($)`

**Format Y-Axis as Currency:**
1. Right-click Y-axis numbers
2. **Format Axis**
3. **Number** section → **Category**: Currency
4. Decimal places: 0
5. Symbol: $ (or your currency)

**Chart Style:**
1. **Chart Design** tab → **Chart Styles**
2. Choose a clean, professional style (recommend Style 3 or 8)

**Markers:**
- Should already have markers from chart type selection
- If not: **Chart Design** → **Change Chart Type** → **Line with Markers**

### Step 7: Final Touches
1. Resize chart: Drag corners to make width = 10 columns, height = 25 rows
2. Add gridlines: **Chart Design** → **Add Chart Element** → **Gridlines** → **Primary Major Horizontal**
3. Legend: **Chart Design** → **Add Chart Element** → **Legend** → **None** (not needed for single series)

### Verification Checklist:
- [ ] Chart shows monthly data points chronologically
- [ ] Line has visible markers at each data point
- [ ] Y-axis formatted as currency
- [ ] Chart title is descriptive
- [ ] Axes are labeled
- [ ] No legend (since only one data series)

---

## Chart 2: Top 10 Products by Revenue (Horizontal Bar Chart)

**Type**: Horizontal Bar Chart
**Purpose**: Show product performance (Question 2b - Patterns)
**Time Estimate**: 5 minutes
**Priority**: ⭐ HIGH (Data ready in Stats sheet!)
**Status**: ❌ Missing

### Prerequisites:
✅ Data already prepared in **Stats** sheet, rows 60-72

### Step 1: Locate Data Source
1. Go to **Stats** sheet
2. Find "Top 10 Items by Revenue" section (should be around Row 60)
3. Data structure:
   - Column C: Item names
   - Column D: Revenue values

### Step 2: Select Data
1. Click on cell C60 (or wherever "Item" header is)
2. Drag to select range: **C60:D71** (header + 10 items + total row)
3. **IMPORTANT**: Do NOT include the "Total" row in your selection
4. Correct selection: **C60:D70** (header + 10 items only)

### Step 3: Insert Bar Chart
1. With data selected, go to **Insert** tab
2. **Charts** group → **Bar Chart** icon (horizontal bars)
3. Select: **Clustered Bar** (first option)
4. Chart appears on Stats sheet

### Step 4: Move Chart to Charts Sheet
1. Click chart border to select entire chart
2. **Cut** (Ctrl+X or Cmd+X)
3. Go to **Charts** sheet
4. Click cell where you want chart (suggest **A35** - below Chart 1)
5. **Paste** (Ctrl+V or Cmd+V)

### Step 5: Format Chart
**Chart Title:**
1. Click chart title
2. Type: `Top 10 Products by Revenue`

**Axis Titles:**
1. **Chart Design** → **Add Chart Element** → **Axis Titles**
2. **Primary Horizontal**: Type `Total Revenue ($)`
3. **Primary Vertical**: Type `Product`

**Sort Bars (Descending - Highest at Top):**
1. Right-click on Y-axis (product names)
2. **Format Axis**
3. Check box: **Categories in reverse order**
4. Close format pane

**Format X-Axis as Currency:**
1. Right-click X-axis numbers (revenue values)
2. **Format Axis**
3. **Number** → **Category**: Currency
4. Decimal places: 0
5. Symbol: $

**Add Data Labels:**
1. Click on any bar
2. **Chart Design** → **Add Chart Element** → **Data Labels** → **Outside End**
3. Right-click on data labels → **Format Data Labels**
4. Check: **Value**
5. Number format: Currency, 0 decimals

**Remove Legend:**
1. Click legend box
2. Press **Delete** (not needed for single series)

### Step 6: Color and Style
1. Click on any bar to select all bars
2. **Format Data Series** (right-click → Format Data Series)
3. **Fill**: Choose solid color (suggest blue or green)
4. **Border**: No line
5. **Gap Width**: Set to 50% for better spacing

### Step 7: Final Adjustments
1. Resize chart: Width = 8 columns, Height = 25 rows
2. Ensure all product names are fully visible (expand chart if needed)

### Verification Checklist:
- [ ] 10 bars displayed (not 11 - Total row excluded)
- [ ] Bars sorted with highest revenue at top
- [ ] X-axis shows currency format
- [ ] Data labels show dollar amounts
- [ ] All product names fully visible
- [ ] No legend displayed

---

## Chart 3: Sales by Region (Pie Chart)

**Type**: Pie Chart with Percentage Labels
**Purpose**: Show geographic revenue distribution (Question 2b - Patterns)
**Time Estimate**: 6-8 minutes
**Priority**: Medium
**Status**: ❌ Missing

### Prerequisites:
- Need to create pivot table first
- Region field must exist in Sales_Cleaned

### Step 1: Create Pivot Table
1. Go to **Sales_Cleaned** sheet
2. Click anywhere in the table
3. **Insert** → **PivotTable**
4. Settings:
   - New Worksheet
   - Click **OK**
5. Rename sheet to: **Pivot_Region**

### Step 2: Configure Pivot Table
**Drag fields:**
- **Rows**: Region
- **Values**: Total_Recalc (Sum)

**Result**: Should show 3-5 regions with revenue totals

### Step 3: Insert Pie Chart
1. Click anywhere in pivot table
2. **Insert** tab → **Charts** → **Pie** → **Pie** (first option, not 3D)

### Step 4: Move to Charts Sheet
1. Cut chart (Ctrl+X / Cmd+X)
2. Go to **Charts** sheet
3. Paste at cell **K5** (next to Chart 1)

### Step 5: Format Chart
**Chart Title:**
- Type: `Revenue Distribution by Region`

**Data Labels - Show Percentages:**
1. **Chart Design** → **Add Chart Element** → **Data Labels** → **More Data Label Options**
2. Check boxes:
   - ✅ **Category Name** (region names)
   - ✅ **Percentage**
   - ❌ **Value** (uncheck)
   - ✅ **Leader Lines** (check)
3. **Separator**: New Line
4. **Label Position**: Best Fit
5. **Number Format**: Percentage, 1 decimal place

**Legend:**
1. **Chart Design** → **Add Chart Element** → **Legend** → **Right**
2. OR remove legend if data labels include category names

**Colors:**
1. **Chart Design** → **Change Colors**
2. Choose a colorful palette (Colorful Palette 2 or 3)

### Step 6: Enhance Appearance
**Pull Out Largest Slice:**
1. Click on chart once (selects entire chart)
2. Click again on the largest slice only (selects single slice)
3. Drag slice slightly outward to emphasize
4. Distance: ~10% of radius

**Format Slices:**
1. Click on chart area
2. **Format Data Series** (right-click)
3. **Border**: White, 2pt width (separates slices clearly)

### Step 7: Final Touches
1. Resize chart: Make it square (10 columns × 20 rows)
2. Ensure all labels are readable and not overlapping

### Verification Checklist:
- [ ] All regions displayed
- [ ] Percentages sum to 100%
- [ ] Labels show region names AND percentages
- [ ] Largest slice slightly pulled out
- [ ] Clean borders between slices
- [ ] Professional color scheme

---

## Chart 4: Online vs In-Store Sales (Column Chart)

**Type**: Clustered Column Chart
**Purpose**: Compare sales channels (Question 2b - Patterns)
**Time Estimate**: 3 minutes
**Priority**: ⭐ HIGH (Data ready in Stats sheet!)
**Status**: ❌ Missing

### Prerequisites:
✅ Data already in **Stats** sheet (Location Distribution table)

### Step 1: Locate Data
1. Go to **Stats** sheet
2. Find "Location Distribution" table (around Row 65-69)
3. Data structure:
   - Column C: Location (Online, In-store)
   - Column D: Count
   - Column E: % of Total

### Step 2: Select Data for Chart
**Option A - Use Count values:**
1. Select range: **C66:D68** (Location header, Online, In-store)
2. Do NOT include Total row

**Option B - Use Revenue (if available):**
- If you have revenue by location, use that instead for more meaningful comparison

### Step 3: Insert Column Chart
1. With data selected: **Insert** tab
2. **Charts** → **Column** → **Clustered Column** (first option)
3. Chart appears on Stats sheet

### Step 4: Move to Charts Sheet
1. Cut chart (Ctrl+X / Cmd+X)
2. Go to **Charts** sheet
3. Paste at cell **K35** (below Chart 3)

### Step 5: Format Chart
**Chart Title:**
- Type: `Sales Comparison: Online vs In-Store`

**Axis Titles:**
1. **Chart Design** → **Add Chart Element** → **Axis Titles**
2. **Primary Vertical**: Type `Number of Transactions` (or `Revenue ($)` if using revenue)
3. **Primary Horizontal**: Not needed (already says Online/In-store)

**Add Data Labels:**
1. Click any column
2. **Chart Design** → **Add Chart Element** → **Data Labels** → **Outside End**
3. Format labels:
   - Font size: 12pt
   - Bold
   - Number format: Number with comma separator (e.g., 12,345)

**Format Columns:**
1. Click on columns to select series
2. **Format Data Series** → **Fill**
3. Online: Blue color
4. In-store: Green color
5. **Gap Width**: 150% (makes columns wider)

**Remove Legend:**
- Click legend and press Delete (labels on X-axis make it redundant)

### Step 6: Color Code for Clarity
**If you want to keep legend:**
1. Keep legend on right
2. Match colors: Online (Blue), In-store (Green)

**Y-Axis Formatting:**
- If using transaction counts: Format as Number with comma
- If using revenue: Format as Currency ($)

### Step 7: Final Adjustments
1. Resize: Width = 8 columns, Height = 20 rows
2. Add gridlines: **Chart Design** → **Add Chart Element** → **Gridlines** → **Primary Major Horizontal**

### Verification Checklist:
- [ ] Two columns displayed (Online and In-store)
- [ ] Data labels showing exact values
- [ ] Columns are distinct colors
- [ ] Y-axis properly formatted
- [ ] Chart title is clear
- [ ] Gridlines for easy reading

---

## Chart 5: Payment Method Distribution (Horizontal Bar Chart)

**Type**: Horizontal Bar Chart with Percentages
**Purpose**: Show payment preference patterns (Question 2b - Patterns)
**Time Estimate**: 5 minutes
**Priority**: ⭐ HIGH (Data ready in Stats sheet!)
**Status**: ❌ Missing

### Prerequisites:
✅ Data already prepared in **Stats** sheet, rows 53-58

### Step 1: Locate Data
1. Go to **Stats** sheet
2. Find "Payment Method" table (around Row 53-58)
3. Data structure:
   - Column C: Payment methods (Credit Card, Debit Card, Cash, PayPal)
   - Column D: Count
   - Column E: % of Total

### Step 2: Select Data
**Select columns for chart:**
1. Select: **C54:C57** (payment method names only, no header, no Total)
2. Hold **Ctrl** (Windows) or **Cmd** (Mac)
3. Also select: **E54:E57** (percentage column only)
4. Now you have: Payment names + Percentages selected (non-adjacent ranges)

**Why percentages?**: More meaningful than raw counts for showing preferences

### Step 3: Insert Bar Chart
1. With data selected: **Insert** tab
2. **Charts** → **Bar** → **Clustered Bar**
3. Chart appears on Stats sheet

### Step 4: Move to Charts Sheet
1. Cut chart (Ctrl+X / Cmd+X)
2. Go to **Charts** sheet
3. Paste at cell **A65** (below Chart 2)

### Step 5: Format Chart
**Chart Title:**
- Type: `Transaction Count by Payment Method`

**Axis Titles:**
1. **Chart Design** → **Add Chart Element** → **Axis Titles**
2. **Primary Horizontal**: Type `Percentage of Transactions (%)`
3. **Primary Vertical**: Type `Payment Method`

**Sort Bars (Descending):**
1. Right-click Y-axis (payment methods)
2. **Format Axis**
3. Check: **Categories in reverse order**
4. Bars now show highest at top

**Format X-Axis as Percentage:**
1. Right-click X-axis numbers
2. **Format Axis**
3. **Number** → **Category**: Percentage
4. Decimal places: 1
5. Close pane

**Add Data Labels:**
1. Click bars to select series
2. **Chart Design** → **Add Chart Element** → **Data Labels** → **Outside End**
3. Right-click labels → **Format Data Labels**
4. **Number** → Percentage, 1 decimal
5. Font: Bold, 11pt

**Color Bars Consistently:**
1. Click on bars
2. **Format Data Series**
3. **Fill**: Gradient or solid color (suggest teal or purple)
4. **Gap Width**: 80%

**Remove Legend:**
- Click and delete (not needed)

### Step 6: Add Insight Annotation (Optional)
**If one method dominates (>40%):**
1. **Chart Design** → **Add Chart Element** → **Text Box**
2. Type: "Most popular: [method name]"
3. Position near highest bar

### Step 7: Final Touches
1. Resize: Width = 8 columns, Height = 20 rows
2. Ensure all payment method names fully visible

### Verification Checklist:
- [ ] 4 bars displayed (Credit Card, Debit Card, Cash, PayPal)
- [ ] Sorted with highest percentage at top
- [ ] X-axis shows percentages (not counts)
- [ ] Data labels show percentage values
- [ ] Bars are uniform color
- [ ] All labels readable

---

## Chart 6: Customer Distribution by Membership Level (Column Chart)

**Type**: Column Chart with Data Labels
**Purpose**: Show customer segments (Question 2b - Patterns)
**Time Estimate**: 6-8 minutes
**Priority**: Medium
**Status**: ❌ Missing

### Prerequisites:
- Need to create pivot table first
- Membership Level field must exist in Sales_Cleaned

### Step 1: Create Pivot Table
1. Go to **Sales_Cleaned** sheet
2. **Insert** → **PivotTable** → New Worksheet
3. Rename sheet: **Pivot_Membership**

### Step 2: Configure Pivot Table
**Important**: We want UNIQUE customers, not transaction count

**Method - Count Unique Customers:**
1. **Rows**: Membership_Level
2. **Values**: Customer_ID
3. Click dropdown on "Sum of Customer_ID" in Values area
4. **Value Field Settings**
5. **Summarize Values By**: Select **Count**
6. Click **OK**
7. This gives count of transactions per membership level

**Note**: Excel pivot tables count rows, not unique values. If you need unique customer count, you might need to use distinct count (requires data model) or accept transaction count as proxy.

### Step 3: Sort Data
1. Click dropdown in "Row Labels"
2. **Sort** → **More Sort Options**
3. **Descending** by Count
4. Highest membership level shows first

### Step 4: Insert Column Chart
1. Click anywhere in pivot table
2. **Insert** → **Column Chart** → **Clustered Column**

### Step 5: Move to Charts Sheet
1. Cut chart (Ctrl+X / Cmd+X)
2. Go to **Charts** sheet
3. Paste at cell **K65** (next to Chart 5)

### Step 6: Format Chart
**Chart Title:**
- Type: `Customer Distribution by Membership Level`

**Axis Titles:**
1. **Chart Design** → **Add Chart Element** → **Axis Titles**
2. **Primary Vertical**: Type `Number of Customers` (or `Number of Transactions`)
3. **Primary Horizontal**: Delete or leave blank (membership levels already labeled)

**Add Data Labels:**
1. Click columns
2. **Chart Design** → **Add Chart Element** → **Data Labels** → **Outside End**
3. Format: Number with comma, Bold, 11pt

**Color Columns by Level (Optional Enhancement):**
1. Click on each column individually (single click on chart, then click specific column)
2. **Format Data Point**
3. Assign colors:
   - Platinum: Gold/Yellow
   - Gold: Orange
   - Silver: Gray
   - Bronze: Brown
   - Standard/Basic: Blue

**Remove Legend:**
- Delete if columns are color-coded by name

### Step 7: Final Formatting
1. **Gap Width**: 100% (moderate spacing)
2. Add gridlines for readability
3. Resize: Width = 8 columns, Height = 20 rows

### Verification Checklist:
- [ ] All membership levels shown
- [ ] Bars sorted by size (largest first)
- [ ] Data labels show counts
- [ ] Y-axis formatted with commas
- [ ] Meaningful colors (optional)
- [ ] Chart title clear

---

## Chart 7: Average Transaction Value by Membership Level (Column Chart)

**Type**: Column Chart with Currency Labels
**Purpose**: Show spending patterns by customer tier (Question 2b - Relationships)
**Time Estimate**: 6-8 minutes
**Priority**: Medium
**Status**: ❌ Missing

### Prerequisites:
- Can use same Pivot_Membership sheet from Chart 6
- Or create new pivot

### Step 1: Create or Modify Pivot Table
**Option A - Add to existing Pivot_Membership:**
1. Go to **Pivot_Membership** sheet
2. In PivotTable Fields, click **Values** dropdown
3. Add: Total_Recalc (drag to Values area)
4. Click dropdown on "Sum of Total_Recalc"
5. **Value Field Settings**
6. **Summarize Values By**: Select **Average**
7. **Number Format**: Currency, 0 decimals
8. Now you have: Count AND Average in same pivot

**Option B - Create separate pivot:**
1. New pivot table → New sheet → Rename **Pivot_Membership_Avg**
2. **Rows**: Membership_Level
3. **Values**: Total_Recalc → Change to **Average**

### Step 2: Select Data for Chart
**If using Option A (pivot with both metrics):**
1. Select only: Membership_Level names + Average Total_Recalc column
2. Use Ctrl/Cmd to select non-adjacent ranges

**If using Option B:**
1. Select entire pivot table

### Step 3: Insert Column Chart
1. **Insert** → **Column Chart** → **Clustered Column**

### Step 4: Move to Charts Sheet
1. Cut chart
2. Go to **Charts** sheet
3. Paste at cell **A95** (below Chart 4)

### Step 5: Format Chart
**Chart Title:**
- Type: `Average Transaction Value by Membership Level`

**Axis Titles:**
1. **Primary Vertical**: `Average Transaction Value ($)`
2. **Primary Horizontal**: Can remove (already labeled)

**Format Y-Axis as Currency:**
1. Right-click Y-axis
2. **Format Axis** → **Number** → Currency
3. Decimal places: 0
4. Symbol: $

**Add Data Labels:**
1. Click columns
2. **Chart Design** → **Add Chart Element** → **Data Labels** → **Outside End**
3. Format labels as Currency: $X,XXX

**Color Columns (Match Chart 6):**
- Use same color scheme as Chart 6 for consistency:
  - Platinum: Gold
  - Gold: Orange
  - Silver: Gray
  - Bronze: Brown
  - Standard: Blue

**Sort by Average (Descending):**
- Right-click X-axis → **Format Axis** → **Categories in reverse order**
- OR leave in membership level order (Platinum → Standard)

### Step 6: Add Trendline (Optional)
**If membership levels are ordinal (Platinum > Gold > Silver...):**
1. Right-click on columns
2. **Add Trendline**
3. Select **Linear**
4. Shows if higher tiers spend more

### Step 7: Final Touches
1. Gridlines: Add horizontal major gridlines
2. Resize: Width = 8 columns, Height = 20 rows
3. Gap width: 100%

### Verification Checklist:
- [ ] Columns show average (not sum or count)
- [ ] Y-axis formatted as currency
- [ ] Data labels show dollar amounts
- [ ] Colors match Chart 6 for consistency
- [ ] Chart title specifies "Average"
- [ ] Easy to compare membership tiers

---

## Chart 8: Quantity Distribution (Histogram)

**Type**: Histogram
**Purpose**: Show distribution of quantities ordered (Question 2c - Outliers)
**Time Estimate**: 7-9 minutes
**Priority**: Low
**Status**: ❌ Missing

### Prerequisites:
- Direct data from Sales_Cleaned[Quantity] column
- Excel 2016+ (has built-in Histogram chart)

### Method 1: Using Built-in Histogram (Recommended)

### Step 1: Select Data
1. Go to **Sales_Cleaned** sheet
2. Click on Quantity column header (selects entire column)
3. OR select range with data only (avoid header): e.g., click first Quantity value, Ctrl+Shift+End

### Step 2: Insert Histogram
1. **Insert** tab → **Charts** group
2. Click **Insert Statistic Chart** icon (looks like histogram)
3. Select **Histogram** (first option)
4. Chart appears on Sales_Cleaned sheet

### Step 3: Move to Charts Sheet
1. Cut chart (Ctrl+X / Cmd+X)
2. Go to **Charts** sheet
3. Paste at cell **K95** (next to Chart 7)

### Step 4: Configure Bins
**Automatic bins (easiest):**
- Excel chooses bin width automatically
- Usually works well for most data

**Manual bins (more control):**
1. Right-click on horizontal axis (quantity values)
2. **Format Axis**
3. **Axis Options** → **Bins**
4. Select **Bin width**
5. Enter: **2** (groups quantities in increments of 2)
   - OR enter **5** for wider bins
6. Adjust until histogram looks informative (not too many, not too few bars)

**Alternative - Number of bins:**
1. **Bins** → Select **Number of bins**
2. Enter: **10** bins
3. Excel calculates bin width automatically

### Step 5: Format Chart
**Chart Title:**
- Type: `Distribution of Quantity per Transaction`

**Axis Titles:**
1. **Chart Design** → **Add Chart Element** → **Axis Titles**
2. **Primary Horizontal**: `Quantity Ordered`
3. **Primary Vertical**: `Frequency (Number of Transactions)`

**Format Bars:**
1. Click on any bar
2. **Format Data Series**
3. **Fill**: Solid color (suggest blue or teal)
4. **Border**: Solid line, white, 1pt (separates bars clearly)
5. **Gap Width**: 0% (histogram bars should touch)

**Remove Legend:**
- Click legend and delete (not needed)

### Step 6: Add Statistics (Optional Enhancement)
**Add mean line:**
1. Calculate mean quantity (in Stats sheet or formula)
2. **Chart Design** → **Add Chart Element** → **Lines** → **Drop Lines**
3. Manually add vertical line at mean value using text box

### Step 7: Analyze Distribution
**Look for:**
- Skewness (left/right tail)
- Outliers (bars far from main cluster)
- Multiple peaks (bimodal distribution)

Add annotation text box with finding: "Right-skewed distribution with most orders 1-5 items"

### Step 8: Final Touches
1. Resize: Width = 9 columns, Height = 22 rows
2. Gridlines: Add horizontal major gridlines
3. Ensure bin width makes sense for your data range

### Verification Checklist:
- [ ] Bars touch each other (no gaps - this is histogram, not bar chart)
- [ ] Bin width is reasonable (not too wide, not too narrow)
- [ ] X-axis shows quantity ranges
- [ ] Y-axis shows frequency
- [ ] Chart reveals distribution shape clearly
- [ ] Any outliers visible

---

### Method 2: Using Data Analysis ToolPak (Alternative)

**If Method 1 doesn't work:**

### Step 1: Enable Data Analysis ToolPak
1. **File** → **Options** → **Add-ins**
2. **Manage**: Excel Add-ins → **Go**
3. Check **Analysis ToolPak** → **OK**

### Step 2: Create Histogram
1. **Data** tab → **Data Analysis**
2. Select **Histogram** → **OK**
3. **Input Range**: Select Quantity column
4. **Bin Range**: Leave blank (auto) or create bins
5. **Output Range**: New Worksheet
6. Check: **Chart Output**
7. **OK**

### Step 3: Move and Format
- Follow same formatting steps as Method 1

---

## Chart 9: Total Revenue Distribution (Histogram)

**Type**: Histogram
**Purpose**: Show distribution of transaction values (Question 2c - Outliers)
**Time Estimate**: 7-9 minutes
**Priority**: Low
**Status**: ❌ Missing

### Prerequisites:
- Data from Sales_Cleaned[Total_Recalc] column
- Similar to Chart 8, but for revenue instead of quantity

### Step 1: Select Data
1. Go to **Sales_Cleaned** sheet
2. Click on Total_Recalc column header
3. OR select data range only (avoid header)

### Step 2: Insert Histogram
1. **Insert** tab → **Insert Statistic Chart** → **Histogram**
2. Chart appears on Sales_Cleaned sheet

### Step 3: Move to Charts Sheet
1. Cut chart
2. **Charts** sheet
3. Paste at cell **A125** (below Chart 8)

### Step 4: Configure Bins
**Revenue data typically needs more bins due to wider range:**

1. Right-click horizontal axis
2. **Format Axis** → **Axis Options** → **Bins**
3. Select **Bin width**
4. Try these values:
   - Start with: **$100** (groups revenue in $100 increments)
   - If too many bars: Increase to **$200** or **$500**
   - If too few bars: Decrease to **$50**

**Recommended:** 15-20 bins for clear visualization

**Alternative approach:**
1. Use **Number of bins**: 15
2. Let Excel calculate optimal bin width

### Step 5: Format Chart
**Chart Title:**
- Type: `Distribution of Transaction Values`

**Axis Titles:**
1. **Primary Horizontal**: `Transaction Value ($)`
2. **Primary Vertical**: `Frequency (Number of Transactions)`

**Format X-Axis as Currency:**
1. Right-click X-axis (revenue values)
2. **Format Axis** → **Number** → Currency
3. Decimal places: 0
4. Symbol: $

**Format Bars:**
1. Click bars
2. **Format Data Series**
3. **Fill**: Solid color (suggest green or orange - different from Chart 8)
4. **Border**: White, 1pt
5. **Gap Width**: 0% (bars touch)

**Remove Legend:**
- Delete legend

### Step 6: Identify Outliers
**Visual analysis:**
- Look for bars far from main cluster (outliers)
- Note if distribution is normal or skewed

**Add annotation (optional):**
1. Insert text box
2. Label key findings:
   - "Most transactions: $X - $Y range"
   - "High-value outliers: $Z+"
3. Position near relevant bars

### Step 7: Statistical Overlay (Advanced - Optional)
**Add percentile markers:**
1. Calculate 25th, 50th, 75th percentiles in Stats sheet
2. Add vertical lines or annotations at these values
3. Helps identify quartile ranges

### Step 8: Final Formatting
1. Resize: Width = 10 columns, Height = 22 rows
2. Add gridlines
3. Ensure currency formatting clear

### Verification Checklist:
- [ ] Bins cover full revenue range
- [ ] X-axis formatted as currency
- [ ] Bin width is appropriate (not too wide/narrow)
- [ ] Bars touch (histogram style)
- [ ] Distribution shape is clear
- [ ] Outliers are visible (if present)

---

## Chart 10: Gross Profit by Category (Column Chart)

**Type**: Column Chart, Sorted Descending
**Purpose**: Compare profitability across categories (Question 2b - Patterns)
**Time Estimate**: 7-9 minutes
**Priority**: Medium
**Status**: ❌ Missing

### Prerequisites:
- Need pivot table to aggregate by category
- Gross_Profit_After_Discount column in Sales_Cleaned

### Step 1: Create Pivot Table
1. Go to **Sales_Cleaned** sheet
2. **Insert** → **PivotTable** → New Worksheet
3. Rename sheet: **Pivot_Category**

### Step 2: Configure Pivot Table
**Drag fields:**
- **Rows**: Category
- **Values**: Gross_Profit_After_Discount
  - Should show as "Sum of Gross_Profit_After_Discount"

### Step 3: Sort Descending
1. Click dropdown on "Row Labels"
2. **More Sort Options**
3. **Descending** by Sum of Gross_Profit_After_Discount
4. Highest profit category appears first

### Step 4: Insert Column Chart
1. Click anywhere in pivot
2. **Insert** → **Column Chart** → **Clustered Column**

### Step 5: Move to Charts Sheet
1. Cut chart
2. **Charts** sheet
3. Paste at cell **K125** (next to Chart 9)

### Step 6: Format Chart
**Chart Title:**
- Type: `Total Gross Profit by Category`

**Axis Titles:**
1. **Primary Vertical**: `Gross Profit ($)`
2. **Primary Horizontal**: Can delete (categories already labeled)

**Format Y-Axis as Currency:**
1. Right-click Y-axis
2. **Format Axis** → **Number** → Currency
3. Decimal: 0
4. Symbol: $

**Add Data Labels:**
1. Click columns
2. **Chart Design** → **Add Chart Element** → **Data Labels** → **Outside End**
3. Format as Currency

**Color Columns:**
**Option A - Gradient (shows ranking):**
1. Click columns
2. **Format Data Series** → **Fill** → **Gradient fill**
3. Preset: Green gradient (high to low)

**Option B - Individual colors by category:**
1. Click each column individually
2. Assign distinct colors per category

**Remove Legend:**
- Delete (not needed)

### Step 7: Enhance with Profit Margin (Optional Advanced)
**Add second axis with margin %:**
1. In pivot, add: Gross_Margin_% (as Average)
2. Create combo chart: Column + Line
3. Column = Gross Profit ($)
4. Line = Gross Margin (%)
5. Line uses secondary Y-axis (right side)

### Step 8: Final Touches
1. Resize: Width = 10 columns, Height = 22 rows
2. Gridlines: Add horizontal major
3. Gap width: 80%

### Verification Checklist:
- [ ] All categories displayed
- [ ] Sorted by profit (highest first)
- [ ] Y-axis formatted as currency
- [ ] Data labels show dollar amounts
- [ ] Easy to compare categories
- [ ] Colors help distinguish categories

---

## Chart 11: Sales by Year (Column Chart)

**Type**: Column Chart with Year-over-Year Growth
**Purpose**: Show annual trends (Question 2b - Trends)
**Time Estimate**: 8-10 minutes
**Priority**: Medium
**Status**: ❌ Missing

### Prerequisites:
- Need pivot table to aggregate by year
- Sales data spans multiple years (2023-2025)

### Step 1: Create Pivot Table
1. Go to **Sales_Cleaned** sheet
2. **Insert** → **PivotTable** → New Worksheet
3. Rename: **Pivot_Year**

### Step 2: Configure Pivot Table
**Drag fields:**
- **Rows**: Date (or Year column if you have it)
- **Values**: Total_Recalc (Sum)

**Group by Year:**
1. Right-click on any date in Row Labels
2. **Group**
3. Select: **Years** only
4. **OK**

**Result**: Should show 2023, 2024, 2025 (or your date range)

### Step 3: Calculate YoY Growth (Optional)
**Add calculated field for growth %:**
1. In pivot area, next to years, add column header: "YoY Growth %"
2. Formulas:
   - 2024: `=(B3-B2)/B2` (where B3=2024, B2=2023 revenue)
   - Format as percentage
3. This will be added as data labels

### Step 4: Insert Column Chart
1. Select only: Year + Revenue columns (not YoY%)
2. **Insert** → **Column Chart** → **Clustered Column**

### Step 5: Move to Charts Sheet
1. Cut chart
2. **Charts** sheet
3. Paste at cell **A155** (below Chart 10)

### Step 6: Format Chart
**Chart Title:**
- Type: `Annual Sales Performance`

**Axis Titles:**
1. **Primary Vertical**: `Total Revenue ($)`
2. **Primary Horizontal**: `Year`

**Format Y-Axis:**
1. Currency format: $
2. Decimal: 0

**Add Data Labels on Columns:**
1. Click columns
2. **Add Data Labels** → **Outside End**
3. Format as Currency
4. Font: Bold, 12pt

### Step 7: Add YoY Growth % Labels (Advanced)
**If you calculated YoY growth:**
1. **Chart Design** → **Add Chart Element** → **Data Labels** → **Data Callout**
2. Edit text boxes manually to show:
   - "2024: $XXX (+15%)"
   - "2025: $YYY (+8%)"
3. Position above each bar

**OR use text boxes:**
1. Insert text box above each column
2. Type: "+15%" or "-3%" (growth rate)
3. Color code: Green (positive), Red (negative)

### Step 8: Add Trendline
1. Right-click on columns
2. **Add Trendline**
3. **Linear**
4. Check: **Display Equation** (optional)
5. Shows growth trend direction

### Step 9: Color Code by Performance
**If showing growth:**
- Columns with positive growth: Green
- Columns with negative growth: Red
- First year (baseline): Blue

### Step 10: Final Formatting
1. Resize: Width = 8 columns, Height = 22 rows
2. Gridlines: Add horizontal major
3. Gap width: 120% (wider spacing for emphasis)

### Verification Checklist:
- [ ] All years displayed
- [ ] Revenue values formatted as currency
- [ ] Data labels clear and visible
- [ ] YoY growth % shown (if applicable)
- [ ] Trendline helps visualize growth direction
- [ ] Colors indicate performance (optional)

---

## Chart 12: Customer Age Distribution (Histogram)

**Type**: Histogram
**Purpose**: Show age demographics (Question 2b - Patterns)
**Time Estimate**: 5 minutes
**Priority**: ⭐ HIGH (Data ready!)
**Status**: ❌ Missing

### Prerequisites:
✅ Data available in Sales_Cleaned[Customer Age] column

### Step 1: Select Data
1. Go to **Sales_Cleaned** sheet
2. Click on **Customer Age** column header
3. OR select data range only (exclude header)

### Step 2: Insert Histogram
1. **Insert** tab → **Insert Statistic Chart** → **Histogram**
2. Chart appears on sheet

### Step 3: Move to Charts Sheet
1. Cut chart
2. **Charts** sheet
3. Paste at cell **K155** (next to Chart 11)

### Step 4: Configure Bins for Age
**Age data works well with 5-year bins:**
1. Right-click horizontal axis
2. **Format Axis** → **Axis Options** → **Bins**
3. Select **Bin width**
4. Enter: **5**
5. Result: Age groups like 18-23, 23-28, 28-33, etc.

**Alternative - Specific age ranges:**
1. Select **Number of bins**: 10
2. Or manually set bins: 20-30, 30-40, 40-50, 50-60, 60+

### Step 5: Format Chart
**Chart Title:**
- Type: `Customer Age Distribution`

**Axis Titles:**
1. **Primary Horizontal**: `Age (Years)`
2. **Primary Vertical**: `Number of Customers` (or `Frequency`)

**Format Bars:**
1. Click bars
2. **Format Data Series**
3. **Fill**: Solid color (suggest blue or purple)
4. **Border**: White, 1pt
5. **Gap Width**: 0% (histogram style)

**Remove Legend:**
- Delete legend

### Step 6: Add Age Insights
**Identify key demographics:**
1. Look at tallest bar(s) - this is primary age group
2. Add text box annotation:
   - "Primary demographic: Ages X-Y"
   - "Median age: Z years" (calculate in Stats sheet)

### Step 7: Statistical Reference Lines (Optional)
**Add mean/median line:**
1. Calculate mean age from Stats sheet
2. Insert vertical line using **Shape** tool
3. Label: "Mean: X years"

### Step 8: Final Touches
1. Resize: Width = 9 columns, Height = 22 rows
2. Gridlines: Add horizontal major
3. Ensure all age ranges visible

### Verification Checklist:
- [ ] Bins are 5-year age groups
- [ ] Bars touch (histogram style)
- [ ] X-axis shows age ranges clearly
- [ ] Distribution shape is clear
- [ ] Identifies primary customer age group
- [ ] No legend (not needed)

---

## Chart 13: Box Plot - Transaction Values by Region

**Type**: Box and Whisker Plot
**Purpose**: Visualize outliers and distribution by region (Question 2c - Outliers)
**Time Estimate**: 8-10 minutes
**Priority**: Low (Advanced chart)
**Status**: ❌ Missing

### Prerequisites:
- Excel 2016+ (has Box and Whisker chart)
- Direct data from Sales_Cleaned
- Region and Total_Recalc columns

### Step 1: Prepare Data Layout
**Box plots need data in columns by category:**

**Option A - Use Pivot:**
1. Not ideal for box plots - skip this

**Option B - Organize data manually:**
1. Create new sheet: **BoxPlot_Data**
2. Column headers: Region 1, Region 2, Region 3, etc.
3. Copy Total_Recalc values for each region into respective columns
4. This can be tedious - see Option C

**Option C - Direct selection (Recommended):**
- Excel 2016+ can create box plot directly from raw data
- Will guide through this method

### Step 2: Insert Box Plot Directly
1. Go to **Sales_Cleaned** sheet
2. Select two columns: **Region** AND **Total_Recalc**
3. Make sure to include headers
4. Example selection: Columns for Region (e.g., G1:G25001) + Total_Recalc (e.g., N1:N25001)
5. Hold Ctrl/Cmd to select both non-adjacent columns

### Step 3: Create Box and Whisker Chart
1. **Insert** tab → **Insert Statistic Chart**
2. Select **Box and Whisker** (second option)
3. Chart appears

**If Excel doesn't recognize structure:**
- You may need to create pivot table first that shows data by region
- Then create box plot from pivot

### Alternative Method Using Pivot:

### Step 3 Alternative: Create Supporting Pivot
1. Create pivot: **Rows** = Region, **Values** = Total_Recalc (no summarization needed, just show data)
2. Right-click on pivot → **PivotChart**
3. **Change Chart Type** → **Box and Whisker**

### Step 4: Move to Charts Sheet
1. Cut chart
2. **Charts** sheet
3. Paste at cell **A185** (below Chart 12)

### Step 5: Format Chart
**Chart Title:**
- Type: `Transaction Value Distribution by Region`

**Axis Titles:**
1. **Primary Vertical**: `Transaction Value ($)`
2. **Primary Horizontal**: `Region`

**Format Y-Axis as Currency:**
1. Right-click Y-axis
2. **Format Axis** → Currency, 0 decimals

**Interpret Box Plot Elements:**
- **Box**: Shows Q1 (bottom), Median (middle line), Q3 (top)
- **Whiskers**: Extend to min/max within 1.5×IQR
- **Dots**: Outliers beyond whiskers

### Step 6: Customize Box Plot Options
1. Right-click on chart
2. **Format Data Series**
3. Options:
   - **Show inner points**: Check (displays individual outliers)
   - **Show outlier points**: Check
   - **Show mean markers**: Check (adds X marker for mean)
   - **Show mean line**: Check (connects means across regions)

### Step 7: Color Code Boxes by Region
1. Click on each box individually
2. **Format Data Point**
3. Assign distinct color per region:
   - North: Blue
   - South: Orange
   - East: Green
   - West: Purple

### Step 8: Add Statistical Reference
**Add text box with statistics:**
1. Insert text box
2. Note findings:
   - "Region X has highest median: $YYY"
   - "Region Z shows most outliers"
   - "Region A has widest range (highest variability)"

### Step 9: Final Formatting
1. Resize: Width = 12 columns, Height = 25 rows (needs more space)
2. Gridlines: Add horizontal major
3. Ensure all outlier points visible

### Verification Checklist:
- [ ] Box plot for each region displayed
- [ ] Y-axis formatted as currency
- [ ] Boxes show Q1, Median, Q3
- [ ] Whiskers extend appropriately
- [ ] Outliers displayed as dots
- [ ] Mean markers visible (optional)
- [ ] Easy to compare regions

---

## Chart 14: Scatter Plot - Quantity vs Total Revenue

**Type**: Scatter Plot with Trendline
**Purpose**: Show relationship between variables (Question 2b - Relationships)
**Time Estimate**: 6-8 minutes
**Priority**: Medium
**Status**: ⚠️ Similar chart exists (Discount vs Margin)

### Prerequisites:
✅ Data available: Sales_Cleaned[Quantity] and Sales_Cleaned[Total_Recalc]

### Note:
You already have a scatter plot: "Relationship between Discount Rate and Gross Margin %"
This chart is similar concept but different variables. You may choose to:
- Create this additional scatter plot (Quantity vs Revenue)
- OR keep the existing one and skip this
- OR replace existing with this one

### Step 1: Select Data
1. Go to **Sales_Cleaned** sheet
2. Select two columns:
   - **X-axis**: Quantity (Column with quantity values)
   - **Y-axis**: Total_Recalc (Column with revenue)
3. Include headers
4. Hold Ctrl/Cmd to select both columns

### Step 2: Insert Scatter Plot
1. **Insert** tab → **Charts** → **Scatter**
2. Select: **Scatter** (first option - just dots, no lines)
3. Chart appears

### Step 3: Move to Charts Sheet
1. Cut chart
2. **Charts** sheet
3. Paste at cell **K185** (next to Chart 13)

### Step 4: Format Chart
**Chart Title:**
- Type: `Relationship: Quantity vs Transaction Value`

**Axis Titles:**
1. **Primary Horizontal**: `Quantity Ordered`
2. **Primary Vertical**: `Transaction Value ($)`

**Format Y-Axis as Currency:**
1. Right-click Y-axis
2. **Format Axis** → Currency

### Step 5: Add Trendline
**This is crucial for scatter plots:**
1. Right-click on any data point
2. **Add Trendline**
3. **Trendline Options**:
   - Type: **Linear** (straight line)
   - Check: **Display Equation**
   - Check: **Display R-squared value**
4. **Line Color**: Make it bold (red or black)
5. **Width**: 2pt

### Step 6: Interpret Trendline
**R-squared value indicates correlation strength:**
- R² = 0.0 - 0.3: Weak correlation
- R² = 0.3 - 0.7: Moderate correlation
- R² = 0.7 - 1.0: Strong correlation

**Add text box with finding:**
- "Strong positive correlation (R²=0.XX)"
- "Higher quantities associate with higher transaction values"

### Step 7: Format Data Points
1. Click on data points
2. **Format Data Series**
3. **Marker Options**:
   - **Fill**: Solid, semi-transparent (70% transparency)
   - **Color**: Blue
   - **Size**: 4-6pt
4. **Border**: None

**Why transparency?**: With 25,000 points, they overlap. Transparency shows density.

### Step 8: Add Data Density Insight (Advanced)
**If points are too crowded:**
1. Consider reducing marker size to 3pt
2. Or create bins/groups and use average per bin instead

### Step 9: Final Touches
1. Resize: Width = 10 columns, Height = 24 rows
2. Gridlines: Both horizontal and vertical major gridlines
3. Ensure equation and R² are readable

### Verification Checklist:
- [ ] Data points plotted (X=Quantity, Y=Revenue)
- [ ] Trendline displayed
- [ ] R-squared value shown
- [ ] Y-axis formatted as currency
- [ ] Both axes labeled
- [ ] Points are semi-transparent for density
- [ ] Correlation direction clear (positive/negative/none)

---

## Chart 15: Heatmap - Sales by Category and Region

**Type**: Heatmap using Conditional Formatting
**Purpose**: Show multi-dimensional patterns (Question 2b - Patterns)
**Time Estimate**: 10-12 minutes
**Priority**: Low (Complex)
**Status**: ❌ Missing

### Prerequisites:
- Need Pivot 8: Category × Region (from Pivot section of plan)
- Conditional formatting capability

### Note on Excel Heatmaps:
Excel doesn't have native "heatmap chart" type. We create heatmaps using:
1. Pivot table (Category rows × Region columns)
2. Conditional formatting with color scales
3. Screenshot or copy as image to Charts sheet

### Step 1: Create Pivot Table
1. Go to **Sales_Cleaned** sheet
2. **Insert** → **PivotTable** → New Worksheet
3. Rename: **Pivot_Heatmap**

### Step 2: Configure Pivot for Heatmap
**Drag fields:**
- **Rows**: Category
- **Columns**: Region
- **Values**: Total_Recalc (Sum)

**Result**: Matrix showing sales for each Category-Region combination

### Step 3: Format Pivot Table
**Simplify appearance:**
1. Click anywhere in pivot
2. **Design** tab → **Report Layout** → **Show in Tabular Form**
3. **Design** tab → **Subtotals** → **Do Not Show Subtotals**
4. **Design** tab → **Grand Totals** → **Off for Rows and Columns**

**Remove field headers:**
1. Right-click "Row Labels" → **Hide Field List**
2. Clean up headers so only Category names and Region names show

### Step 4: Apply Conditional Formatting (The "Heat")
1. Select the data cells only (not headers, not row/column labels)
   - Example: If categories in rows 2-10, regions in columns B-E, select B2:E10
2. **Home** tab → **Conditional Formatting**
3. **Color Scales** → **More Rules**
4. **Format Style**: 3-Color Scale
5. **Minimum**: Red (lowest sales)
6. **Midpoint**: Yellow (middle sales)
7. **Maximum**: Green (highest sales)
8. Click **OK**

**Result**: Cells are colored based on value - creates visual heatmap

### Step 5: Enhance Heatmap Appearance
**Adjust number formatting:**
1. Right-click data cells → **Format Cells**
2. **Number** → Currency, 0 decimals
3. OR use: Custom format `$#,##0,K` (shows thousands)

**Adjust cell size:**
1. Make cells square-ish (equal width and height)
2. Select columns B-E → Right-click → Column Width → 15
3. Select rows → Right-click → Row Height → 30

**Border cells:**
1. Select data range
2. **Home** → **Font** group → **Borders** → **All Borders**
3. Choose white or gray borders (1pt)

### Step 6: Add Title and Legend
**Add title above heatmap:**
1. In cell A1 (or wherever): Type `Sales Heatmap: Category × Region`
2. Format: Bold, 14pt, merge cells if needed

**Add color legend:**
1. Below heatmap, create mini legend:
   - Cell: "Low" → Format fill: Red
   - Cell: "Medium" → Format fill: Yellow
   - Cell: "High" → Format fill: Green

### Step 7: Copy Heatmap to Charts Sheet
**Excel doesn't treat this as a "chart object", so:**

**Method A - Copy as Image:**
1. Select entire heatmap (including title, headers, data, legend)
2. **Home** → **Copy** dropdown → **Copy as Picture**
3. Options: As shown on screen, Picture
4. Go to **Charts** sheet
5. Paste at cell **A215** (below Chart 14)

**Method B - Link as table:**
1. Select heatmap range
2. Copy (Ctrl+C / Cmd+C)
3. Charts sheet
4. **Paste Special** → **Paste Link**
5. Updates if pivot data changes

### Step 8: Annotate Findings
**Add text boxes on Charts sheet highlighting:**
1. "Highest sales: [Category X] in [Region Y]"
2. "Weakest combination: [Category A] in [Region B]"
3. "Best region overall: [Region Z]"

**Point to specific cells with arrows or callouts**

### Step 9: Alternative - Create Clustered Column Chart
**If heatmap too complex, create chart instead:**
1. Use same pivot (Category × Region)
2. **Insert** → **Column Chart** → **Clustered Column**
3. Each category gets grouped columns (one per region)
4. Less visual than heatmap but easier to read exact values

### Step 10: Final Adjustments
1. Ensure all category and region labels are fully visible
2. Verify color scale makes sense (green=high, red=low)
3. Add gridlines to separate cells clearly
4. Size appropriately: ~12 columns × 15 rows (larger than typical chart)

### Verification Checklist:
- [ ] Matrix layout: Categories in rows, Regions in columns
- [ ] Conditional formatting applied (color scale)
- [ ] Red = low sales, Green = high sales
- [ ] All cells sized consistently
- [ ] Title and legend present
- [ ] Copied to Charts sheet
- [ ] Annotations highlight key patterns
- [ ] Easy to identify best/worst combinations

---

## 🎯 Chart Creation Priority Order

Based on data availability and deliverable requirements:

### **Phase 1: Quick Wins** (20-30 min total)
1. ✅ Chart 12: Customer Age Histogram (5 min) - Data ready
2. ✅ Chart 2: Top 10 Products Bar (5 min) - Data ready
3. ✅ Chart 5: Payment Method Bar (5 min) - Data ready
4. ✅ Chart 4: Online vs In-Store Column (3 min) - Data ready

### **Phase 2: Simple Pivots** (30-40 min total)
5. Chart 3: Sales by Region Pie (6-8 min)
6. Chart 6: Customer by Membership (6-8 min)
7. Chart 7: Avg Transaction by Membership (6-8 min)
8. Chart 10: Gross Profit by Category (7-9 min)
9. Chart 11: Sales by Year (8-10 min)

### **Phase 3: Distributions** (20-25 min total)
10. Chart 8: Quantity Histogram (7-9 min)
11. Chart 9: Revenue Histogram (7-9 min)
12. Chart 14: Scatter Plot - Quantity vs Revenue (6-8 min)

### **Phase 4: Time Series** (8-10 min total)
13. Chart 1: Monthly Sales Trend Line (8-10 min) - Fix date issue first!

### **Phase 5: Advanced** (18-22 min total)
14. Chart 13: Box Plot by Region (8-10 min)
15. Chart 15: Heatmap - Category × Region (10-12 min)

**Total Time: 2.5-3 hours for all 15 charts**

---

## 💡 General Tips for All Charts

### Formatting Best Practices:
1. **Consistent sizing**: Most charts should be 8-10 columns wide × 20-25 rows tall
2. **Font sizes**: Title (14pt), Axis titles (12pt), Labels (10-11pt)
3. **Colors**: Use consistent color scheme across related charts
4. **Currency**: Always format money as Currency with $ symbol, 0 decimals
5. **Percentages**: Always show % symbol, typically 1 decimal place
6. **Gridlines**: Add horizontal major gridlines for bar/column/line charts
7. **Legends**: Remove if redundant (single series, or labels on axes)
8. **Data labels**: Add when exact values matter, position "Outside End"
9. **Borders**: Use white borders (1-2pt) between chart elements
10. **Gap width**: 80-120% for columns, 0% for histograms

### Common Issues and Fixes:
- **Chart is blurry**: Don't resize excessively; recreate if needed
- **Labels overlap**: Rotate text 45°, or increase chart size
- **Data not updating**: Right-click chart → Refresh Data
- **Can't move chart**: Click chart border (not inside chart area)
- **Wrong data displayed**: Check Select Data Source, adjust ranges
- **Legend blocks data**: Move legend to right or bottom, or remove
- **Axis doesn't start at zero**: Right-click axis → Format Axis → Set minimum to 0

### Documentation for Report:
For each chart, note in Insights sheet:
- **What it shows**: One sentence description
- **Key pattern/insight**: What stands out?
- **Evidence for Question 2b/2c**: Which requirement does it address?
- **Statistical support**: Any descriptive stats backing the visual?

---

## ✅ Completion Checklist

Track your progress as you create each chart:

- [ ] Chart 1: Monthly Sales Trend (Line Chart)
- [ ] Chart 2: Top 10 Products by Revenue (Bar Chart)
- [ ] Chart 3: Sales by Region (Pie Chart)
- [ ] Chart 4: Online vs In-Store Sales (Column Chart)
- [ ] Chart 5: Payment Method Distribution (Bar Chart)
- [ ] Chart 6: Customer by Membership Level (Column Chart)
- [ ] Chart 7: Avg Transaction by Membership (Column Chart)
- [ ] Chart 8: Quantity Distribution (Histogram)
- [ ] Chart 9: Total Revenue Distribution (Histogram)
- [ ] Chart 10: Gross Profit by Category (Column Chart)
- [ ] Chart 11: Sales by Year (Column Chart)
- [ ] Chart 12: Customer Age Distribution (Histogram)
- [ ] Chart 13: Box Plot - Transaction by Region (Box Plot)
- [ ] Chart 14: Scatter Plot - Quantity vs Revenue (Scatter)
- [ ] Chart 15: Heatmap - Category × Region (Heatmap)

---

**End of Chart Implementation Guide**

*For questions or issues, refer to project_excel_plan.md for context and requirements.*
