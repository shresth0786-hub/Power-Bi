# Build the Order Flow & Fulfillment report

This guide uses the fictional [`orders.csv`](../data/orders.csv) dataset. It provides a repeatable learning path; the Power BI `.pbix` itself is not included.

## 1. Load and inspect the data

In Power BI Desktop, select **Get data → Text/CSV**, load `data/orders.csv`, and rename the query to `Orders`.

In Power Query, check the data types:

| Column | Type |
| --- | --- |
| OrderID | Text |
| OrderDate, DeliveryDate | Date |
| OriginRegion, DestinationRegion, Category, Product, Segment | Text |
| Units | Whole number |
| Revenue, Cost | Decimal number / Fixed decimal number |

Create a `Profit` column in Power Query (`Revenue - Cost`) if you want row-level profit available for inspection, or use the DAX measure below. Remove duplicates only after verifying the intended grain: one row per order in this sample.

## 2. Create a date table

Create a calendar table and mark it as the date table using `Date`:

```DAX
Calendar =
ADDCOLUMNS (
    CALENDAR ( MIN ( Orders[OrderDate] ), MAX ( Orders[OrderDate] ) ),
    "Year", YEAR ( [Date] ),
    "Month Number", MONTH ( [Date] ),
    "Month", FORMAT ( [Date], "MMM" ),
    "Year-Month", FORMAT ( [Date], "YYYY-MM" )
)
```

Sort `Calendar[Month]` by `Calendar[Month Number]`. Create a one-to-many relationship from `Calendar[Date]` to `Orders[OrderDate]`. Keep the model simple for this learning dataset; if you use delivery-date analysis, create a second inactive date relationship and activate it in a dedicated measure with `USERELATIONSHIP`.

## 3. Add starter measures

```DAX
Revenue = SUM ( Orders[Revenue] )

Cost = SUM ( Orders[Cost] )

Profit = [Revenue] - [Cost]

Profit Margin = DIVIDE ( [Profit], [Revenue] )

Orders = DISTINCTCOUNT ( Orders[OrderID] )

Units Sold = SUM ( Orders[Units] )

Average Order Value = DIVIDE ( [Revenue], [Orders] )

Average Delivery Days =
AVERAGEX (
    Orders,
    DATEDIFF ( Orders[OrderDate], Orders[DeliveryDate], DAY )
)

Revenue Previous Year =
CALCULATE ( [Revenue], DATEADD ( Calendar[Date], -1, YEAR ) )

Revenue YoY % =
DIVIDE ( [Revenue] - [Revenue Previous Year], [Revenue Previous Year] )
```

Format `Revenue`, `Cost`, and `Profit` as currency; `Profit Margin` and `Revenue YoY %` as percentages. The sample covers one year, so the prior-year measure will be blank until you add another year of data.

## 4. Build report pages

### Page A — Executive overview

- KPI cards: Revenue, Profit, Profit Margin, Orders.
- Line chart: `Calendar[Year-Month]` by `[Revenue]`.
- Bar chart: `Category` by `[Profit]`.
- Slicers: `Calendar[Year]`, `OriginRegion`, `Segment`.
- Include a visible reset-filters button and meaningful visual titles.

### Page B — Route flows

- Use a chord visual only if you need to show movement between `OriginRegion` and `DestinationRegion`.
- Map source to `OriginRegion`, target to `DestinationRegion`, and weight to `[Revenue]` or `[Orders]`, following the visual publisher's field mapping.
- Add a native matrix with origin, destination, and `[Orders]` so users have a readable alternative.
- Explain that the sample has only a few regions and is for demonstration, not a logistics forecast.

### Page C — Fulfillment timeline

- Configure a Gantt visual with `OrderID` as the task, `OrderDate` as start, `DeliveryDate` as end, `DestinationRegion` as a grouping field, and `[Profit]` as an optional tooltip where supported.
- Add a native table with OrderID, dates, and delivery days. Do not rely on color alone to convey delay or status.

### Page D — Product and distribution exploration

- Word cloud: use `Product` as the term; size by `[Revenue]` where supported. Treat it as exploratory, not a precise ranking chart.
- Violin/distribution visual: compare `Revenue` or delivery duration by `Category` using the visual's documented field mapping.
- Provide a box plot, histogram, or table as an easier-to-read alternative if the custom visual is inaccessible or unsupported.

### Page E — Custom HTML card (optional)

Use an HTML Content visual only for a small, carefully tested presentation element. Prefer native cards for essential KPIs. Do not put untrusted data into HTML or JavaScript; check the visual publisher's security guidance and your organization's policy.

## 5. Try the Deneb example

Install Deneb from its official source, add a Deneb visual, and choose a Vega-Lite specification. Add `Calendar[Year-Month]` and `[Revenue]` to the visual's data fields, then paste [`monthly-revenue.json`](../visuals/deneb/monthly-revenue.json) into the editor. If the generated dataset field names differ, update the field references in the specification to match Deneb's data preview.

## 6. Validate and document

- Test slicers, cross-highlighting, tooltips, drill-through, and filter reset.
- Check totals against a Power BI table and the source CSV.
- Test keyboard navigation, screen reader labels, contrast, and a narrow layout.
- Verify rendering in the target environment (Desktop, Service, mobile, or export).
- Record each visual's publisher, version, source, license/terms, and any tenant approval in the evaluation worksheet.
- Add screenshots and your own findings to the repository only after checking that no restricted data or licensed assets are included.
