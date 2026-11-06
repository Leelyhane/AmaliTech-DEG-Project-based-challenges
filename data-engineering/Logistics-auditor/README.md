# The "Last Mile" Logistics Auditor - Verdict Logistics

## A. Executive Summary
An audit of 98,207 completed customer orders from the Brazilian E-Commerce dataset by Olist reveals that overall delivery performance is strong nationwide, averaging -11.88 days ahead of estimated dates with a high overall review score of 4.12 out of 5 stars. However, regional delivery bottlenecks exist where late (>5 days late) and unfulfilled shipments cause customer review scores to drop sharply from ~4.1 stars down to 1–2 stars. Bulky product categories such as `bed_bath_table` and `furniture_decor` account for disproportionately higher order volumes and freight costs, confirming that specific bulky inventory and regional carrier handoffs drive localized customer dissatisfaction rather than a systemic nationwide failure.

## B. Project Links
- **Link to the notebook:** https://github.com/Leelyhane/AmaliTech-DEG-Project-based-challenges.git
- **Link to the dashboard:** https://drive.google.com/file/d/1yev2OoiazD_qlRj81QGOmlxx8W3LsB6I/view?usp=drive_link
- **Link to the presentation:** https://docs.google.com/presentation/d/1HW1jFtnBKnaXVnq6SD0tVUI2bL-JQmVJLMGgLIyPAxY/edit?usp=sharing

## C. Technical Explanation

### 1. Data Cleaning & Pipeline (Story 1 & 2)
- **1-to-Many Join Prevention:** Aggregated the `olist_order_reviews_dataset` by `order_id` to calculate mean review scores per order and selected primary items from `olist_order_items_dataset` prior to joining. This avoided row duplication and metric inflation during table merges.
- **Filtering Unfulfilled Orders:** Filtered out `canceled` and `unavailable` orders before computing delivery performance metrics, isolating actual carrier transit efficiency.
- **Delay Calculation & Categorization:** Calculated `delay_days` as `order_delivered_customer_date` minus `order_estimated_delivery_date`. Categorized orders into `On Time` (<=0 days delay), `Late` (1–5 days late), and `Super Late` (>5 days late).
- **Category Translation (Story 5):** Joined Portuguese product categories with `product_category_name_translation.csv` to map items to clear English equivalents (e.g `bed_bath_table`, `furniture_decor`).

### 2. Candidate's Choice Addition
- **Freight Value vs. Category Delay Risk Analysis:** Integrated product category order volumes and average freight values alongside delivery delay metrics. This isolated whether heavy/bulky item logistics (high freight cost) correlate with increased delivery variance and lower review scores, providing regional directors with targeted logistics intervention points.

### 3. Note on Heatmap Visualization
- The standard geospatial map visual in Power BI Desktop encounters rendering limitations with two-letter Brazilian state ISO codes (e.g `RJ`, `SP`, `AL`). To maintain data integrity and clear readability, state-level delay performance is visualized using a sorted horizontal bar chart highlighting top regional delivery bottlenecks.