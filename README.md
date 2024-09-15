# Unpacking 16 Years of NHL Data

## 1. Introduction

This project aims to analyze NHL games and player data. The focus is on sourcing comprehensive datasets, primarily from NHL seasons 2008-2024, and using Azure Synapse Analytics to extract, load, and transform the data. In the final step, Power BI is used for building an interactive analytics dashboard to visualize key insights and trends.

All datasets are from https://moneypuck.com/data.htm

## 2. Tech Stack

My tech stack for this project:

Languages and libraries

* Python
* PySpark

Tools

* Azure Synapse Analytics
* Power BI

## 3. Data Pipeline Architecture

The actual pipeline was very simple in this case. Azure Synapse Analytics (ASA) is used in all phases except the data visualization. 

First, a 'Copy Data' activity is used in ASA to get the data via a HTTP request from Moneypuck. Additionally, some supplemental data was compiled from Wikipedia.  

Second, the raw data is loaded to Azure Data Lake Gen 2.

Third, the ASA's Notebook functionality is used to clean the data, transform it and write into SQL tables.

Fourth, Power BI reads the data from SQL tables and is used to create the final visualizations.

![image](https://github.com/user-attachments/assets/aa5a5eef-ec3c-4b3d-b90e-050600b24801)

The actual Azure Synapse Analytics pipelines are provided as JSON-templates in the repository:

- NHL Games Pipeline: extracts the dataset for all games from the period 2008-2024 and saves them to Azure Data Lake Gen 2
- NHL Players Pipeline: extracts the individual player datasets for all players from the period 2008-2024 Azure Data Lake Gen 2

## 5. Extracting Data

This part was actually extremely easy. Azure Synapse Analytics' Copy Data functionality allows you to extract data by using a HTTP GET request by creating a REST-linked service and simply copying the data into a specified sink (for example, Azure Data Lake Gen2 or dozens of other options). After sinking the data, it can be further transformed with a Dataflow-activity or using a Synapse Notebook (which is very similar to a Jupyter Notebook).

## 6. Transforming Data

In this case, I decided to use a Notebook to further clean and transform the data. PySpark (which is the Python API for Spark) is an extremely convenient way of transforming data via python/pandas-like code.

First, all needed data was read into separate dataframes.

Team names were cleaned, e.g. a team's name or abbreviation could appear in many different forms ('L.A.', 'L.A' or 'LAK to name a few examples).

Column names were cast to proper types in order to make sure that calculation of numeric metrics was possible later on.

Some data quality checks were implemented to reveal duplicate rows, missing values and ensuring the schema was as expected. In this project, I used the star schema principle to model the data.

Games schema:

![image](https://github.com/user-attachments/assets/d40af9cc-0bdb-4d02-ae12-b921577e3725)

Players schema:

![image](https://github.com/user-attachments/assets/076a63ac-1cd7-4871-a2fa-4c5e19b26d2a)

You can see all of the details in code by checking nhl_games_notebook.ipynb and nhl_players_notebook.ipynb 

## 7. Loading Data

Lastly, data is written to an SQL data warehouse and then it is ready to be used for analytics. Luckily this is also just one line of code when using the Spark SQL Analytics libraries.

## 8. Results and Analysis

Power BI was used to create analytics about games, teams, goals and penalties. Some example pages below:

![image](https://github.com/user-attachments/assets/81de9986-e3f1-428a-96e7-20e246cdb27c)

![image](https://github.com/user-attachments/assets/f657fc72-c5d7-44cc-a2fb-f26dcab44ca6)

![image](https://github.com/user-attachments/assets/20af85e1-ede5-41d5-9277-be059f17fb79)

![image](https://github.com/user-attachments/assets/35bae7f2-e15c-4895-9d31-84560a11a27d)

## 9. Future Work
