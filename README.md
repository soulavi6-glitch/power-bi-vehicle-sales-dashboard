# power-bi-vehicle-sales-dashboard
# Power BI Practice: Vehicle Sales Data and Chart Types

Power BI practice workbook covering 13 chart and report types. The main dataset is vehicle product sales (classic cars, motorcycles, trucks, planes, ships and trains), used for the cards, trend, pie/donut, table and matrix reports. Smaller practice datasets are used for the other chart types.

## Tools Used

- Power BI Desktop
- Power Query (data cleaning and transformation)
- DAX (measures and calculated columns)

## Report Pages

| Page | Visual | Data used |
| ---- | ------ | --------- |
| dashboard2 | Line chart | Orders by month (vehicle sales) |
| Page 1 | Ribbon chart | Population by member state |
| water fall type report | Waterfall chart | Population by member state |
| scatter chart | Scatter chart | Advertising costs vs sales figures |
| pie and donut | Pie / donut chart | Quantity ordered by deal size (vehicle sales) |
| Tree map chart | Treemap | CO2 emissions by region and country |
| map chart | Bubble map + table | Biocapacity by country and region |
| field chart | Filled map | Biocapacity by country and region |
| gauge chart | Gauge + salesman slicer | Target achieved vs target value |
| Kpi chart | KPI visual + month slicer | Actual vs target sales |
| card chart | Cards, column chart, month and year slicers | Quantity and total sales by month (vehicle sales) |
| Table | Table | Quantity and order count by country (vehicle sales) |
| matrix | Matrix | Quantity by city and country, split by order status (vehicle sales) |

## Main Dataset: Vehicle Product Sales

2,823 order lines from 307 orders, 92 customers and 19 countries, covering Jan 2003 – May 2005. Product lines: Classic Cars, Vintage Cars, Motorcycles, Trucks and Buses, Planes, Ships and Trains.

## Data Preparation (Power Query)

- Loaded the Excel sheet, promoted headers and set data types
- Split the order date and time column and kept only the date
- Removed blank rows and replaced null values in the state and address fields
- Combined contact first and last name into a single customer name column
- Removed columns not needed for analysis (quarter, month, year IDs, address lines, separate contact names)
- Replaced errors in the postal code column with 0

## Data Model

| From | To | Type |
| ---- | -- | ---- |
| Sales_Data1 (Country) | map chart (Country) | Many to one |
| tree map chart (Country) | map chart (Country) | Many to one |
| sales_data (emp_code) | sales_team (emp_code) | Many to one |

## DAX

| Name | Type | Formula | Purpose |
| ---- | ---- | ------- | ------- |
| Total quantity | Measure | `SUM(Sales_Data1[QUANTITYORDERED])` | Total units ordered |
| Total_sales | Measure | `SUMX(Sales_Data1, Sales_Data1[QUANTITYORDERED] * Sales_Data1[PRICEEACH])` | Total sales value, calculated row by row |
| Full_sales_ammount | Calculated column | `Sales_Data1[QUANTITYORDERED] * Sales_Data1[PRICEEACH]` | Sales value per order line |
| Incentive | Calculated column | `Sales_Data1[Full_sales_ammount] * 0.02` | 2% incentive on each order line |

## Key Insights (Vehicle Sales Data)

- **Total sales:** about 8.29 million from 99,067 units and 307 orders.
- **Product lines:** Classic Cars lead with 35.8% of sales, followed by Vintage Cars (19.8%). Trains are the smallest at 2.5%.
- **Countries:** the USA brings in 36.0% of sales, followed by Spain (12.3%) and France (11.1%). By territory, EMEA is 49.8% and North America 38.4%.
- **Deal size:** medium deals make up 59.8% of sales, small deals 31.2% and large deals 8.9%.
- **Order status:** 92.3% of sales value is shipped, and 2.1% is cancelled.
- **Seasonality:** November is the strongest month. Nov 2004 (10,678 units) and Nov 2003 (10,179 units) are the two highest months.
- **Growth:** sales rose from 2.90 million in 2003 to 3.91 million in 2004 (+35%). 2005 covers only Jan–May.
- **Top customers:** Euro Shopping Channel (9.2% of sales) and Mini Gifts Distributors Ltd. (6.4%).
- **Incentive:** at 2% of sales value, the total incentive comes to about 165,800.

## Files

- `power bi dashboard 2(line, waterfall, funnal chart).pbix`: Power BI practice workbook
