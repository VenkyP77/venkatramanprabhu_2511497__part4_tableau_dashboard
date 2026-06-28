# Chart Selection Justification

## 1. Sales Trend View — Dual-Axis Line Chart

**Question answered:** How are total sales and profit changing over time, and do they track each other?

**Why this chart type:** A line chart is the standard for continuous time-series data. It makes trends, seasonality, and reversals immediately visible through the direction and shape of the line — before a viewer reads a single label. A dual axis allows sales and profit to share the same time axis without requiring the viewer to cross-reference two separate charts. The two lines together reveal whether margin is expanding or compressing as revenue grows.

**Fields used:**
- X-axis (Columns): `Order Date` (aggregated to quarter)
- Y-axis (Rows): `SUM(Sales)` and `SUM(Profit)` on a dual axis
- Color: `Measure Names` (Orange for Sales, Blue for Profit), shown in the legend on the dashboard

**Design principle applied:** Pre-attentive processing — the direction of a line is processed by the eye before conscious reading begins. Growth, decline, and seasonal dips are perceptible at a glance, making this the most efficient chart type for communicating temporal change to an executive audience.

**Mistake avoided:** Did not use a bar chart for this view. Bar charts emphasise the magnitude of individual periods and make trend direction harder to perceive, especially when values are close. A line chart communicates trajectory far more clearly for time-series data.

---

## 2. Regional Performance View — Filled Map

**Question answered:** Which states and regions generate the strongest profit margins, and where are the geographic gaps?

**Why this chart type:** A filled map encodes performance spatially — states are coloured by profit margin intensity, allowing the viewer to see regional concentration patterns instantly without reading labels or sorting a table. Geography is the natural organising dimension for this question, and a map exploits the viewer's existing spatial knowledge of India.

**Fields used:**
- Geographic role: `State` (Tableau auto-generates Latitude and Longitude for India)
- Color: `AGG(Profit Margin)` (diverging colour scale — lighter = lower margin, darker = higher margin)
- Labels: `State`, `AGG(Profit Margin)`, `SUM(Sales)`

**Design principle applied:** Spatial pre-attentive encoding — geographic colour intensity is processed before the viewer reads any text. North and West states appear darker (higher margin) while South states appear lighter (lower margin) without requiring the audience to decode a ranked list.

**Mistake avoided:** Did not use a pie chart or stacked bar chart for geographic breakdown. Pie charts make regional comparison extremely difficult because humans cannot accurately judge angle differences. Maps preserve the natural geographic relationship between regions, which ranked bar charts discard.

---

## 3. Category Profitability View — Packed Bubble Chart

**Question answered:** Which sub-categories drive the most profit relative to their sales volume, and which are destroying margin?

**Why this chart type:** A packed bubble chart encodes two dimensions simultaneously — size (Sales volume) and colour (Profit Margin) — within a compact, space-efficient layout grouped by Category. This allows the viewer to identify problematic sub-categories: large red bubbles are high-revenue margin destroyers that demand immediate attention, while small green bubbles are niche but profitable.

**Fields used:**
- Columns: `Category` (groups bubbles into three category columns)
- Labels: `Sub-Category`, `AGG(Profit Margin)` (displayed as percentage), `SUM(Sales)`
- Color: `AGG(Profit Margin)` (diverging red-to-green scale, centred at the portfolio average)
- Size: `SUM(Sales)` (larger bubble = higher sales volume)

**Design principle applied:** Dual pre-attentive encoding — both size and colour communicate meaning independently. A viewer can answer two questions simultaneously: "Which sub-category sells the most?" (size) and "Is that sub-category profitable?" (colour). The combination is more information-dense than a bar chart or table at the same visual footprint.

**Mistake avoided:** Did not use a treemap alone. Treemaps handle size hierarchy well but cannot represent negative profit margin values intuitively — a negative-margin treemap cell requires the viewer to read the label to understand it is a loss. The packed bubble chart's diverging colour scale makes losses (red) and gains (green) immediately distinct without any label reading.

---

## 4. Customer Segment View — Grouped Bar Chart

**Question answered:** How do the three customer segments compare across sales, profit, and average order value?

**Why this chart type:** A grouped bar chart provides precise, side-by-side comparison of multiple measures across a small number of discrete categories. With only three segments (Consumer, Corporate, Home Office), grouped bars allow the viewer to compare all three segments on each measure without any ambiguity about relative magnitude — each bar starts at a common baseline of zero.

**Fields used:**
- Columns: `Customer Segment`
- Rows: Multiple measures — `SUM(Sales)`, `SUM(Profit)`, `AGG(Average Order Value)`
- Color: `Customer Segment` (three distinct colours, one per segment)

**Design principle applied:** Common baseline alignment — every bar in a grouped chart starts at zero, making inter-segment comparisons accurate. The viewer's eye immediately spots which segment leads on each metric without needing to mentally subtract starting positions, which stacked or 100% bars require.

**Mistake avoided:** Did not use stacked bars. Stacked bars make it nearly impossible to compare the middle and top segments because they do not share a common baseline. For a three-way segment comparison across multiple measures, stacking obscures the very differences the chart is meant to reveal.

---

## 5. Shipping Performance View — Bar Chart with Delay Bucket Colour

**Question answered:** Which shipping modes cause delivery delays, and how are orders distributed across fast, standard, and slow delivery tiers?

**Why this chart type:** A bar chart with Ship Mode on the X-axis and Average Delivery Days on the Y-axis directly answers the primary question — which mode is slowest on average. Colouring each bar by Shipping Delay Bucket adds the distributional detail without requiring a separate chart: the viewer can see both the average and the proportion of orders falling into each delay tier through colour.

**Fields used:**
- Columns: `Ship Mode` (First Class, Same Day, Second Class, Standard Class)
- Rows: `AVG(Delivery Days)`
- Color: `Shipping Delay Bucket` (Shipping Delay Bucket calculated field: Same Day/Next Day, Fast 2–3 days, Standard 4–5 days, Slow 6+ days)
- Label: Count of orders per delay bucket per ship mode

**Design principle applied:** Layered detail — the bar height communicates the primary metric (average delay) at a glance, while the colour breakdown within each bar provides operational detail (what fraction of orders fall into the problematic Slow bucket) without adding visual clutter or requiring a second chart.

**Mistake avoided:** Did not use a line chart. Ship Mode is a nominal categorical variable — there is no meaningful continuum between "First Class" and "Standard Class." Connecting them with a line implies an ordered, continuous relationship that does not exist, which would mislead the viewer about the nature of the variable.

---

## 6. Discount vs. Profit View — Scatter Plot (Standalone Worksheet)

**Question answered:** What is the relationship between the discount level applied to an order and the profit that order generates?

**Why this chart type:** A scatter plot is the correct tool for revealing the relationship between two continuous variables at the individual observation level. Each point represents a single order, making the negative correlation between high discounts and profit immediately visible as a cluster pattern — and crucially, it shows the full distribution including outliers and the concentration of losses, which any aggregated chart would hide.

This view is built as a standalone worksheet rather than embedded in the main dashboard. The scatter plot contains 4,200 individual points and is most valuable for deep analytical investigation rather than executive monitoring at a glance.

**Fields used:**
- X-axis (Columns): `Profit` (individual order profit, can be negative)
- Y-axis (Rows): `Discount` (0% to 35%)
- Color: `Category` (Furniture, Office Supplies, Technology — reveals which category drives the loss cluster)
- Size: `Sales` (larger circles represent higher-value orders)

**Design principle applied:** Category represented as colour and Sales volume represented as circle size — this turns the scatter plot from a simple correlation chart into a diagnostic tool. The viewer can simultaneously answer: "Is there a discount-profit relationship?" (plot pattern), "Which category is most affected?" (colour), and "Are the losses on large or small orders?" (size).

**Mistake avoided:** Did not use a line chart or aggregated bar chart for this analysis. Aggregating discount and profit into bins or averages hides the individual-order variability that makes the risk visible — specifically that some high-discount orders generate losses of -₹17,757 on a single transaction. The scatter plot preserves this granularity.

---

## 7. Return Analysis View — Horizontal Bar Chart

**Question answered:** Which product categories, sub-categories, and customer segments have the highest return rates?

**Why this chart type:** A horizontal bar chart ranked by Return Rate allows clear, accurate comparison across categories and sub-categories. Placing Category and Sub-Category on the row axis produces a natural two-level hierarchy — the viewer can read from the most- to least-returned sub-category without sorting a table. Colouring by Customer Segment adds a second dimension (which segment drives returns in each category) without requiring a separate chart.

**Fields used:**
- Rows: `Category` and `Sub-Category` (hierarchical row structure)
- Columns: `AGG(Return Rate)` (calculated field: `SUM([return_flag]) / COUNT([order_id])`, displayed as a percentage)
- Color: `Customer Segment` (Consumer, Corporate, Home Office — shows which segment's returns dominate each bar)
- Label: Return Rate percentage for each bar

**Design principle applied:** Normalisation — displaying Return Rate (a percentage) rather than raw return counts prevents high-volume categories from appearing riskier simply because they have more orders. A category with 50 returns out of 200 orders (25% rate) is structurally more problematic than one with 80 returns out of 2,000 orders (4% rate). The normalised rate makes this comparison honest.

**Mistake avoided:** Did not use raw return counts as the primary metric. Raw counts are volume-sensitive and would make high-order-volume categories (e.g., Office Supplies) appear to have more risk than they do. Return Rate is the correct business metric because it normalises for exposure and enables fair comparison across sub-categories of different sizes.
