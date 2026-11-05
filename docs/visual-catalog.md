# Custom visual catalog

This catalog is a learning checklist, not an endorsement of a particular product. Power BI visuals and their terms can change; find and verify each visual through Microsoft AppSource or the publisher's official page before installation. This repository does not bundle visual packages.

| Visual type | Example use in this project | Key question to evaluate | Native alternative |
| --- | --- | --- | --- |
| Deneb (Vega / Vega-Lite) | Custom monthly revenue chart or distribution | Can the specification be maintained, and does it preserve useful accessibility and tooltips? | Line chart, bar chart, scatter chart |
| Chord diagram | Order movement between origin and destination regions | Does the circular layout clarify relationships, or make values harder to compare? | Matrix, Sankey-style visual (if approved), small multiples |
| Word cloud | Exploratory view of products by revenue | Is this only a discovery aid? Word size is not precise enough for comparison. | Sorted bar chart or table |
| Violin / distribution plot | Compare order value or delivery duration distributions | Does the visual expose the distribution clearly and support enough observations? | Histogram, box plot, strip/scatter plot |
| Gantt chart | Show order-to-delivery timelines | Are start/end dates and task labels clear, and does it work at the report's scale? | Table, timeline, matrix |
| HTML content | Optional decorative or compact summary element | Does it render safely and consistently, and is the same information available in native visuals? | Card, text box, KPI |

## Official discovery and documentation

- [Microsoft AppSource — Power BI visuals](https://appsource.microsoft.com/marketplace/apps?product=power-bi-visuals)
- [Microsoft Learn — Power BI visuals](https://learn.microsoft.com/power-bi/developer/visuals/power-bi-custom-visuals)
- [Deneb documentation](https://deneb-viz.github.io/)
- [Deneb source repository](https://github.com/deneb-viz/deneb)

For chord, word cloud, violin, Gantt, or HTML content visuals, search AppSource by visual type and check the publisher's official documentation. Confirm the publisher identity and current license/terms; names can refer to multiple different offerings.

## Install responsibly

1. Search for the visual in AppSource from Power BI Desktop or the AppSource website.
2. Verify its publisher, certification status if relevant, supported Power BI environments, and current terms.
3. Review its documentation, privacy/security behavior, updates, accessibility, export behavior, and known limitations.
4. Ask your administrator whether the visual is allowed in your tenant before using it with work data.
5. Record the exact visual and version in [`../templates/visual-evaluation.md`](../templates/visual-evaluation.md).
