# Part 4 — Executive Tableau Dashboard

## Business Problem Summary

The retail leadership team requires a single executive dashboard to monitor and act on sales performance across regions, product categories, customer segments, shipping modes, discount behaviour, and return patterns. The dashboard must surface both risks (margin erosion, delivery delays, returns) and opportunities (high-margin segments, seasonal peaks, efficient acquisition channels) to support data-driven decision-making.

---

## Dataset Description

**File:** `data/dashboard_sales_data.xlsx`

| Attribute | Value |
|---|---|
| Total rows | 4,200 orders |
| Date range | January 2024 – December 2025 |
| Total sales | ~₹217 crore |
| Total profit | ~₹33.3 crore |
| Overall profit margin | 15.35% |
| Return rate | 4.55% (191 of 4,200 orders) |

### Columns

| Column | Type | Description |
|---|---|---|
| order_id | String | Unique order identifier |
| order_date | Date | Date order was placed |
| ship_date | Date | Date order was shipped |
| customer_id | String | Unique customer identifier |
| customer_segment | String | Consumer / Corporate / Home Office |
| region | String | East / North / South / West |
| state | String | Indian state |
| city | String | City name |
| category | String | Furniture / Office Supplies / Technology |
| sub_category | String | 13 sub-categories (Accessories, Art, Binders, Bookcases, Chairs, Copiers, Furnishings, Labels, Machines, Paper, Phones, Storage, Tables) |
| product_name | String | Product description |
| ship_mode | String | First Class / Same Day / Second Class / Standard Class |
| sales | Float | Order revenue |
| quantity | Integer | Units ordered (1–10) |
| discount | Float | Discount applied (0–0.35) |
| profit | Float | Order profit (can be negative) |
| return_flag | Integer | 1 = returned, 0 = not returned |
| delivery_days | Integer | Days between order and ship date (0–9) |
| customer_rating | Float | Customer satisfaction score (2.1–5.0) |
| campaign_channel | String | Organic / Social / Referral / Paid / Email |

---

## Tableau Workbook Description

**File:** `tableau/executive_dashboard.twbx`

The packaged workbook contains:
- 7 individual worksheet views (see below)
- 1 executive dashboard embedding 6 of those views
- 5 calculated fields
- 4 dashboard filter actions + 1 highlight action for cross-chart interactivity
- Colour legends for Profit Margin, Measure Names, and Customer Segment serving as summary references

---

## Calculated Fields Created

| Calculated Field | Formula | Purpose |
|---|---|---|
| Profit Margin | `SUM([profit]) / SUM([sales])` | Measures profitability as a percentage of revenue |
| Cost | `[sales] - [profit]` | Derives cost from sales and profit |
| Average Order Value | `SUM([sales]) / COUNTD([order_id])` | Average revenue per unique order |
| Return Rate | `SUM([return_flag]) / COUNT([order_id])` | Percentage of orders that were returned |
| Shipping Delay Bucket | `IF [delivery_days] <= 1 THEN "Same Day/Next Day" ELSEIF [delivery_days] <= 3 THEN "Fast (2-3 days)" ELSEIF [delivery_days] <= 5 THEN "Standard (4-5 days)" ELSE "Slow (6+ days)" END` | Categorises delivery performance into four tiers |

---

## Dashboard Components

### Worksheets (7 total)

| Sheet Name | Chart Type | Business Question | On Dashboard |
|---|---|---|---|
| Sales Trend View | Dual-axis line chart (Sales + Profit, coloured by Measure Names) | How are sales and profit trending over time? | Yes |
| Regional Performance View | Filled map (State, coloured by Profit Margin) | Which states and regions perform best? | Yes |
| Category Profitability View | Packed bubble chart (Category columns, Sub-Category bubbles, size = Sales, colour = Profit Margin) | Which sub-categories drive or destroy profit? | Yes |
| Customer Segment View | Grouped bar chart (Segment vs Sales, Profit, AOV; coloured by Segment) | How do segments compare across key metrics? | Yes |
| Shipping Performance View | Bar chart (Ship Mode vs Avg Delivery Days, coloured by Shipping Delay Bucket) | Which ship modes cause delivery delays? | Yes |
| Return Analysis View | Horizontal bar chart (Category / Sub-Category vs Return Rate, coloured by Customer Segment) | Which categories and segments have high return rates? | Yes |
| Discount vs Profit | Scatter plot (Profit on X, Discount on Y, colour = Category, size = Sales) | How does discount level affect profitability? | Standalone sheet |

### Summary References on Dashboard
- **Measure Names legend** (Sales Trend View) — distinguishes Sales vs Profit lines
- **Profit Margin colour legend** (Category Profitability View) — diverging scale showing margin range
- **Customer Segment colour legend** (Return Analysis View) — segment breakdown in return bars

---

## Filters and Interactions

### Dashboard Actions (5 total)
| Action | Source Sheet | Behaviour |
|---|---|---|
| Filter 1 | Regional Performance View | Clicking a state filters all other views on the dashboard |
| Filter 2 | Sales Trend View | Clicking a time period filters all other views on the dashboard |
| Filter 3 | Customer Segment View | Clicking a segment bar filters all other views on the dashboard |
| Filter 4 | Category Profitability View | Clicking a bubble filters all other views on the dashboard |
| Highlight 1 | Any sheet | Selecting a Customer Segment highlights matching marks across all views |

---

## Key Business Insights

1. Sales show consistent Q2 dips each year, with the highest revenue recorded in Q4 driven by seasonal demand.
2. North and West regions lead in both sales and profit; South region underperforms on margin.
3. Technology is the highest-margin category (visible as large green bubbles in the packed bubble chart); Furniture sub-categories (Tables, Bookcases) appear as smaller, redder bubbles — frequently producing negative profit.
4. Home Office segment has the highest average order value with minimal discount pressure.
5. Discounts above 20% consistently result in negative or near-zero profit — visible as a downward scatter trend beyond the 20% reference line.
6. Standard Class shipping causes 6–9 day delays for a measurable subset of orders (Slow bucket in the bar chart).
7. Return rate is 4.55% (191 of 4,200 orders), concentrated in Technology and Furniture categories.
8. Organic and Referral channels deliver better per-order margins than Paid channel.

---

## Dashboard Story Summary

The business is growing in revenue but faces profitability pressure from aggressive discounting in Furniture, underperforming Southern operations, and shipping delays that harm customer experience. The Technology category and Home Office segment represent the strongest growth levers. Three immediate actions can protect margin: capping discounts at 20%, renegotiating carrier SLAs for Standard Class shipments, and reallocating paid channel budgets to Referral and Email programmes.

Full story: `outputs/dashboard_story.md`

---

## Assumptions and Limitations

- Delivery days are calculated as the difference between `ship_date` and `order_date`. This assumes ship date is a reliable proxy for dispatch; actual customer receipt date is not captured.
- Return reasons are not available — only a binary flag. Root-cause analysis is not possible from this dataset alone.
- Campaign channel spend data is absent; true channel ROI cannot be calculated.
- 32 records have missing `customer_rating` values and are excluded from satisfaction analysis.
- All monetary values are assumed to be in Indian Rupees (INR) based on geographic context (Indian states and cities).
- The dataset covers exactly 2 years (2024–2025); long-term trend conclusions are limited.

---

## Screenshots Included

| File | Contents |
|---|---|
| `screenshots/full_dashboard.png` | Complete executive dashboard — all 6 embedded views, title, and colour legends |
| `screenshots/sales_trend_view.png` | Dual-axis line chart: monthly Sales and Profit trend (Jan 2024 – Dec 2025) |
| `screenshots/regional_performance_view.png` | Filled state map coloured by Profit Margin |
| `screenshots/category_profitability_view.png` | Packed bubble chart — sub-category bubbles sized by Sales, coloured by Profit Margin |
| `screenshots/filter_interaction_view.png` | Dashboard with a filter action applied (e.g., clicking a region or segment) showing cross-chart filtering |
