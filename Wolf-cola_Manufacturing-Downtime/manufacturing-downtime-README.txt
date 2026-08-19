 Manufacturing Downtime Analysis — Wolf Cola

 Overview
An interactive Power BI dashboard analyzing bottling line productivity and downtime for Wolf Cola, a soft drink manufacturer based in Philadelphia. Built as a case study project, this dashboard picks up where a former production manager left off — turning a raw Excel dataset into an actionable view of line efficiency, downtime drivers, and operator performance.

The Business Case
Situation: As Production Manager for Wolf Cola, I inherited a productivity improvement project for the bottling line, along with a raw Excel file of operational data collected by the previous manager.

Assignment: Analyze the productivity and downtime data to identify opportunities to work with the operating staff and improve overall line efficiency.


Objectives:
1. Calculate overall line efficiency
2. Identify the main downtime factors
3. Break down downtime by operator and by factor

Data Source
- Source: Maven Analytics || Manufacturing Downtime (https://mavenanalytics.io/guided-projects/manufacturing-downtime-analysis)
- Table: Line productivity, Products, Downtime factors, Line downtime
- Connection type: Import
- Model: Star Schema


Notable DAX Measures
Output Efficiency = DIVIDE([Productive Hour],[Total Workhour],0)
No of Batches = COUNT('Line productivity'[Batch])
Productive Hour = [Total Workhour]-[Total Downtime]
Total Downtime = SUM('Line downtime'[Downtime Hr])
Total Workhour = SUM('Line productivity'[Shift])


Key Findings
1. The line is running at 64% efficiency — meaning over a third of total workhours (23.1 of 64.3 hours) were lost to downtime rather than production. 
2. Machine issues are the single biggest lever for improvement. The top two downtime factors — Machine Adjustment (5.5 hrs) and Machine Failure (4.2 hrs) — together account for nearly 42% of all downtime, more than Inventory Shortage, Batch Change, and Batch Coding Error combined. This points squarely at equipment maintenance and calibration as the highest-impact fix, ahead of process or staffing changes.
3. Cola drives the most downtime by volume, unsurprising given it's the flagship product with the highest batch count — but worth normalizing against batch volume to confirm it's not disproportionately downtime-heavy per batch versus flavors like Root Beer or Lemon Lime.
4. Operator performance is fairly tight, but not flat. Output efficiency ranges from Charlie's 66.8% down to Mac's 61.0% — a real but modest 5.8-point spread. Charlie also logs the most total downtime hours (6.4 hrs) alongside the highest efficiency, which likely reflects Charlie handling a higher batch volume overall rather than being the least efficient operator.
5. Recommendation: Prioritize a maintenance/calibration review on machine adjustment and failure rates before investing in operator retraining — the data points to equipment, not people, as the primary efficiency bottleneck.


Tools Used
Power BI Desktop (data modeling, DAX, visuals) 
Excel (source data, initial exploration)

