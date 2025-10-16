# 📊 Airlines Delayed Flights Project

## Table of Contents
---
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Preparation](#Data-Preparation)
- [Data Analysis](#Data-Analysis)
- [Results](#Results)
- [Key Learning](#Key-Learning)

---

### Project Overview

This data analysis project aims to provide insights about airlines delayed flights and performance in 2008. By analyzing various aspects of the flights data, we seek to identify trends, make data-driven recommendations, and gain a deeper understanding of every the carrier's and airport's performance.

### Data Sources

Delayed Flights Data: The primary dataset used for this analysis is the "DelayedFlights.csv" file, containing detailed information about each flight made by every the carrier.
  - [Download here](https://www.kaggle.com/datasets/giovamata/airlinedelaycauses) or from attachments

 <br />

### Tools

1. Applications
- Anaconda (Jupyter Notebook) - Data Exploration and Cleaning by Python/Pandas
  - [Download here](https://www.anaconda.com/)
- PowerBI - Creating reports
  - [Download here](https://www.microsoft.com/en-us/power-platform/products/power-bi/downloads)

 <br />
  
2. AI 
- [Chatgpt](https://chatgpt.com): help me with background design 
- [LMArena](https://lmarena.ai): help me with analysis suggestions

 <br />

3. Desing 
- [Coolors](https://coolors.co): help me to find a suitable color palette (Deep Ocean Blue)
- [Flaticon](https://www.flaticon.com): help me to find a suitable icon for Bookmarks and Navigation

 <br />

### Data Preparation

Collecting Related Data:
- I got 2 more files for Airports & Carriers containing more details about their codes, region and names to help me analysis data.

Python (By using Pandas): Explore and cleaning the data, I focused on three things: -

1 - Data Understanding (Types, measures and each column meaning)

2 - Check duplication and null values and replace them with suitable values by:

  - Replace all null values in times with "0" to keep the data has no time
  - Replace all null values in tail number with "Unknown" to keep the data has no numbers

3 - Minimize data storage as can as possible by:
  - Change data type from Float to Integer because all times are measured by (minutes) 

 <br />

### Data Analysis

- **Include some interesting code/features worked with Python**

1 - Import Pandas
```python
import pandas as pd
```
2 - Import DelayedFlights Dataset & Read it
```python
df = pd.read_csv("DelayedFlights.csv")
df
```
3 - Rename the first column 'unnamed' by 'ID' & Order by Asc
```python
df = df.rename(columns={"Unnamed: 0": "ID"})
df = df.sort_values(by="ID", ascending=True)
df
```

4 - Get Dataset Info Then Change Type
```python
df.info()
pd.set_option("display.max_columns", None) 
df.head(10)

df["DepTime"] = df["DepTime"].astype("Int64")
df["ArrTime"] = df["ArrTime"].astype("Int64")
df["TaxiIn"] = df["TaxiIn"].astype("Int64")
df["TaxiOut"] = df["TaxiOut"].astype("Int64")
df["ActualElapsedTime"] = df["ActualElapsedTime"].astype("Int64")
df["CRSElapsedTime"] = df["CRSElapsedTime"].astype("Int64")
df["AirTime"] = df["AirTime"].astype("Int64")
df["ArrDelay"] = df["ArrDelay"].astype("Int64")
df["DepDelay"] = df["DepDelay"].astype("Int64")
df["CarrierDelay"] = df["CarrierDelay"].astype("Int64")
df["WeatherDelay"] = df["WeatherDelay"].astype("Int64")
df["NASDelay"] = df["NASDelay"].astype("Int64")
df["SecurityDelay"] = df["SecurityDelay"].astype("Int64")
df["LateAircraftDelay"] = df["LateAircraftDelay"].astype("Int64")
```
5 - Check Duplicated Values
```python
print(df.duplicated().sum())
```

6 - Check Null Values
```python
print(df.isnull().sum())
```
7 - Fill All Null Values
```python
df.fillna({"ArrTime":0}, inplace = True)
df.fillna({"ActualElapsedTime":0}, inplace = True)
df.fillna({"CRSElapsedTime":0}, inplace = True)
df.fillna({"AirTime":0}, inplace = True)
df.fillna({"ArrDelay":0}, inplace = True)
df.fillna({"TaxiIn":0}, inplace = True)
df.fillna({"TaxiOut":0}, inplace = True)
df.fillna({"CarrierDelay":0}, inplace = True)
df.fillna({"WeatherDelay":0}, inplace = True)
df.fillna({"NASDelay":0}, inplace = True)
df.fillna({"SecurityDelay":0}, inplace = True)
df.fillna({"LateAircraftDelay":0}, inplace = True)
df.fillna({"TailNum":"Unknown"}, inplace = True)

print(df.isnull().sum())
```
8 - Export Cleaned CSV File
```python
df.to_csv('CleanedDelayedFlights.csv', index=False)
```

 <br />

- **Power BI: Data modeling, DAX measures, and building interactive dashboards**

Data Modeling:
- Make a star schema to improve analysis performance

DAX Measures:
```dax
Average Air Time = AVERAGE(FactDelayedFlights[AirTime])
```
```dax
Average Distance = AVERAGE(FactDelayedFlights[Distance])
```
```dax
Average TaxiIn = AVERAGE(FactDelayedFlights[TaxiIn])
```
```dax
Average TaxiOut = AVERAGE(FactDelayedFlights[TaxiOut])
```
```dax
Cancellation Rate = DIVIDE([Total Cancelled Flights],[Total Flights])
```
```dax
Diversion Rate = DIVIDE([Total Diverted Flights], [Total Flights])
```
```dax
Late Aircraft Delay Flights = CALCULATE([Total Flights], FactDelayedFlights[LateAircraftDelay]<> 0)
```
```dax
NAS Delay Flights = CALCULATE([Total Flights], FactDelayedFlights[NASDelay]<> 0)
```
```dax
Number of Airport = DISTINCTCOUNT(DimAirport[Airport Code])
```
```dax
Number of Carriers = DISTINCTCOUNT(DimCarrier[Carrier Code])
```
```dax
Security Delay Flights = CALCULATE([Total Flights], FactDelayedFlights[SecurityDelay]<> 0)
```
```dax
Total Air Time = SUM(FactDelayedFlights[AirTime])
```
```dax
Total Cancelled Flights = SUM(FactDelayedFlights[Cancelled])
```
```dax
Total Distance = SUM(FactDelayedFlights[Distance])
```
```dax
Total Diverted Flights = SUM(FactDelayedFlights[Diverted])
```
```dax
Total Flights = COUNT(FactDelayedFlights[ID])
```
```dax
Weather Delay Flights = CALCULATE([Total Flights], FactDelayedFlights[WeatherDelay]<> 0)
```

Reporting:
1. Make a star schema to improve analysis performance
2. Make a dimension for Date using a simple M language code
3. Make 5 reports to get valuable insights from data

 <br />

### Results

The analysis results are summarized as follows:
1. The highest carrier and airport in flights are Southwest Airlines (377602) and Hartsfield-Jackson Atlanta International Airport (132158).
2. December is the most mounth has the flights (204792 Flights).
3. The highest carrier and airport in late aircraft delay flights are Southwest Airlines (164080) and Chicago O'Hare International Airport (54515).
4. The highest carrier and airport in cancelled flights American Eagle (104) and Chicago O'Hare International Airport (86).
5. The highest carrier and airport in cancellation rate is Pinnacle Airlines (29.76%) and Minot International Airport (27.41%).
6. December is the most mounth has the cancelled flights (481).
7. The highest carrier and airport in diverted flights are Southwest Airlines (1386) and Chicago O'Hare International Airport (443).
9. December is the most mounth has the diverted flights (1403).
10. The highest carrier and airport in diversion rate flights are Aloha (25.58%) and Ralph Wien Memorial Airport (23.29%).
11. June is the most mounth has total air time and distance.
12. Southwest Airlines is the most carrier has total air time and distance.



### Key Learning

💡 Combining Python for heavy data processing with Power BI for interactive dashboards creates a powerful working.
