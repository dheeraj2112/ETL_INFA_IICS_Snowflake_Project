**Project Summary: Data Integration and Analytics with IICS and Snowflake**

**Project Title: Integrated Data Pipelines for Analytics and Reporting**

1) Project Overview and objective

The goal of a data warehouse project is to consolidate data from various sources into a centralized repository for analysis and reporting. This enhances decision-making capabilities by providing a holistic view of the organization's data.

The end-to-end data pipelines flow represents the complete data journey, from its source, whether on-premise, in the cloud or otherwise, to its final display in Enterprose Data Warehouse to dashboards and reports thereafter. It starts with the collection of data from various sources, such as transactional databases or CRM systems, through to the presentation of intuitive reports or visualisations. This process includes transforming and cleansing the data using ETL (Extract, Transform, Load) techniques in a centralised Data Warehouse project.

The goal of this project is to design and implement robust data integration pipelines that enables Analytics and Reporting for the oragnization. By leveraging IICS for ETL (Extract, Transform, Load) processes and Snowflake as the cloud data warehouse, the project aimed to improve decision-making through timely access to consolidated data.

1.1) Pre-requisite: 

i. Valid IICS and Snowflake Accounts 

ii. Secure Agent for IICS configured and the agent is up/running

iii. On-Prem Oracle db (configured as an ODBC connection in IICS) with HR schema objects. The objects with data can be created from #2 mentioned below, if not available already.

1.2) Reference Architecture Diagram

![image](https://github.com/user-attachments/assets/5e96470f-1078-4b3e-8a76-371978be6cb1)

2) Source and Target 

Source: Source is Oracle on-prem HR schema. The script can be used to generate that data set, if not available handy. https://github.com/dheeraj2112/INFA_IICS_Snowflake_Project/blob/a69bf3a16396e40a7a6fa0aedafebf485ddfecd8/HR%20Objects%20and%20Data%20For%20Live%20SQL.sql

Target: Target is Snowflake having both EDW_STG and EDW Layers. The DDLs can be found in the repo. https://github.com/dheeraj2112/INFA_IICS_Snowflake_Project/blob/a69bf3a16396e40a7a6fa0aedafebf485ddfecd8/IICS_ORA_SNFLK_EDW_DDL.sql

3) ETL/ELT Data Flows using Mappings and Mapping Tasks

i. Source (Oracle) to EDW_STG (Snowflake) : Using SCD Type-1 (Optinally can be SCD Type-4 with addtional History tables)

![image](https://github.com/user-attachments/assets/7b6096af-2192-4b16-b52e-1bb9bfcc2ecd)

ii. EDW_STG (Snowflake) to EDW(Snowflake) : Using SCD Type-2

![image](https://github.com/user-attachments/assets/8ba17954-e11e-44a2-8572-07d788e127c3)

iii. Orchestration and scheduling : Using IICS/Taskflows or Snowflake Tasks as per needed schedule.

**SRC to STG**

![image](https://github.com/user-attachments/assets/e63a7caf-5ff8-490f-88c6-dbfacf91a887)

**STG to EDW**

![image](https://github.com/user-attachments/assets/ccdf50f0-2b15-49ad-95f7-a77203714916)

**ALL IN ONE TASKFLOW (Using Sub-Task flow to combine SRC to STG and STG to EDW Taskflows into one single WF)**

![image](https://github.com/user-attachments/assets/6362056c-f85f-48a6-8eb9-735fc1ffa098)


**Optinal:** EDW_STG to EDW data pipelines can be implemented using Snowflake features itself using Streams, Tasks, Stored Proc etc. The code can be found here. 

https://github.com/dheeraj2112/INFA_IICS_Snowflake_Project/blob/a69bf3a16396e40a7a6fa0aedafebf485ddfecd8/EDW%20STG%20to%20EDW%20Pipelines%20using%20Snowflake%20based%20on%20ORA%20HR%20DB.sql

4) ETL Code using IICS

**Pre-requisite: Valid IICS account and an agent with DIS service should be up and running. Once this is already in place then re-configure/re-point the connections (DB, Flat File and APIs etc) to your enviroment accordingly. Once these are setup properly then import the ETL code from repo to IICS Org.**

The ETL Code can be found in the repo which can be imported in IICS.Once the import is sucessfull then the corresponding project and folders will be appear as mentioned below.  

https://github.com/dheeraj2112/ETL_INFA_IICS_Snowflake_Project/blob/master/Enterprise%20Data%20Warehouse%20Export%204_Octtober_2024.zip

**Project and Folders for STG and EDW(as well as the Extracts generation) Jobs:**

SRC to EDW_STG jobs: Enterprise Data Warehouse\EDW_STG

EDW_STG to EDW jobs: Enterprise Data Warehouse\EDW

EDW_EXTR jobs: Enterprise Data Warehouse\EDW_EXTR

Note: ODBC connection has been used from IICS to Snowflake  but if you have the JDBC connector feel free to re-point the Snowflake database and other connections accordingly.

5) Analysis and Reporting (ETL Code)
   
Views or Dynamic tables can be leveraged accordingly for the analytics and reporting or visualization needs. This can be done from IICS ETL job or Snowflake specific features as per need.

https://github.com/dheeraj2112/INFA_IICS_Snowflake_Project/blob/a69bf3a16396e40a7a6fa0aedafebf485ddfecd8/EDW_EXTR%20Views%20and%20Dynamic%20Tables%20for%20Reporting.sql

6) Addtionally, a Snowflake quickstart on **Harness the Power of Snowflake with Informatica Intelligent Data Management Cloud** can be followed whoever wants to do some specific hands on Snowflake with Informatica Cloud.

https://quickstarts.snowflake.com/guide/harness_the_power_of_snowflake_with_informatica_idmc/index.html?index=..%2F..index#0

7) Next Steps -->

i. Enchance the existing EDW_STG to EDW pipelines in ELT(Extract, Load, Transform) mode within IICS.

ii.Incremental/CDC logic handling ( either having some audit framework or IICS specific CDC handling features with { SETVARIABLE option / in-built $LastRunDate or $LastRunTime variables})

iii. Build the EDW_STG to EDW data pipelines using Snowflake features as mentioned in the optional section of #3.

iv. Additional integration with AWS/Azure/GCP in place of Informatica to implement this project. Just SRC to EDW_STG data pipelines logic to be implemented as EDW_STG to EDW data pipelines are already in place within Snowflake as mentioned in point #ii above.


**ENDOFDOCUMENT**
