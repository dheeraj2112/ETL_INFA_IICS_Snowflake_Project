**Sample Datawarehouse Project using IICS with Snowflake**

1) Project Overview

The goal of a data warehouse project is to consolidate data from various sources into a centralized repository for analysis and reporting. This enhances decision-making capabilities by providing a holistic view of the organization's data.

2) Source and Target 

Source: Source is Oracle on-prem HR schema. The script can be used to generate that data set, if not available handy. https://github.com/dheeraj2112/INFA_IICS_Snowflake_Project/blob/a69bf3a16396e40a7a6fa0aedafebf485ddfecd8/HR%20Objects%20and%20Data%20For%20Live%20SQL.sql

Target: Target is Snowflake having both EDW_STG and EDW Layers. The DDLs can be found in the repo. https://github.com/dheeraj2112/INFA_IICS_Snowflake_Project/blob/a69bf3a16396e40a7a6fa0aedafebf485ddfecd8/IICS_ORA_SNFLK_EDW_DDL.sql

3) ETL/ELT Data Flows using Mappings and Mapping Tasks

Source (Oracle) to Stg(Snowflake) : Using SCD Type-1

Stg (Snowflake) to EDW(Snowflake) : Using SCD Type-2

orchestration and scheduling : Using Taskflows and as per needed schdule.

**SRC to STG**

![image](https://github.com/user-attachments/assets/e63a7caf-5ff8-490f-88c6-dbfacf91a887)

**STG to EDW**

![image](https://github.com/user-attachments/assets/ccdf50f0-2b15-49ad-95f7-a77203714916)

**ALL IN ONE TASKFLOW (Using Sub-Task flow to combine SRC to STG and STG to EDW Taskflows into one single WF)**

![image](https://github.com/user-attachments/assets/6362056c-f85f-48a6-8eb9-735fc1ffa098)


Optinal: EDW_STG to EDW data flow can be implemented using Snowflake features itself using Streams, Tasks, Stored Proc etc. The code can be found here.  https://github.com/dheeraj2112/INFA_IICS_Snowflake_Project/blob/a69bf3a16396e40a7a6fa0aedafebf485ddfecd8/EDW%20STG%20to%20EDW%20Pipelines%20using%20Snowflake%20based%20on%20ORA%20HR%20DB.sql

4) ETL Code using IICS

**Pre-requisite: Valid IICS account and an agent with DIS service should be up and running. Once this is already in place then re-configure/re-point the connections (DB, Flat File and APIs etc) to your enviroment accordingly. Once these are setup properly then import the ETL code from repo to IICS**

The ETL Code can be found in the repo.  https://github.com/dheeraj2112/INFA_IICS_Snowflake_Project/blob/a69bf3a16396e40a7a6fa0aedafebf485ddfecd8/Enterprise%20Data%20Warehouse%20Export%204_Octtober_2024.zip

SRC to EDW STG: Enterprise Data Warehouse\EDW_STG
EDW STG to EDW: Enterprise Data Warehouse\EDW
EDW_EXTR: Enterprise Data Warehouse\EDW_EXTR

Note: ODBC connection has been used from IICS to Snowflake  but if you have the JDBC connector feel free to re-point the Snowflake database and other connections accordingly.

5) Analysis and Reporting (ETL Code)
   
Views or Dynamic tables can be leveraged accordingly. This can be done from ETL job or Snowflake db objects as per need.

https://github.com/dheeraj2112/INFA_IICS_Snowflake_Project/blob/a69bf3a16396e40a7a6fa0aedafebf485ddfecd8/EDW_EXTR%20Views%20and%20Dynamic%20Tables%20for%20Reporting.sql

6) Addtionally, a Snowflake quickstart on **Harness the Power of Snowflake with Informatica Intelligent Data Management Cloud** can be followed whoever wants to do some specific hands on Snowflake with Informatica Cloud.

https://quickstarts.snowflake.com/guide/harness_the_power_of_snowflake_with_informatica_idmc/index.html?index=..%2F..index#0

7) Next Steps -->

i. Incremental/CDC logic handling ( either having some audit framework or IICS specific CDC handling features with SETVARIABLE option / in-built $LastRunDate or $LastRunTime variables)
ii. Build the EDW_STG to EDW data pipelines using Snowflake features as mentioned in the optional section of #3.
iii. Addtinal integration with AWS/Azure/GCP in place of Informatica to implemnt this project. just SRC to EDW_STG logic to be implemneted as EDW_STG to EDW data pipelines are already in place as mentioned in #ii above.

<ENDOFDOCUMENT>
