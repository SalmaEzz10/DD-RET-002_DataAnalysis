# Crescent Grocery: Promotions, Returns & Inventory Analysis

A retail analytics project built with **Python** and **Power BI**. It looks at sales, margin, promotions, returns and inventory for a Saudi grocery chain.

The data is synthetic and comes from the [Findi360](https://findi360.com) retail case study (DD-RET-002, Level 2).

## Business question

Which promotions and products actually make money, and is inventory working in the company's favour?

## The data

| | |
|---|---|
| Company | Crescent Grocery, 15 stores (express, supermarket, hypermarket) |
| Period | Jan 2023 to Dec 2025 |
| Currency | SAR |
| Sales | 30,000 transaction lines |
| Inventory | 40,500 monthly store-product snapshots |
| Dimensions | Date, Store, Product, Supplier, Channel, Promotion |

## Data model

A **star schema** with two fact tables (a galaxy schema): sales and inventory share the Date, Store and Product dimensions.

- 11 relationships, all many-to-one, single direction.
- Fulfilment date and return date are **inactive** relationships, switched on inside measures with `USERELATIONSHIP`.

## Steps

1. **Clean** the raw files in Python. Suspicious rows are flagged, not deleted, so totals stay intact.
2. **Model** the 8 clean tables in Power BI.
3. **Measure**: 64 DAX measures, checked against the expected answers.
4. **Report**: 5 dashboard pages.

## Dashboards

| Page | Focus |
|---|---|
| D1 Executive Overview | Sales, margin, growth |
| D2 Sales Performance | Stores, categories, products, suppliers |
| D3 Promotions & Margin | Promotion impact, private label |
| D4 Returns & Fulfilment | Returns by channel and category, same-day delivery |
| D5 Inventory & Working Capital | Stock levels, stockouts, days of supply |

## Key findings

**1. Promotions reduce margin (D3)**
Gross margin is about 23% on promoted sales and about 35% on non-promoted sales. Loyalty promotions are the weakest: about 21% discount for about 19% margin. Bundle promotions do better.

**2. Returns are high in two channels (D4)**
Click and Collect (5.8%) and Online (5.5%) have more than twice the return rate of In Store (2.4%). Same-day fulfilment is about 25% in those channels versus 100% in store.

**3. Inventory is in the wrong place (D5)**
Dairy and Ready Meals hold about 36% of inventory but bring about 17% of gross margin. At the same time, 144 items are below their reorder point.

## Recommendations

- Reduce Loyalty discounts and favour Bundle promotions.
- Investigate returns in Click and Collect and Online (picking, substitutions, delivery time).
- Cut Dairy stock, watch Ready Meals cover, and redirect the cash to low-stock items.

## Files

```
Cleaning.ipynb          Python cleaning notebook
Data/                   Clean CSV files (output of the notebook)
RET002.pbix             Power BI report
```

## How to run

1. Put the raw DD-RET-002 CSV files in a folder and set `BASE` in the notebook.
2. Run `Cleaning.ipynb`. It writes 8 `_clean.csv` files to `Data/`.
3. Open `RET002.pbix`, point the data sources to `Data/`, and refresh.

## Tools

Python (pandas), Power BI, DAX.
