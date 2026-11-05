# Power BI Order Flow & Fulfillment Analytics

This portfolio project explores a fictional retailer's 2025 orders to answer three practical questions: **When does revenue peak? Which product categories contribute the most profit? How long do deliveries take across destination regions?**

It demonstrates an end-to-end analytics workflow: inspect and transform tabular data, define business measures, summarize results, and communicate findings with clear visuals. The repository includes a synthetic dataset, Power BI build instructions, DAX measure examples, and three **data-backed SVG charts** calculated from the included CSV.

> **Data and report status:** The CSV is fictional and contains 24 sample orders. The charts below show aggregates calculated from that CSV; they are not screenshots of a completed interactive Power BI report. The `.pbix` still needs to be built in Power BI Desktop using the guide.

## Data-backed visual results

### Monthly revenue

![Monthly revenue by order month, computed from the sample orders](SVG%20Visuals/monthly-revenue.svg)

Revenue totals **$4,357.30** across the 24 sample orders. December is the highest month (**$508.90**) and January the lowest (**$135.95**). These are small-sample observations, not evidence of seasonality.

### Profit by product category

![Profit by category, computed as revenue minus cost from the sample orders](SVG%20Visuals/profit-by-category.svg)

Furniture contributes the most sample profit (**$958.00**), followed by Electronics (**$444.71**) and Office (**$272.84**). Total profit is **$1,675.55**, a **38.45%** margin on sample revenue.

### Average delivery time by destination

![Average calendar days from order to delivery by destination region](SVG%20Visuals/delivery-days-by-region.svg)

Across all orders, the average order-to-delivery time is **4.46 days**. In this sample, East has the highest regional average (**5.29 days**, 7 orders) and South the lowest (**3.50 days**, 6 orders). Small group sizes mean these differences should be treated as exploratory.

## Project contents

- [`data/orders.csv`](data/orders.csv) — fictional order-level input data (24 rows, one row per order).
- [`SVG Visuals/monthly-revenue.svg`](SVG%20Visuals/monthly-revenue.svg) — monthly revenue totals.
- [`SVG Visuals/profit-by-category.svg`](SVG%20Visuals/profit-by-category.svg) — profit totals by category.
- [`SVG Visuals/delivery-days-by-region.svg`](SVG%20Visuals/delivery-days-by-region.svg) — average elapsed delivery days and order count by destination.
- [`docs/report-build-guide.md`](docs/report-build-guide.md) — Power Query, data model, DAX measures, and Power BI page-building steps.
- [`docs/visual-catalog.md`](docs/visual-catalog.md) — custom visual ideas and evaluation notes.
- [`docs/accessibility-and-safety.md`](docs/accessibility-and-safety.md) — review checklist.
- [`templates/visual-evaluation.md`](templates/visual-evaluation.md) — worksheet for assessing a visual.
- [`visuals/deneb/monthly-revenue.json`](visuals/deneb/monthly-revenue.json) — optional Deneb/Vega-Lite chart specification.

The earlier [`fulfillment-dashboard-preview.svg`](SVG%20Visuals/fulfillment-dashboard-preview.svg) is a design mockup, not a data-backed report output; use the three charts above for the dataset's actual aggregates.

## How to reproduce the analysis in Power BI

1. Open Power BI Desktop and import `data/orders.csv` using **Get data → Text/CSV**.
2. Verify column types and inspect the data in Power Query.
3. Follow the [report build guide](docs/report-build-guide.md) to create the calendar table, relationships, and measures.
4. Build report pages for the overview, product category, and fulfillment analyses.
5. Check each Power BI total against the CSV and the chart summaries above.
6. Save your report as `reports/order-flow-fulfillment.pbix`, then replace or supplement the SVG illustrations with screenshots of the finished report.

## Suggested measures

The guide includes DAX for revenue, cost, profit, profit margin, order count, average order value, average delivery days, and year-over-year revenue. The dataset only covers **2025**, so year-over-year results are blank until another year is added.

## Scope and limitations

- This is a learning project using synthetic data, not a real company's operational results.
- With only 24 orders and one year of records, category and regional comparisons are illustrative; do not generalize them to real business decisions.
- Delivery days are calendar-day differences between `OrderDate` and `DeliveryDate`.
- The SVG charts are static outputs. They are not interactive and do not replace the Power BI report.
- Custom visuals and third-party assets are not bundled. Review publisher terms, privacy, accessibility, and tenant approval before installing or using visuals with organizational data.

## Portfolio description

After you build and validate the `.pbix`, you can describe the work accurately, for example:

> Developed a Power BI order and fulfillment analysis using Power Query, a date dimension, and DAX measures; compared monthly revenue, category profit, and delivery duration by destination, validating report totals against the source data.

Add your own screenshots, design choices, and findings. Only claim features and results you personally implemented and tested.
