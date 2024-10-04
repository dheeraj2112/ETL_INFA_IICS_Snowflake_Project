#Sample Datawarehouse Project

1) Project Overview
2) 
The goal of a data warehouse project is to consolidate data from various sources into a centralized repository for analysis and reporting. This enhances decision-making capabilities by providing a holistic view of the organization's data.

3) Source and Target 

Source: Source is Oracle on-prem HR schema. The script can be used to generate that data set, if not available handy. HR Objects and Data For Live SQL.sql
Target: Target is Snowflake having both EDW_STG and EDW Layers. The DDLs can be found in the repo. IICS_ORA_SNFLK_EDW_DDL.sql

3) Data Flow

Source (Oracle) to Stg(Snowflake) : Using SCD Type-1
Stg (Snowflake) to EDW(Snowflake) : Using SCD Type-2

Optinal EDW_STG to EDW data flow can be implemented using Snowflake features itself using Streams, Tasks, Stored Proc etc. The code can be found here. 

4) ETL Code using IICS

The ETL Code can be found in the repo.  Enterprise Data Warehouse Export 4_Octtober_2024.zip

<END OF DOCUMENT>
