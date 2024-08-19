# NHL 2008-2024 data ELT and Analysis

## Overview

Goals for the project:
* Find comprehensive datasets for NHL games and players
* Extract, load and transform the data using Azure Synapse Analytics
* Ingest data for PowerBI analysis in Microsoft Fabric
* Build an analytics dashboard in Power BI

## Data Source

All datasets are from https://moneypuck.com/data.htm

## ELT Pipeline

![image](https://github.com/user-attachments/assets/aa5a5eef-ec3c-4b3d-b90e-050600b24801)

The actual Azure Synapse Analytics pipelines are provided as JSON-templates in the repository:

- NHL Games Pipeline: extracts the dataset for all games from the period 2008-2024 and saves them to Azure Data Lake Gen 2
- NHL Players Pipeline: extracts the individual player datasets for all players from the period 2008-2024 Azure Data Lake Gen 2

After that, the datasets are further transformed and cleaned in the Azure Synapse notebooks and data is modelled according to star schemas.

Games schema:

![image](https://github.com/user-attachments/assets/d40af9cc-0bdb-4d02-ae12-b921577e3725)

Players schema:

![image](https://github.com/user-attachments/assets/076a63ac-1cd7-4871-a2fa-4c5e19b26d2a)

Lastly, data is written to an SQL data warehouse in Azure.

After that, the data is ready to be used in analytics.

## Analytics dashboard in Power BI

Power BI was used to create analytics about games, teams, goals and penalties. Some example pages below:

![image](https://github.com/user-attachments/assets/81de9986-e3f1-428a-96e7-20e246cdb27c)

![image](https://github.com/user-attachments/assets/f657fc72-c5d7-44cc-a2fb-f26dcab44ca6)

![image](https://github.com/user-attachments/assets/20af85e1-ede5-41d5-9277-be059f17fb79)

![image](https://github.com/user-attachments/assets/35bae7f2-e15c-4895-9d31-84560a11a27d)
