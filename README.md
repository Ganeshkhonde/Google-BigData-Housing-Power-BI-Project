# House Market Analysis Dashboard

### Dashboard Link : (Add your Power BI Service link here)

## Problem Statement

This dashboard helps stakeholders understand housing market trends, sales performance, and pricing dynamics across different regions. It provides insights into property prices, sales growth, and factors influencing purchase decisions.

Through this dashboard, users can analyze median price changes, regional sales distribution, and relationships between offer price and purchase price. It also highlights key drivers impacting property pricing and market behavior.

Since housing prices and sales trends vary significantly across regions and time periods, this dashboard helps in identifying growth opportunities and potential risks in the real estate market.

---

### Tools Used

- Power BI Desktop  
- Google BigQuery (Data Source)  
- SQL (Data Transformation in BigQuery)  
- Power Query Editor  
- DAX (Data Analysis Expressions)  
- Data Modeling & Visualization  

---

### Steps followed 

- Step 1 : Data was loaded from Google BigQuery server into Power BI.
- Step 2 : Data transformation and preprocessing were performed using SQL within BigQuery.
- Step 3 : Cleaned and structured dataset before importing into Power BI.
- Step 4 : Opened Power Query Editor & enabled "Column distribution", "Column quality" & "Column profile".
- Step 5 : Applied profiling on entire dataset.
- Step 6 : Handled missing and inconsistent values in pricing and area-related fields.
- Step 7 : Created required measures using DAX.
- Step 8 : Designed visuals such as bar charts, scatter plots, donut charts, and KPI cards.
- Step 9 : Added slicers for Area, City, and Sales Type.
- Step 10 : Built report across three pages:
           (a) House Market Overview
           (b) Sales Performance
           (c) Property Insights & Pricing Analysis
- Step 11 : Published report to Power BI Service.

---

# Report Snapshot (Power BI DESKTOP)

### Page 1 : House Market Overview
<img width="2394" height="1352" alt="Image" src="https://github.com/user-attachments/assets/a85022d1-8d80-459f-bbf8-efc64ae2599f" />

### Page 2 : Sales Performance
<img width="2404" height="1328" alt="Image" src="https://github.com/user-attachments/assets/b3d82b00-2e0e-43e1-a593-362a76890102" />

### Page 3 : Property Insights & Pricing Analysis
<img width="2394" height="1348" alt="Image" src="https://github.com/user-attachments/assets/380be671-f1af-44a5-bef1-fd999a797ba7" />

---

# DAX Measures

Avg Price Per SQM =  
AVERAGE('housing'[sqm_price])

---

Last 12 Months Sales =  
CALCULATE(  
SUM('housing'[purchase_price]),  
DATESINPERIOD('housing'[date].[Date], MAX('housing'[date]), -12, MONTH)  
)

---

Median Sales Price Change =  
VAR CurrMedianPrice =  
MEDIANX(  
FILTER('housing', YEAR('housing'[date].[Date]) = YEAR(MAX('housing'[date].[Date]))),  
'housing'[purchase_price]  
)  
VAR PrevMedianPrice =  
MEDIANX(  
FILTER('housing', YEAR('housing'[date].[Date]) = YEAR(MAX('housing'[date].[Date])) - 1),  
'housing'[purchase_price]  
)  
RETURN  
IF(PrevMedianPrice <> 0, (CurrMedianPrice - PrevMedianPrice) / PrevMedianPrice * 100, BLANK())

---

Offer Price to SQM Ratio =  
DIVIDE(SUM('housing'[Offer Price]), SUM('housing'[sqm]))

---

Sales by Region =  
CALCULATE(SUM('housing'[purchase_price]), ALLEXCEPT('housing', 'housing'[region]))

---

Total YTD Sales =  
TOTALYTD(SUM('housing'[purchase_price]), 'housing'[date].[Date])

---

Units Sold in Latest Year & Quarter =  
CALCULATE(  
DISTINCTCOUNT('housing'[house_id]),  
YEAR('housing'[date]) = YEAR(MAX('housing'[date])),  
QUARTER('housing'[date]) = QUARTER(MAX('housing'[date]))  
)

---

YOY Sales Growth =  
VAR curryearsales =  
CALCULATE(SUM('housing'[purchase_price]), YEAR('housing'[date]) = YEAR(MAX('housing'[date])))  

VAR prevyearsales =  
CALCULATE(SUM('housing'[purchase_price]), YEAR('housing'[date]) = YEAR(MAX('housing'[date])) - 1)  

RETURN  
IF(prevyearsales <> 0, (curryearsales - prevyearsales) / prevyearsales * 100, BLANK())

---

# Insights

A multi-page report was created on Power BI Desktop & published to Power BI Service.

### [1] Regional Sales Analysis

Zealand contributes the highest sales followed by Jutland and Fyn & Islands.  
Bornholm shows minimal contribution.  

thus, majority of sales are concentrated in major regions.

---

### [2] Price Trends

Median sales price has declined across all regions.  
Regions like Bornholm and Zealand show higher percentage drops.  

thus, housing market is experiencing downward price pressure.

---

### [3] Sales Performance

Total sales in last 12 months reached significant volume.  
Units sold in latest quarter indicate steady demand.  

thus, despite price decline, transaction volume remains stable.

---

### [4] Offer vs Purchase Price

Strong linear relationship between offer price and purchase price.  

thus, pricing strategies are closely aligned with market expectations.

---

### [5] Property Type Analysis

Different property types show variation in:
- Offer price  
- Purchase price  
- Price per SQM  

thus, property type plays a crucial role in valuation.

---

### [6] Key Influencers

Age and other demographic or property features influence purchase price significantly.  

thus, multiple factors drive housing price variations.

---

### [7] Growth Trends

YOY sales growth shows fluctuations across years.  
Some categories like family sales show negative growth.  

thus, growth is uneven across sales types.

---

# Conclusion

This dashboard provides a comprehensive analysis of housing market trends, pricing behavior, and sales performance. By integrating Google BigQuery with Power BI, it enables scalable data processing and real-time insights.

It helps stakeholders make informed decisions related to property investments, pricing strategies, and market analysis.


