# Business Insights

## Calculated Fields Reference

| Calculated Field | Formula | Purpose |
|---|---|---|
| Profit Margin | `SUM([profit]) / SUM([sales])` | Profitability as a percentage of revenue |
| Cost | `[sales] - [profit]` | Derives cost from revenue and profit |
| Average Order Value | `SUM([sales]) / COUNTD([order_id])` | Average revenue per unique order |
| Return Rate | `SUM([return_flag]) / COUNT([order_id])` | Fraction of orders returned |
| Shipping Delay Bucket | `IF [delivery_days] <= 1 THEN "Same Day/Next Day" ELSEIF [delivery_days] <= 3 THEN "Fast (2-3 days)" ELSEIF [delivery_days] <= 5 THEN "Standard (4-5 days)" ELSE "Slow (6+ days)" END` | Groups delivery speed into four business tiers |

---

## Insight 1 — Sales Trend: Q2 Slump and Q4 Peak Are Consistent Patterns

**Observation:** Quarterly sales show a recurring dip in Q2 each year, followed by recovery in Q3 and a peak in Q4. This W-shaped intra-year pattern repeats across both 2024 and 2025.

**Data Evidence:** Total sales across two years amount to approximately ₹217 crore. The Sales Trend View (dual-axis line chart) shows Q4 values clearly above annual averages each year, while Q2 quarters fall visibly below the trend line. Profit tracks a similar seasonal shape.

**Business Interpretation:** Q4 peaks are driven by year-end corporate budget cycles and festive purchasing. The Q2 dip likely reflects post-Q1 slowdowns once annual budgets are committed and before mid-year reviews unlock new spend.

**Recommended Action:** Pre-position inventory and lock in marketing spend by October each year to maximise Q4 capture. Design a targeted Q2 stimulus campaign (discounts with controlled margins, bundle offers) to reduce the seasonal revenue valley.

---

## Insight 2 — Regional Performance: North and West Lead, South Lags

**Observation:** The filled state map shows North and West states with consistently darker shading, indicating higher profit margins. South states appear lighter, signalling weaker profitability relative to sales volume.

**Data Evidence:** Four regions are present — East, North, South, West. Profit margin across regions is visible on the Regional Performance View, where South states (Karnataka, Tamil Nadu, Andhra Pradesh) show noticeably thinner margins despite generating meaningful order volumes.

**Business Interpretation:** North and West benefit from denser urban markets (Punjab, Rajasthan, Maharashtra) and likely more efficient distribution networks. The South may be absorbing higher last-mile delivery costs or offering steeper discounts to compete with local suppliers.

**Recommended Action:** Conduct a cost-structure audit for South-region orders: break down shipping cost, discount rate, and category mix. Explore regional carrier renegotiation and targeted promotions anchored to high-margin Technology products to improve South profitability.

---

## Insight 3 — Category Profitability: Technology Leads, Furniture Tables Are a Consistent Loss

**Observation:** The packed bubble chart shows Technology sub-categories (Copiers, Phones, Accessories) as large green bubbles — high sales volume and strong profit margins. Furniture sub-categories, particularly Tables and Bookcases, appear as smaller red bubbles, indicating below-average or negative profit margins relative to their sales.

**Data Evidence:** The dataset's minimum profit row is -₹17,757, which occurs in Furniture. The overall portfolio profit margin is 15.35%, but Furniture sub-categories pull this down. Technology sub-categories consistently exceed the portfolio average margin.

**Business Interpretation:** Furniture has high unit cost and is frequently discounted aggressively to close deals, producing losses. Technology commands brand pricing power, keeping margins intact even at moderate discount levels.

**Recommended Action:** Introduce a minimum-margin floor for Furniture orders — no approval system should permit a Furniture deal below a defined margin threshold. Evaluate whether Tables and Bookcases can be re-priced, bundled with higher-margin accessories, or phased out of the catalogue.

---

## Insight 4 — Customer Segment: Home Office Has the Highest Average Order Value

**Observation:** The Customer Segment View (grouped bar chart) shows Corporate as the highest-volume segment by total sales, but Home Office leads in Average Order Value. Consumer is the most frequent buyer segment by order count.

**Data Evidence:** Three segments — Consumer, Corporate, Home Office — are compared across SUM(Sales), SUM(Profit), and Average Order Value. The dataset mean AOV is ₹51,670. Home Office orders skew larger in individual transaction size due to premium product preferences and lower discount demands.

**Business Interpretation:** Corporate clients drive total revenue through volume but compress margins through bulk discount negotiations. Home Office clients buy premium products selectively, accept standard pricing, and deliver better per-order profit. Consumer segment is transactional and price-sensitive.

**Recommended Action:** Protect margin on Corporate deals by adding a VP-approval gate for discounts above 20%. Target Home Office buyers through Email and Referral channels with premium Technology and Furniture bundles — this segment rewards quality over price.

---

## Insight 5 — Discount Impact: Profitability Collapses Above 20% Discount

**Observation:** The Discount vs. Profit scatter plot reveals a clear inflection point: orders with discounts below 20% are predominantly profitable, while those above 25% cluster in the negative-profit zone. The pattern is most pronounced in Furniture (visible through category colour encoding).

**Data Evidence:** Discounts range from 0% to 35% with a mean of 14%. Minimum profit in the dataset is -₹17,757. The scatter plot (Profit on X-axis, Discount on Y-axis, size = Sales) shows the loss cluster concentrated in the upper-left quadrant — high discount, negative profit — with Furniture category orders dominating that zone.

**Business Interpretation:** Sales teams are trading margin for deal closure at rates that destroy value. A 35%-discounted Furniture order generates a loss that requires several profitable orders to offset. The pattern is structural, not occasional.

**Recommended Action:** Cap standard discounts at 20%. Flag any proposed discount above 25% for mandatory manager review. Build a live margin calculator into the quoting workflow so sales teams see the profit impact before submitting an order.

---

## Insight 6 — Shipping Performance: Standard Class Orders Fall into the "Slow" Bucket

**Observation:** The Shipping Performance View (bar chart, Ship Mode vs. AVG Delivery Days, coloured by Shipping Delay Bucket) shows Standard Class with the highest average delivery time. A visible portion of Standard Class orders falls into the "Slow (6+ days)" bucket, while Same Day and First Class remain in the "Same Day/Next Day" and "Fast" tiers respectively.

**Data Evidence:** Delivery days across the dataset range from 0 to 9, with a mean of 3.59 days. Standard Class is the most used shipping mode. The Shipping Delay Bucket calculated field reveals that 6–9 day deliveries are disproportionately Standard Class orders.

**Business Interpretation:** Over-reliance on Standard Class to minimise shipping costs is creating measurable customer experience failures. Customer rating data (mean 4.06 out of 5, with values as low as 2.1) likely reflects dissatisfaction among customers who received "Slow" shipments.

**Recommended Action:** Offer automatic upgrade to Second Class for orders above a value threshold (e.g., ₹50,000). Audit Standard Class carrier routes with chronic delays and replace carriers on those lanes. Set a delivery time SLA and track compliance monthly.

---

## Insight 7 — Return Patterns: 4.55% Return Rate, Technology and Furniture Drive Risk

**Observation:** The Return Analysis View (horizontal bar chart, Category/Sub-Category vs. Return Rate, coloured by Customer Segment) shows Technology and Furniture sub-categories with elevated return rates. Corporate segment colour appears more frequently in the higher-return bars.

**Data Evidence:** 191 of 4,200 orders carry `return_flag = 1`, producing a 4.55% return rate. Aggregating return rate by Category and Sub-Category in the Return Analysis View highlights that certain Technology products (Machines, Copiers) and Furniture items (Tables) carry above-average return rates relative to their order volumes.

**Business Interpretation:** Technology returns are likely driven by product specification mismatches or defects on high-ticket items — each returned Copier or Machine erases the profit from multiple other orders. Furniture returns are plausibly linked to transit damage given the longer Standard Class delivery windows.

**Recommended Action:** Implement pre-shipment quality checks for high-value Technology SKUs. Require reinforced packaging for Furniture items shipped via Standard Class. Introduce a structured return-reason field in the order management system to enable root-cause analysis.

---

## Insight 8 — Campaign Channel: Organic and Referral Outperform Paid on Margin

**Observation:** Five campaign channels (Organic, Social, Referral, Paid, Email) drive orders across the dataset. Organic and Referral channel orders tend to carry lower average discounts, while Paid channel orders show a pattern of higher discount rates — suggesting price-sensitive customers acquired via paid advertising.

**Data Evidence:** Campaign channel is a dimension across all 4,200 orders. Filtering the Discount vs. Profit scatter plot by channel (via the dashboard filter actions) reveals that Paid channel orders cluster more heavily in the higher-discount zones compared to Organic and Referral orders, which concentrate in the low-discount / profitable zone.

**Business Interpretation:** Paid advertising attracts customers who have comparison-shopped and expect a deal, creating a double cost — ad spend plus margin erosion. Referral customers arrive pre-qualified with a recommendation, accept standard pricing, and require no discounting to convert. Organic customers exhibit similar quality.

**Recommended Action:** Reallocate 15–20% of Paid channel budget to a structured Referral incentive programme and an Email nurture sequence targeting past Organic buyers. Track margin-by-channel as a monthly KPI alongside revenue-by-channel to surface this hidden cost.
