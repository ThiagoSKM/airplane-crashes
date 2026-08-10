# Airplane Crashes (1908-2009)

## Project Overview
**Objectives**: The aim of this project was to implement an end-to-end analytics solution using Microsoft Fabric to ingest, transform, model, and visualize aircraft crashes data. The solution features various Microsoft Fabric artifacts, such as Lakehouses, Data Warehouses, Dataflows, Pipelines, and Semantic Models, as well as a Power BI report.

**Context**: This work was developed throughout 2024-2025 as part of a subject deliverable during my master's degree. Each student was asked to implement a BI solution in Microsoft Fabric using a dataset of their choice. While exploring datasets in Kaggle, I eventually came across the airplane crashes dataset, which immediately drew me in.

**Data Source**: A .csv file containing over 5000 rows of aircraft crash accidents involving civil, commercial and military transport worldwide from 1908 to 2009. While the dataset was originally hosted by Open Data by Socrata, it can currently be downloaded in platforms such as Kaggle. The dataset contains essential details of individual crashes, including their date, time, location, operator, flight route, aircraft type/model & respective design year, number of people aboard, in-flight fatalities, and ground fatalities.

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
**Dataflows Gen2**: Dataflows Gen2 were a fundamental element in the ETL process, enabling the manipulation and transformation of source data and serving as the foundation for the data cleaning, preparing and modeling stages. Key changes implemented through the dataflows include:
- Addressing missing values in variables through a case-to-case analysis and data imputation methods.
- Fixing inconsistencies in the source data, which mainly consisted of formatting & semantic discrepancies, misspellings, and extra characters that were likely inserted by mistake.
- Designing the Fact and Dimension tables for the dimensional model through the definition of business and surrogate keys, selection of relevant columns for each table, and creation of new, insightful columns based on the information available in existing columns (e.g. creation of a "aircraft_manufacturer" column based on the information present in the "aircraft_model" column, possible through parsing techniques and additional research to ensure accurate correspondence).

**Data Pipelines**:

**Data Warehouse**:

**Semantic Model**:

## Power BI Report

## Key Insights
- From 1908 to 2009, there has been an overall increase in airplane crashes. This increase has recorded several fluctuations along its evolution, with the period from the 70s to the 90s recording the highest numbers and the 00s presenting a relatively sharp decline.
