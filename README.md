# Airplane Crashes (1908-2009)

## Project Overview
**Objectives**: The aim of this project was to implement an end-to-end analytics solution using Microsoft Fabric to ingest, transform, model, and visualize aircraft crashes data. The solution features various Microsoft Fabric artifacts, such as Lakehouses, Data Warehouses, Dataflows, Pipelines, and Semantic Models, as well as a Power BI report.

**Context**: This work was developed throughout 2024-2025 as part of a subject deliverable during my master's degree. Each student was asked to implement a BI solution in Microsoft Fabric using a dataset of their choice. While exploring datasets in Kaggle, I eventually came across the airplane crashes dataset, which immediately drew me in.

**Data Source**: A .csv file containing over 5000 rows of aircraft crash accidents involving civil, commercial and military transport worldwide from 1908 to 2009. While the dataset was originally hosted by Open Data by Socrata, it can currently be downloaded in platforms such as Kaggle. The version used in this project can be accessed here: https://www.kaggle.com/datasets/saurograndi/airplane-crashes-since-1908. The dataset contains essential details of individual crashes, including their date, time, location, operator, flight route, aircraft type/model & respective design year, number of people aboard, in-flight fatalities, and ground fatalities.

**Workflow Summary**: An overview of the project workflow can be seen in the image below.
![Workflow](https://github.com/ThiagoSKM/airplane-crashes/blob/main/assets/workflow-img.png)

## Technology Stack
- DAX
- Fabric Data Factory (Pipelines, Dataflows Gen2, and Copy Jobs)
- OneLake
- Power BI semantic models & reports
- Power Query
- SQL
- Synapse Data Warehouse

## Core Developments
**Dataflows Gen2** were a fundamental element in the ETL process, enabling the manipulation and transformation of source data and serving as the foundation for the data cleaning, preparing and modeling stages. Key changes implemented through the dataflows include:
- Addressing missing values in variables through a case-to-case analysis and data imputation methods.
- Fixing inconsistencies in the source data, which mainly consisted of formatting & semantic discrepancies, misspellings, and extra characters that were likely inserted by mistake.
- Designing the Fact and Dimension tables for the dimensional model through the definition of business and surrogate keys, selection of relevant columns for each table, and creation of new, insightful columns based on the information available in existing columns (e.g. creation of a "aircraft_manufacturer" column based on the information present in the "aircraft_model" column, possible through parsing techniques and additional research to ensure accurate correspondence).

**Data Pipelines** allowed for data orchestration and workflow automation within the Fabric environment. Within the project, they served the purpose of:
- Moving data in between environments.
- Performing data quality checks on the model tables and storing the results.
- Storing lookup test results in a lookup table.
- Notify updates regarding the pipeline execution status via email.
- Streamlining the workflow through the creation of a single, unified pipeline.
![Unified Pipeline](https://github.com/ThiagoSKM/airplane-crashes/blob/main/assets/pl_unified.png)

**Data Warehouse**: A Data Warehouse (DW) consists of a central repository of information that stores cleansed transactional data, in a form that is ready to be used in analytical processing activities. In this project, the Kimball strategy (also known as the Data Mart strategy) was adopted, with the development of the DW being supported by Kimball’s four-step process: 1) select the business process to model; 2) declare the grain; 3) identify the dimensions; 4) identify the facts. Additionally, the DW followed a star schema comprised of six Dimension tables and one Fact table, as illustrated in the image below.
![DW Schema](https://github.com/ThiagoSKM/airplane-crashes/blob/main/assets/dw_schema.png)

**Semantic Model**: Semantic models provide a shared, simplified, business-friendly view of complex data, which helps users to more easily interact with data. In this project, they essentially served as a bridge between the data stored in the DW and the developed dashboards and reports. The design process of the semantic model was as follows:
- Relationships between fact and dimension tables were established by linking the FKs from the fact table with the SKs from the dimension tables.
- Attribute titles were renamed using a friendlier, business-like terminology.
- Attribute visibility and formatting settings were adjusted.
- Hierarchies were created and defined for certain attributes.
- Calculated measures and KPI were created using DAX, supporting the analytical exploration of data.
![Semantic Model](https://github.com/ThiagoSKM/airplane-crashes/blob/main/assets/semantic_model.png)

## Power BI Report
Using the designed semantic model as the data source connection, a Power BI report was developed to enable the visual exploration of key analytical insights regarding the airplane crashes data. Each page of the report aimed to address specific business questions defined at the start of the project. The report pages and their related business questions are presented below.

### Page 1 - Airplane Crashes Across Time

![Page 1](https://github.com/ThiagoSKM/airplane-crashes/blob/main/assets/pg1.png)
**Business Questions:**
- BQ1 - “How has the number of crashes evolved every year?”
- BQ2 - “How does the in-flight fatality rate per passengers aboard of each year compare to the specified target rate?”
- BQ3 - “How has the number of ground & in-flight fatalities evolved every year?”

- ### Page 2 - Airplane Models

![Page 2](https://github.com/ThiagoSKM/airplane-crashes/blob/main/assets/pg2.png)
**Business Questions:**
- BQ6 - “What are the top 10 aircraft models with the highest crash occurrences and the top 10 with the highest fatalities?”
- BQ7 - “What are the top 10 aircraft manufacturers with the highest crash occurrences and the top 10 with the highest fatalities?”
- BQ8 - “What is the number of recorded crash occurrences and fatalities by design year of aircraft model?”
- BQ9 - “What are the top 10 aircraft model design years with the highest crash occurrences and the top 10 with the highest fatalities?”
- BQ10 - “What is the number of crashes, passengers aboard, in-flight fatalities, ground fatalities & total fatalities by aircraft model category?”

### Page 3 - Operators

![Page 3](https://github.com/ThiagoSKM/airplane-crashes/blob/main/assets/pg3.png)
**Business Questions:**
- BQ11 - “What is the number of crashes & fatalities by operator type?”
- BQ12 - “What is the number of crashes, passengers aboard, in-flight fatalities, ground fatalities & total fatalities by operator?”
- BQ13 - “What is the number of crashes, total fatalities & passengers aboard by operator country?”
- BQ14 - “What is the number of crashes, passengers aboard, in-flight fatalities, ground fatalities & total fatalities by operator alliance & group?”

### Page 4 - Flight Routes

![Page 4](https://github.com/ThiagoSKM/airplane-crashes/blob/main/assets/pg4.png)
**Business Questions:**
- BQ15 - “What is the number of crashes & fatalities by flight type?”
- BQ16 - “What is the number of crashes & fatalities by flight purpose?”
- BQ17 - “What is the number of crashes, passengers aboard, in-flight fatalities, ground fatalities & total fatalities by flight route?”

### Page 5 - Locations

![Page 5](https://github.com/ThiagoSKM/airplane-crashes/blob/main/assets/pg5.png)
**Business Questions:**
- BQ18 - “What are the top 20 countries with the highest crash occurrences and the top 20 with the highest fatalities?”
- BQ19 - “What is the number of crashes, passengers aboard, in-flight fatalities, ground fatalities & total fatalities by country, state, city and location?”
- BQ20 - “How do crash occurrences by country look like in a visual map?”

### Page 6 - Locations Across Time

![Page 6](https://github.com/ThiagoSKM/airplane-crashes/blob/main/assets/pg6.png)
**Business Questions:**
- BQ21 - “How do crashes and fatalities by location evolve across the years?”

## Key Takeaways
Working on this project allowed me to learn more about what generally goes into the development of a BI project, as well as how Power BI and Microsoft Fabric tools can be leveraged to build a robust BI solution including both a dedicated Data Warehouse environment and a reporting layer to present key analytical insights. 

Furthermore, many of the learnings I extracted from this project stem from the difficulties encountered throughout its development. The airplane crashes dataset proved to be much more difficult to handle than initially expected. Some aspects regarding its data quality were quite poor, and the large number of inconsistencies required me to spend a significant amount of time transforming the dataset to ensure quality and consistency before designing the dimension and fact tables. On the bright side, this meant I had to explore different tools, resources and research to come up with efficient ways to address these challenges. 

Regarding dashboarding & visual reporting, studying and experimenting with different layout and design choices improved my practical understanding of visual reporting principles and applications. 
