Superstore Sales Overview Dashboard


Overview
An interactive sales performance dashboard built on the Superstore dataset, giving a monthly snapshot of sales, profit, orders, and customer activity with filters by region, segment, and year. Built to track overall business health and spot trends at a glance.


Data Source
Source: [Superstore dataset, Kaggle] (https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)
Connection type: Import


Key Questions Answered
	How is sales, profit, and order volume trending month over month?
	How does performance this period compare to the same period last year?
	Which product categories and discount levels are driving the most sales?
	What are the top-performing products?


Notable DAX Measures
¬---------------------------------------------------------------------------------------------
Calender = ADDCOLUMNS(
    CALENDAR(MIN(superstore_dataset[ship_date]),MAX(superstore_dataset[ship_date])),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month", FORMAT([Date], "MMMm"),
    "Month Short", FORMAT([Date],"MMM"),
    "Quarter", "Q" & QUARTER([Date]),
    "Year Month", FORMAT([Date],"YYYY-MM"),
    "Day", DAY([Date]),
    "Day Name", FORMAT([Date],"dddd"),
    "Week Number", WEEKNUM([Date]))
------------------------------------------------------------------------------------------------
Sales YTD growth % = 
VAR 
    SalesYTD = TOTALYTD([Sales Total],Calender[Date])
VAR
    SalesLastYear = CALCULATE([Sales Total],SAMEPERIODLASTYEAR(Calender[Date]))
VAR
    Growth = DIVIDE([Sales Total]-SalesLastYear,SalesLastYear,0)
RETURN
    IF(
    Growth > 0,
    "▲ " & FORMAT(Growth, "0.00%"),
        IF(
        Growth < 0,
        "▼ " & FORMAT(ABS(Growth), "0.00%"),
        "▬ 0.00%"
        )
    )
---------------------------------------------------------------------------------------------
TITLE = "SALES OVERVIEW (" & FORMAT(MAX(Calender[Date]),"MMMM yyyy)")
---------------------------------------------------------------------------------------------
Sales Total = SUM(superstore_dataset[quantity])
---------------------------------------------------------------------------------------------


Key Findings — December 2021
	Total sales reached 9,823 units for the month, up 1.32% MoM and 21.14% YoY
	Total profit hit $82.94K, growing 4.16% MoM and a strong 31.90% YoY
	Order volume (1,305) dipped slightly month-over-month (-0.15%) despite the sales increase, but is still up 24.05% YoY
	Sales are heavily concentrated in no-discount transactions (49.05%), suggesting most revenue isn't being driven by markdowns
	Office Supplies is the dominant category at 60.54% of sales, more than double Furniture (22.16%) and Technology (17.3%) combined
	Staples is the top-selling individual product, well ahead of the next closest item
	Sales trended strongly upward from August through December, with a notable spike in September


Tools Used
	Power BI Desktop (data modeling, DAX, visuals) 
	Excel/Kaggle CSV (source data)
	