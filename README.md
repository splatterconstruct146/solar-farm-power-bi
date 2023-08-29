# solar_farm_power_bi
A Power BI report used to analyze the daily yield and other metrics at a solar farm I designed/constructed.

## Motivation
This report was created as a response to the company board wanting to be able to view the output and revenue of the solar farm without having to use the farm control and monitoring tools.

Note that this is no substitute for an actual plant SCADA system; it is merely just an additional avenue to view plant related information.

## Shortcomings
Since this report takes data from csv files the information shown will not be real-time. This isn't meant to be a dashboard nor a substitute for one. 

Additionally the report is bottlenecked to the information that's available in the csv files in the first place. In this case only a few days worth of information and a few metrics were obtained. 

## Files 
The files found in this repository and their descriptions are as follows:
1. InverterData.xlsx: Dimension table holding information regarding each inverter.
2. InverterOutput.xlsx: Fact table holding important plant information like yield, hourly output etc.
3. data_cleaning.pbix: A separate Power BI file made just for the data cleaning and transformation step. In reality the working files could be suppressed from being used in the report to reduce computing resource, but ultimately separating them is neater.
4. solar_farm_reporting.pbix: Main Power BI report. View the screenshot folder for more screenshots.


## Sample Screenshots
![image 1 - summary](https://github.com/splatterconstruct146/solar_farm_power_bi/assets/135209633/0c873fc3-0184-43b2-9b59-519dedefc1d1)
Image 1: Summary page of the report.

![image 5 - daily profile (slicer)](https://github.com/splatterconstruct146/solar_farm_power_bi/assets/135209633/8ff9d784-4d00-45b8-8983-742584213657)
Image 2: A page showing the daily profile of the farm. Users can slice to the transformer or inverter level for granularity.

