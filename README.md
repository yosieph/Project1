# Project Topic  : Data Analysis on the Relationship Between Low-Carbon Electricity usage and Global Average Temperatures & CO2 emissions 
# Team Members: Danik Lafrance, Khadija Fahr, Yosieph Fissuh


# Why we choose this topic:

The relationship between low-carbon electricity usage and global average temperatures is a critical subject in today's world.
Understanding how the use of low-carbon energy sources can affects global temperatures and CO2 emissions associated is very important for 
policymakers, governments, researchers, and the general public. 
This data analysis help to explore this relationship and highlight its significance.

# Project Objective 
The primary objective of this data analysis is to investigate if there is a correlation between first Temperature & energy consumption ,second the use of low-carbon electricity sources and global average temperatures across 101 different countries. 
Additionally, the analysis will examine the emissions of CO2 and their impact on temperatures.

#  Research Questions: 

###  1 - Do higher and lower temperatures have an impact on energy consumption? Danik

###  2 - What is the percentage of low-carbon electricity used in the highest & lowest countries ? Khadija
       #### “do this for the  highest & lowest  countries 
       #### “do this for  10 top &bottom highest & lowest  countries 
       
    1- ###  3- Do countries with high CO2 emissions use less low-carbon electricity? Yosieph
             ####  Do countries with low CO2 emissions use more low-carbon electricity? 

# Data analysis process 


## Data Collection : 

###  - Collect data on low-carbon electricity percentage usage for each of the 101 countries. This data may include the percentage of electricity generated from low carbon  sources like wind, solar, hydro, and nuclear power.
###    - Gather data on global average temperatures over a specific time period (year 2019) for these countries.
###  - Collect data on emissions related to the use of energy ,  CO2 emissions .
###  - Collect the Longitude and latitude value of differents countries to make a good map 
## Datasets  used: 

‘https://www.weatherstack.com, ‘
‘https://www.kaggle.com/datasets/anshtanwar/global-data-on-sustainable-energy,’
‘https://www.kaggle.com/datasets/nelgiriyewithana/countries-of-the-world-2023,’


## Data processing

Our CSV file named "project_data.csv" is obtained from merging three datasets , and claining them and take the data values which we want to use ,
this final dataset  contain data related to various countries and their energy-related statistics &temperature average 
all data included are in the same period “year on 2019 “. 
the first column contain 101 countries  sorted by alphabet .
The all columns in our dataset are:

```
1. Country
2. Average Temperature in 2019
3. Renewable Energy Share in the Total Final Energy Consumption (%)
4. Electricity from Fossil Fuels (TWh - Terawatt-hours)
5. Electricity from Nuclear (TWh)
6. Electricity from Renewables (TWh)
7. Low-carbon Electricity (% of Electricity)
8. Primary Energy Consumption per Capita (kWh/person)
9. CO2 Emissions (Metric Tons per Capita)
10. Latitude
11. Longitude
12. Population 
```
## Data Visualizations:**
- A variety of visualizations, including scatter plots, box plots, linear regression and map plots, were used to explore different aspects of the data. These visualizations enhanced our understanding of the data and provided insights into distribution, correlation, and geographic patterns.


========================================
## Data Analysis (code developed ):

#### dependencies and setup
```

import matplotlib.pyplot as plt
import pandas as pd
import scipy.stats as st
import seaborn as sns
import numpy as np
from scipy.stats import linregress
from pathlib import Path
import hvplot.pandas

# Turn off warning messages
import warnings
warnings.filterwarnings("ignore")

```
```
#import files and read the data
main_data_path = Path("Resources/projectdata.csv")
main_data = pd.read_csv(main_data_path)
main_data

```

### Temperature & energy consumption developed by Danik

#### Map plot of Primary energy consumption per capita (kWh/person)


####  Interpretation and Analysis 
##### 1 Visualization
```
#scatter plot showing the correlation between temp and primary energy consumption
```

##### Analysis
##### The r-squared is: 0.07426043111699936  so The is a no/very weak correlation between energy consumption and average temperature with entire data.

#create two data frames (high and low temperatures)  to deepdive our analysis 
```
high_temps = main_data.loc[main_data['Average Temp'] >= 25]
low_temps = main_data.loc[main_data['Average Temp'] <= 10]
```

##### 2 Visualization
```
#scatter plot showing the correlation between temp and primary energy consumption in high temp 

```
##### Analysis
##### The r-squared is: 0.0028583229372739416 so There is no correlation between energy consumption and countries with average temperatures 25 and higher

##### 3 Visualization
```
#scatter plot showing the correlation between temp and primary energy consumption in low temp 

```
##### Analysis
##### The r-squared is: 0.7053782565845196 so There is a moderate/strong correlation between energy consumption and countries with an average temperature of 10 or lower.

##### 4 Visualization
```
#find outliers within the data

```
##### Analysis
##### The lower quartile of temperatures is: 4599.5175500000005 The upper quartile of temperatures is: 38088.3975 The interquartile range of temperatures is: 33488.87995 The the median of temperatures is: 20460.55 Values below -45633.802375 could be outliers. Values above 88321.71742500001 could be outliers. ['Bahrain', 'Canada', 'Iceland', 'Kuwait', 'Norway', 'Qatar', 'Singapore', 'Trinidad and Tobago', 'United Arab Emirates'] could be outliers. 

##### 5 Visualization
```
##remove outliers and complete new linear regression plot

```
##### Analysis
##### The r-squared is: 0.40616752081275864 so There is a weak correlation between energy consumption and average temperature, after removing outliers.

##### Final Analysis: Based on the data provided, there is a weak correlation between energy consumption and temperature for all countries (outliers removed). The correlation is non-existant when all countries are included in the data. 
However, for countries with an average temperature of 10 or lower, there is a moderate to strong correlation.



### Use of low-carbon electricity sources and average temperatures developed by Khadija

#### Map plot of Low-carbon electricity (% electricity)


#### Map plot of Average Temp


####  Interpretation and Analysis 
```
#The low carbon electricity percentage in the highest & lowest  temperature countries
```
##### Result 
```
The low carbon electricity percentage in the country with the highest temperature (Sudan )is 63.34% 
The low carbon electricity percentage in the country with the lowest temperature(Iceland) is 100.00% 

```
##### 1 Visualization
```
# Create a scatter plot with a linear regression line
output_data/LC-Electricity(%) VS Temperature-scaterPlot.png
```
##### Analysis
##### The r-squared is negatif -2.0688 so there is a negative  correlation between LC-Electricity(%) and average temperature high and low .

##### 2 Visualization
```
#Create a box plot to compare low-carbon electricity percentage by temperature category
output_data/LC-Electricity(%)&Temperature-BoxPlot.png

```
##### Analysis
##### 


##### 3 Visualization
```
#The low carbon electricity percentage in the country with the 10 highest & 10 lowest  temperature countries 

# Display the result main_dataFrame:country ,Average Temp ,Low-carbon electricity (% electricity)

result_df.head(20)

```
##### Analysis
##### the coldest country are Iceland, canada,finland and others  are all Iceland, and the uses of Low carbon electricity pourcentage is very hight above belarus and estonia ,irland 
The highest countries are Sudan ,Niger ,Djibouti and others dont have high carbon electricity pourcentage except Sudan with 63.3% and Cambodia with 53.37% and little be for Mali with 35.24% 
If we have a global look at  the result we can definitely see that the lowest countries use more low carbon electricity than the highest countries except Sudan and Cambodia , so we can add more factors like a development , richness or others in our analysis to be more credible .


##### 4 Visualization
```
# Create subplots with linear regression for the visualizations
#Scatter Plot for Lowest Temperature Countries
# Perform Linear Regression for Lowest Temperature Countries
output_data/Scatter-Plot-with-linear-regression-for-Lowest-Temperature-Countries.png


```
##### Analysis
##### Linear Regression for Lowest Temperature Countries: Slope (Coefficient) = -13.9328 so Colder countries tend to rely more heavily on low-carbon electricity sources

##### 5 Visualization
```
# Scatter Plot for Highest Temperature Countries
# Perform Linear Regression for Highest Temperature Countries
output_data/Scatter-Plot-with-linear-regression-for-highest-Temperature-Countries.png

```
##### Analysis
##### Linear Regression for Highest Temperature Countries: Slope (Coefficient) = 4.6044 so hotter countries in this group demonstrate a preference for low-carbon electricity sources.

##### 6 Visualization
```
# Combined Scatter Plot for All Countries
# Perform Linear Regression for All Countries
output_data/Combined-Scatter-Plot-with-linear-regression-for-All-Countries.png

```
##### Analysis
##### Linear Regression for All Countries: Slope (Coefficient) = -2.07 so this indicate that as the average temperature increases, the percentage of low-carbon electricity decreases





### Final  Analysis

##### The analysis of our results for the top ten countries with the highest and the lowest average temperatures indicates that temperature may indeed play a significant role in influencing the choice of electricity sources in different countries. 
The coldest countries, which are happen to be more developed, exhibit the highest usage of low-carbon electricity sources.
Colder climates may drive the adoption of low-carbon electricity sources as a more efficient and sustainable option, while hotter regions may also be moving in the same direction. 
Additionally, the higher usage of low-carbon electricity in colder, more developed countries highlights the potential correlation between economic development and the adoption of low carbon  energy sources.



### Use of low-carbon electricity sources and CO2 emissions developed by Yoseiph







##### 7 Visualization
```
# 
```
##### Analysis
##### 







# Summary 
 Data Analysis on "Low-Carbon Electricity uses percentage  and Global Average Temperatures & Co2 emission "**

1. **Impact of Temperature on Energy Consumption:**
   -

2. **Percentage of Low-Carbon Electricity uses & Temperature Average **
   - The analysis revealed that a certain percentage of electricity uses    across the analyzed countries comes from low-carbon sources (renewable energy or nuclear power). This indicates a global effort to transition to cleaner energy sources.
   - 


3. **Relationship Between CO2 Emissions and sainstable  Electricity Usage:**

   
===========================================
   


   



#  Conclusion

### This data analysis sheds light on the complex interplay between temperature, energy consumption, low-carbon electricity usage and Co2 emission. 
Understanding these dynamics is crucial for addressing climate change, optimizing energy resources, and making informed decisions regarding energy policy and sustainability initiatives. 
Further research and investigation into specific regions and policy interventions may be necessary to develop targeted strategies for reducing carbon emissions and promoting clean energy adoption.


#  Recommendations 
our recommendations or insights for future research in this area are :
1 -Exploration of Other Factors:
- Further analysis considered additional factors like population and economic indicators, energy consumption over the years, revealing potential relationships between these variables and energy consumption.
Those relationships may offer insights into energy demand patterns and the adoption of low-carbon energy sources and gives more valuable information  for policymakers and energy planners as they prepare for future energy needs.
-
