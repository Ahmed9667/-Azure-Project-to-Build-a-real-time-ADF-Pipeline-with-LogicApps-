# Project Description

## Business Overview:

In the era of analyzing massive data volumes every second, the purpose of a real-time data pipeline has become a central need. Organizations that are capable of creating their data infrastructure on real-time data, gain a decisive competitive advantage, enabling unprecedented success and differentiation from competitors. 

However, collecting and processing data in real-time, and building robust data pipelines to handle this, is a complex challenge. Leveraging cloud services can address many of these challenges, offering scalable and cost-effective solutions. A comprehensive real-time data pipeline is the ideal solution to analyze data as it is generated. By incorporating automation, organizations can achieve cost efficiency, resource optimization, and improved processing speed. This automated approach allows large volumes of streaming data to be managed efficiently without manual intervention.

# Key features:

1- Real-time Data Extraction: Azure-based data pipeline designed to ingest data from the Azure SQL Database in real-time, capturing only newly added records at a particular timestamp. This enables immediate availability of the latest added data for analysis and processing in real-time.

2- Automation: Triggers are configured to automatically detect and retrieve only newly added records from the database without manual intervention. This setup ensures efficient processing by filtering out previously ingested data.

3- Cost Efficiency: Storing only the necessary incremental data, rather than fetching full datasets, it basically keeps storage costs low and ensures more efficient use of space.

4- The execution of retrieving only newly added records from the entire database, the pipeline ensures efficient data processing and resource usage, reducing computational costs.

# Aim:

This project aims to analyze real-time sensor water data collected in European countries using Azure Services. The primary goal is to process data as soon as it becomes available. A comprehensive set of Azure services and triggers ensures that only new real-time data from the entire Azure SQL Database is available for further processing. The project upholds real-time data pipeline standards and efficiently manages the retrieval of newly added records from the Azure SQL Database. The newly added records are automatically loaded into Azure Storage accounts, where they become immediately available for further processing. This setup uses an automated trigger that listens for new data events in the source storage container. As soon as new data becomes available in the source container, it is automatically copied to the destination storage container, which serves as the input for downstream processing tasks. This real-time data movement ensures a seamless and efficient flow of information, eliminating the need for manual intervention and enabling continuous, uninterrupted processing.

# Tech Stack:

- Programming: SQL, Scala

- Services: Azure Managed SQL Server Database, Azure Logic app, Azure Blob Storage, Azure Data Factory, Azure Data Lake Storage Gen2, Azure Databricks, Power BI

  
![image](https://github.com/user-attachments/assets/7975fcf9-520b-4166-a1d1-63bd08346f77)

# Data Description:

The dataset provides a comprehensive view of aggregated water sensor data, containing 32 columns and over one million rows collected across multiple European countries over several years. It includes detailed information on various aspects, such as country, water body category, determinands measured, and concentration levels (minimum, maximum, mean, and median) of each determinand at specific timestamps. Additionally, it tracks the number of quality samples conducted out of the total samples for each observation. With data collection ongoing at each timestamp, each recorded value is associated with a specific country, capturing the concentration of different determinands across various monitoring sites.

In this project, only newly added records are fetched and processed in real time from the entire Azure SQL database. This approach ensures that only the most recent records are generated and processed, without redundantly fetching existing data again.

# Approach:

- The raw data was initially loaded into an Azure SQL Database table using SQL Server Management Studio, and a SQL query was executed to create an auto-incremented unique column.

- A comprehensive workflow was designed in Logic Apps to fetch only newly added records which then upload them to Azure Blob Storage. The recurrence trigger action was added to the workflow to orchestrate the execution without manual intervention.

- Azure Blob Storage was set up to store raw data from an Azure-managed SQL Server database, while an Azure Data Lake Storage Gen2 account with a hierarchical namespace was created as the source for further pipeline processing.

- An Azure Data Factory instance was created and a copy pipeline was developed. The Storage event triggers were configured on this pipeline to automatically copy new data from the blob container to the ADLS container as soon as it lands.

- A "Live" folder was created following Azure DevOps practices, containing all notebooks for the medallion architecture in the Azure Databricks workspace.

- A notebook activity pipeline was set up in Azure Data Factory to orchestrate the bronze, silver, and gold notebooks sequentially. A storage event trigger was added to this pipeline, initiating it whenever new data arrives in the ADLS container in real-time.

- Cleaned newly added records were retrieved from the gold table, and a connection was established to load this data to Power BI. During the next pipeline run, Power BI refreshes data to retrieve only newly added records from the gold table in real time.

 
