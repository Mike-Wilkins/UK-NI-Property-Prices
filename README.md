# UK-NI-Property-Prices

## Table of Contents
* [Business Requirements](#business-requirements)
* [Data Source](#data-source)
* [Objectives](#objectives)
* [Data Exploration Notes](#data-exploration-notes)
* [Data Cleaning](#data-cleaning)
* [Test the Dataset](#test-the-dataset)
* [Power BI Visualisation](#power-bi-visualisation)
* [Analysis](#analysis)

## Business Requirements
Our client has requested a dashboard detailing residential property sales over the last 20+ years. The dashboard should address the following:
- We would like to see a visualisation of the property trend prices across numerous years and have the ability to dynamically focus in on selected time periods.
- The visualisation should provide a means of filtering trends in data by categorizing the regions by Country, County, City, Borough and Town.
- We would like to see a breakdown of the property types (Detached, Semi-detached, Terraced and Flats) for each selected time period/region.
- The dashboard should clearly show the percentage property price increase between each time period.

## Data Source
- https://www.kaggle.com/datasets/fabianwhitaker/uk-regional-property-data
- The data source for this project is provided by Kaggle and represents regional property sales data in the UK and NI across various attributes between 1995 and 2022.
- Orignal data is taken from the UK Government House Price Index (HPI).

## Objectives
- Load the CSV file into SQL Server (SSMS)
- Explore the data provided by the UK Government House Price Index (HPI)
- Clean the data with SQL
- Test the data with SQL
- Visualise the data in Power BI
- Generate the findings based on the insights
  
## Data Exploration Notes
- We have more data than we need, so some of these columns would need to be removed.
- The table contains a column RegionName which lists the region name regardless of whether it is a country, county, borough, town or city. A new column RegionType will need to be created to categorise this data in accordance with the client's requirements.
- We will need to implement a dynamic percentage increase calculation as part of the dashboard using a DAX measure.

## Data Cleaning
The aim is to refine our dataset to ensure it is structured and ready for analysis.

The cleaned data should meet the following criteria and constraints:
- A new table needs to be created including only relevant columns required for the dashboard.
- A new RegionType column should be added to the dataset.
- All data types should be appropriate for the contents of each column.

**1. Create a modified records dataset including only relevant columns:**

``` SQL
SELECT 
	[Date],
	RegionName,
	AveragePrice,
	SalesVolume,
	DetachedPrice,
	SemiDetachedPrice,
	TerracedPrice,
	FlatPrice
INTO 
	UK_NI_Regional_Property_Prices
FROM dbo.[UK-HPI-full-file-2022-08]
```
**2. Create new column RegionType:**

``` SQL
ALTER TABLE UK_NI_Regional_Property_Prices
ADD RegionType varchar(100);
```
**3. Populate RegionType column with row category:**

``` SQL
UPDATE Regional_Property_Prices
SET RegionType = 'City'
WHERE 
	RegionName = 'Bath' OR
	RegionName = 'Birmingham' OR
	RegionName = 'Bradford' OR
	RegionName = 'Brighton & Hove' OR
	RegionName = 'Bristol' OR
	RegionName = 'Cambridge' OR

-- Add additional RegionName here
```
## Test the dataset
**1. All columns within the new dataset should have approproate data types.**

``` SQL
SELECT 
	COLUMN_NAME,
	DATA_TYPE
FROM 
	INFORMATION_SCHEMA.COLUMNS
WHERE 
	TABLE_NAME = 'Regional_Property_Prices'
```

| COLUMN_NAME |	DATA_TYPE |

Date	date
RegionName	nvarchar
AveragePrice	float
SalesVolume	float
DetachedPrice	float
SemiDetachedPrice	float
TerracedPrice	float
FlatPrice	float
RegionType	nvarchar

## Power Bi Visualisation



https://github.com/user-attachments/assets/c16b03d7-9549-4285-9840-7d93abe753be



## Analysis
