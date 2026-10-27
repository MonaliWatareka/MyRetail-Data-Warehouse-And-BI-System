# MyRetail-Data-Warehouse-And-BI-System

MyRetail Data Warehouse & BI System is an end-to-end Data Warehousing and Business Intelligence solution built on a retail sales dataset containing 302,010 transaction records spanning 2023–2024. The project covers the full data pipeline from raw source data through to interactive analytical dashboards.

The solution was developed using Microsoft SQL Server technologies including SSIS for ETL, SSAS for OLAP cube creation, and Power BI for reporting. The data originated from two source types — a CSV flat file containing customer demographic data and a SQL Server database containing sales transaction records — satisfying the multi-source extraction requirement.

A Star Schema dimensional model was designed and implemented in the MyRetail_DW database, consisting of one central fact table (FactSales) and three dimension tables (DimCustomer, DimProduct, DimDate). DimCustomer was implemented as a Slowly Changing Dimension Type 2 to preserve the historical changes of customer attributes such as address and customer segment over time. DimProduct was designed with a three-level Product Category → Brand → Type hierarchy to support drill-down analysis.

Three SSIS packages were developed to handle the full ETL workflow. The Data_Profiling package analysed data quality in staging tables and identified issues including numeric formatting errors, blank empty strings, UTF-8 encoding corruption and State/Country mismatches, all of which were resolved before loading. The Load_Staging package extracted data from both source types into a staging database with OnPreExecute event handlers ensuring idempotent execution. The Load_DW package transformed and loaded data into the star schema in the correct dimensional order, using Lookup transforms for surrogate key resolution and the SCD Wizard for Type 2 customer history management.

The fact table was extended with accumulating snapshot columns to track transaction lifecycle timestamps, with a dedicated Execute SQL Task updating completion times and computing processing hours in hours.

An SSAS Multidimensional Cube was built over the data warehouse with user-facing hierarchies and three KPIs measuring Total Revenue, Total Transactions and Average Ratings. All five core OLAP operations — Roll-Up, Drill-Down, Slice, Dice and Pivot — were demonstrated through Excel PivotTables connected live to the deployed cube.

Four interactive Power BI reports were developed and published to Power BI Service: a Matrix crosstab report showing sales by product and year, a Cascading Slicer dashboard with dynamic country-to-category filtering, a hierarchical date Drill-Down report navigating from Year to Month to Day, and a Drill-Through report enabling navigation from product summary to detailed brand-level analysis.
