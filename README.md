# Power BI Custom Visuals Lab

A hands-on learning project for exploring Power BI custom visuals with a small, synthetic order-fulfillment dataset. The goal is to compare when a custom visual adds real value, build an accessible report, and document the trade-offs—not just collect eye-catching charts.

> **Project status:** Starter kit. It includes sample data, a report plan, DAX examples, and a Deneb spec. Build the `.pbix` report in Power BI Desktop and add your own screenshots as you complete it.

## What you will build

An interactive **Order Flow & Fulfillment Explorer** with report pages for:

1. **Executive overview** — revenue, profit, order count, and monthly trends.
2. **Route flows** — origin-to-destination region movement using a chord-style visual.
3. **Order detail** — a Gantt-style view of order-to-delivery duration and a searchable detail table.
4. **Product exploration** — product/category word cloud and revenue distribution by category.
5. **Visual comparison** — native Power BI visuals alongside custom alternatives, with notes on accessibility, performance, and licensing.

The included data is fictional and contains no personal or customer-identifying information.

## Repository contents

- [`data/orders.csv`](data/orders.csv) — synthetic order and delivery data.
- [`docs/report-build-guide.md`](docs/report-build-guide.md) — data model, measures, and report build instructions.
- [`docs/visual-catalog.md`](docs/visual-catalog.md) — what each example visual is for and where to find it.
- [`docs/accessibility-and-safety.md`](docs/accessibility-and-safety.md) — review checklist before using a visual.
- [`templates/visual-evaluation.md`](templates/visual-evaluation.md) — reusable evaluation worksheet.
- [`visuals/deneb/monthly-revenue.json`](visuals/deneb/monthly-revenue.json) — starter Vega-Lite spec for Deneb.

## Quick start

1. Install **Power BI Desktop** and create a blank report.
2. Import `data/orders.csv` using **Get data → Text/CSV**.
3. Follow the [report build guide](docs/report-build-guide.md) to create the measures and report pages.
4. Add custom visuals only from sources you have reviewed. See the [visual catalog](docs/visual-catalog.md).
5. Try the Deneb spec in `visuals/deneb/monthly-revenue.json` and map its fields as explained in the guide.
6. Save your report as `reports/order-flow-fulfillment.pbix` (the `.pbix` is intentionally not included in this starter kit).
7. Complete the evaluation worksheet and add your own report screenshots and findings.

## Resume-ready project description

Once you have built and tested the report, describe your actual work and outcomes, for example:

> Built an interactive Power BI order-fulfillment report using Power Query, DAX, and a documented star-schema-style model; evaluated custom visuals against native alternatives for route analysis, delivery timelines, and accessibility.

Only claim features and results you personally implemented and validated. Add a quantified result only if you measured it.

## Important notes

- This repository does **not** redistribute `.pbiviz` packages or claim ownership of third-party visuals. Install visuals from AppSource or their official publisher and review their current terms.
- Custom visuals can have different data access, export, certification, accessibility, and tenant-policy implications. Ask your Power BI administrator before using them with organizational data.
- The sample dataset and examples are provided as learning material. Replace them with data you are authorized to use before publishing.
- No license file is included yet. Add the license you choose before distributing this repository or its contents.

## Suggested next steps

- Add a screenshot of each finished report page to `images/`.
- Record the Power BI Desktop version and custom visual versions used.
- Add an analysis section to the README with your own findings and limitations.
- Test report behavior on keyboard navigation and a narrow/mobile layout.
