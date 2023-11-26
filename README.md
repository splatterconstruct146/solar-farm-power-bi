# Solar Farm Power BI
A Power BI report used to analyze the daily yield and other metrics at a solar farm I designed/constructed.\
Public Power BI Report Link: [here](https://www.novypro.com/project/solar-farm-report))

## Motivation
This report was created as a response to the company board wanting to be able to view the output and revenue of the solar farm without having to use the farm control and monitoring tools.

Note that this is no substitute for an actual plant SCADA system; it is merely just an additional avenue to view plant related information.

## Shortcomings
Since this report takes data from csv files the information shown will not be real-time. This isn't meant to be a dashboard nor a substitute for one. 

Additionally the report is bottlenecked to the information that's available in the csv files in the first place. In this case only a few days worth of information and only a few metrics were made available in the first place. 

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

## Process
Shows the process of cleaning the data, creating the relevant tables, to creating the Power BI report. 
### 1. Original Data
The original data was sourced from the solar farm's control and monitoring tools, which took the info from the inverters.\
The control and monitoring tool exports info as an excel file.\
Unfortunately, all entries exported are in text format as opposed to numerical.\
The screenshot below exemplifies.\
![image 7 - uncleaned data (excel)](https://github.com/splatterconstruct146/solar-farm-power-bi/assets/135209633/99a59d0d-1b4d-4219-95c8-9d5f47f59084)
Image 3: Screenshot of the entries in the original data being text format instead of the expected decimals/floats or integers. Also note the data is stored horizontally instead of vertically. 

### 2. Cleaning Step 1 - Text to Numerical
Usually Power BI does a good job at automatically recognizing numbers recorded in text format and can automatically apply transformations.\
Unfortunately that didn't work for this dataset. Even Microsoft Excel's own built-in function to change cell format didn't work in this case. Neither did Python's pandas package.\
The solution was to mass copy and paste the cells without format inside Excel, and then changing the format using Excel's built-in function (the original cells behaved weirdly resistant; but newly copied cells behaved as expected).

### 3. Cleaning Step 2 - Transposing
Once the data was properly formatted to numerical it was reimported into Power BI.\
The screenshot below shows the dataset in Power BI.
![image 6 - uncleaned data (power bi)](https://github.com/splatterconstruct146/solar-farm-power-bi/assets/135209633/8c044f98-739a-425b-8046-76caf8cccfa6)
Image 4: The screenshot above shows how the dataset after being imported into Power BI. Now, numbers were properly recognized as numbers.

Since the data was in a horizontal format it had to be tranposed.\
Due to daily yield, total DC power, total AC power being grouped into each hour, these had to be unpivoted as well.\
The screenshot below shows the entire transformation.
![image 8 - cleaned data (power bi)](https://github.com/splatterconstruct146/solar-farm-power-bi/assets/135209633/a8d84fa5-b982-43bb-bf9a-6d83123c3a94)
Image 5: The screenshot above shows how the dataset looks like after transforming and cleaning it. Note the entire transformation step on the right side of the screen.

### 4. Cleaning Step 3 - UNION 
The original dataset was broken into days. Each day's worth of data is in one file (meaning one table). Combining all the data into one big table made sense.\
The combination of individual days was done with Power BI's UNION function.\
The screenshot below shows the final combined table.
![image 9 - fact table (UNION cleaned data)](https://github.com/splatterconstruct146/solar-farm-power-bi/assets/135209633/07485367-4f54-4e7d-831b-f3d6427d1df6)
Image 6: The screenshot above shows the combined table. Note that this table is also a fact table. More on fact tables in the next section.

### 5. Data Modeling 
Decided to model the data using the star schema. The star schema makes databases run more efficiently in Power BI and also trims unecessary columns from tables.\
Most of the information will be housed in the fact table - which was the table created using UNION in the previous step.\
A dimension table holding information about the inverters have been created as well. This table houses static info like installed capacity, inverter number etc.
![image 10 - dimension table](https://github.com/splatterconstruct146/solar-farm-power-bi/assets/135209633/3a1388e3-318b-463d-91cf-0e60aba134b1)
Image 7: The screenshot above shows the dimension table. 

### 6. Creating the Visuals
Once all relevant setup has been done the report could be created.\
In summary, the report was designed to answer some monitoring and revenue related questions such as:
1. Daily generation
2. Daily revenue
3. Inverter performance
4. Transformer performance

The screenshot below shows the summary page of the report and the tables and measures (Power BI manually calculated values using values found in the tables) on the right side.
![image 11 - main summary page with table details](https://github.com/splatterconstruct146/solar-farm-power-bi/assets/135209633/46708cc8-1694-4857-ad42-ab73eca03ffe)
Image 8: Screenshot of the report summary page. Tables, table columns, and measures shown on the right. 
