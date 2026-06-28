# Executive Dashboard Story

## Executive Summary

This dashboard gives the retail leadership team a single, interactive view of business performance across January 2024 to December 2025. It covers ₹217 crore in total sales across 4,200 orders, yielding a 15.35% overall profit margin. Six views are embedded on the main dashboard — Sales Trend, Regional Performance, Category Profitability, Customer Segment, Shipping Performance, and Return Analysis — linked by four filter actions and a cross-dashboard Customer Segment highlight. A dedicated Discount vs. Profit scatter plot sits as a standalone worksheet for deep-dive analysis.

The headline numbers are healthy. But when the six views are read together, three structural problems emerge: aggressive discounting is destroying margin (especially in Furniture), the South region is underperforming on profitability, and Standard Class shipping is creating customer dissatisfaction through chronic delays. Each problem has a clear lever the business can pull.

---

## What Is Performing Well

**Technology is a consistent profit engine.** The packed bubble chart on the dashboard makes this immediately visible — Technology sub-categories (Copiers, Phones, Accessories) appear as large green bubbles, signalling both high sales volume and strong profit margins. Technology is the category the business should prioritise protecting and growing.

**Q4 demand is reliable and predictable.** The Sales Trend View shows a Q4 peak repeating in both 2024 and 2025. This is structural seasonal demand driven by year-end corporate budget cycles and festive purchasing — not a one-time event. It is a growth lever the business can amplify with early preparation.

**Home Office buyers are the highest-quality customer segment.** The Customer Segment View shows that while Corporate leads on total revenue volume, Home Office commands the highest average order value. Home Office customers buy premium products without demanding heavy discounts — making them the most margin-efficient segment in the portfolio.

**Organic and Referral channels deliver profitable customers.** Orders originating from Organic and Referral channels carry lower average discounts and cluster in the profitable zone of the Discount vs. Profit scatter plot. These channels convert customers who arrive pre-qualified and willing to pay standard pricing.

---

## What Is Underperforming

**Furniture is the portfolio's largest margin problem.** The packed bubble chart flags Tables and Bookcases immediately — small red bubbles despite their sales volume, reflecting below-average or negative profit margins. The minimum single-order profit in the dataset is -₹17,757, occurring in Furniture. The combination of high product cost, aggressive discounting to close deals, and elevated return rates makes Furniture the riskiest category for profitability.

**The South region consistently trails on margin.** The Regional Performance filled map shows South states (Karnataka, Tamil Nadu, Andhra Pradesh) in lighter shades, indicating weaker profit margins relative to their sales volumes. North and West states — Punjab, Rajasthan, Maharashtra — dominate the darker, higher-margin zones. The gap is structural, not seasonal.

**Standard Class shipping is producing customer experience failures.** The Shipping Performance bar chart reveals that Standard Class orders carry the highest average delivery time and contain the largest share of orders in the "Slow (6+ days)" delay bucket. Customer rating data (minimum 2.1 out of 5.0) reflects the downstream impact on satisfaction.

---

## What Risks Are Visible

**Discount indiscipline above 20% is destroying value at scale.** The Discount vs. Profit scatter plot (standalone worksheet) tells the clearest version of this story: orders above 25% discount cluster heavily in the negative-profit zone. The pattern is structural — it repeats across both years and is concentrated in Furniture but visible across all categories. Without a hard discount ceiling, sales teams will continue prioritising deal closure over margin protection.

**A 4.55% return rate creates outsized profit risk in high-ticket categories.** The Return Analysis View shows Technology and Furniture sub-categories with elevated return rates. A single returned Copier or Machine — which are high-value Technology items — can erase the profit from ten or more smaller standard orders. Returns are currently tracked only as a binary flag; without return-reason data, root-cause correction is impossible.

**The Paid acquisition channel may be unprofitable once ad spend is factored in.** Paid channel orders show higher average discounts than Organic or Referral orders. When advertising spend is added to the margin already conceded on these orders, the true cost per profitable Paid customer is likely higher than the channel appears on a revenue-only basis.

---

## What Opportunities Are Visible

**Q4 amplification is the single largest near-term revenue lever.** The Q4 peak is confirmed across both years — the business is capturing it passively. A deliberate Q4 programme (inventory pre-positioning completed by September, targeted Email and Social campaigns from October, Technology bundle offers) could materially increase Q4 profitability without structural change.

**The Q2 slump is addressable.** The Sales Trend View shows a recurring Q2 dip in both years. This is predictable enough to plan against — a mid-cycle stimulus campaign (margin-controlled offers on Office Supplies, cross-sell prompts to past Furniture buyers for Technology accessories) could compress the seasonal valley.

**Home Office segment expansion has low execution risk.** Home Office customers already buy at a premium. A targeted Referral incentive programme and Email nurture sequence aimed at this segment could increase purchase frequency without requiring discounting. This is a high-margin growth path that does not depend on new customer acquisition.

**The South region offers whitespace at known scale.** North and West already demonstrate what is achievable in the Indian retail market. With a 90-day operational focus on the South — carrier renegotiation, reduced discount floors, and a category mix shift toward Technology — the South can close the margin gap visible on the map.

---

## Recommended Business Actions

1. **Enforce a 20% maximum discount policy** — no order should be processed above 20% discount without VP approval. Implement a margin floor check in the quoting workflow before submission.
2. **Renegotiate or discontinue loss-making Furniture SKUs** — specifically Tables and Bookcases. Evaluate re-pricing, minimum margin floors, or catalogue removal for sub-categories that cannot be made profitable within current pricing constraints.
3. **Fix Standard Class carrier performance on slow lanes** — identify the specific routes where Standard Class delivers in 6–9 days and switch carriers on those lanes. Set a delivery SLA with monthly compliance tracking.
4. **Reallocate 15–20% of Paid channel budget to Referral and Email** — measure margin-per-channel monthly, not just revenue-per-channel, and rebalance quarterly based on contribution margin.
5. **Launch a South region recovery sprint** — 90-day programme with dedicated focus on shipping cost reduction, category mix optimisation (more Technology, less high-discount Furniture), and targeted regional promotions.
6. **Build a Q4 readiness playbook** — inventory commitments, campaign calendar, and staffing plan locked by end of August each year to fully capture predictable Q4 demand.

---

## Limitations of the Dashboard

- **Two-year window only.** The dataset covers 2024–2025. Multi-year trend analysis and year-over-year growth rate calculations are limited by the short horizon.
- **Binary return flag, no return reasons.** The dashboard can show where returns are concentrated but cannot explain why. Root-cause analysis requires a structured return-reason field to be added at the order management layer.
- **No campaign spend data.** Channel ROI cannot be calculated because ad spend per channel is absent from the dataset. Margin-by-channel analysis is a directional proxy, not a true ROI.
- **32 missing customer ratings.** Customer satisfaction analysis based on `customer_rating` has a small data gap and may not fully represent the rated population.
- **No competitor or market benchmarks.** Regional underperformance conclusions are inferred from internal data only. External market context (competitor pricing, regional demand patterns) would strengthen the diagnosis.
- **Discount vs. Profit is a standalone sheet.** This view is not embedded in the main dashboard; it requires navigating to the worksheet tab for direct analysis.

---

## Suggested Next Analysis

- **Customer lifetime value (CLV) segmentation** — identify the top 20% of customers by lifetime profit contribution and build a retention and growth strategy specific to them.
- **Return reason dashboard** — after adding return-reason fields to the order system, build a dedicated returns root-cause view by reason, carrier, category, and segment.
- **Campaign ROI dashboard** — integrate advertising spend data and calculate true cost-per-order, margin-per-channel, and payback period by channel.
- **Cohort retention analysis** — track whether customers acquired in 2024 are returning in 2025 and at what frequency, to measure retention health and customer lifetime trajectory.
- **Shipping carrier scorecard** — map average delivery delay by carrier, region, and route to build a data-driven performance scorecard for carrier renegotiation.
- **Discount elasticity model** — quantify the relationship between discount level and order volume at a category and segment level to determine whether high discounts actually increase volume enough to justify the margin concession.
