# Project Topic  : Data Analysis on the Relationship Between Low-Carbon Electricity usage and Global Average Temperatures & CO2 emissions 

###  code ipynb
### https://github.com/yosieph/Project1/edit/main/project1.ipynb
### Report project1
### https://github.com/yosieph/Project1/edit/main/Data-Analysis-Report.pdf


# Why we choose this topic:

The relationship between low-carbon electricity usage and global average temperatures is a critical subject in today's world.
Understanding how the use of low-carbon energy sources can affects global temperatures and CO2 emissions associated is very important for 
policymakers, governments, researchers, and the general public. 
This data analysis help to explore this relationship and highlight its significance.

# Project Objective 
The primary objective of this data analysis is to investigate if there is a correlation between first temperature & energy consumption, second, the use of low-carbon electricity sources and global average temperatures across 101 different countries. Additionally, the analysis will examine the emissions of CO2 and their impact on temperatures.

#  Research Questions: 

### there is any correlation between :
###  1 -temperature and energy consumption

###  2 - temperature and low-carbon electricity      
       
###  3- Co2 emissions & renewable energy .


# Data analysis process 

## Data Collection : 

###  - Collect data on low-carbon electricity percentage usage for each of the 101 countries. This data may include the percentage of electricity generated from low carbon  sources like wind, solar, hydro, and nuclear power.
###  - Gather data on global average temperatures over a specific time period (year 2019) for these countries.
###  - Collect data on emissions related to the use of energy ,  CO2 emissions .
###  - Collect the Longitude and latitude value of differents countries to make a good map

## Datasets used: 

### https://www.kaggle.com/datasets/iamsouravbanerjee/world-population-dataset
### https://www.kaggle.com/datasets/anshtanwar/global-data-on-sustainable-energy
### https://www.kaggle.com/datasets/balabaskar/historical-weather-data-of-all-country-capitals

## Data processing

Our CSV file named "project_data.csv" is obtained from merging three datasets, and cleaning them and keeping the data values which we want to use.
This final dataset contains data related to various countries and their energy-related statistics & temperature averages.

All data included are in the same period "2019", with the exception of country population "2020".
the first column contain 101 countries sorted by alphabet.
The columns in our dataset are:

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
12. 2020 Population 
```
## Data Visualizations:

A variety of visualizations, including scatter plots, box plots, linear regression and map plots, were used to explore different aspects of the data. These visualizations enhanced our understanding of the data and provided insights into distribution, correlation, and geographic patterns.

========================================
## Data Analysis (code developed):

#### dependencies and setup
```
#dependencies and setup
import matplotlib.pyplot as plt
import pandas as pd
import scipy.stats as st
import seaborn as sns
import numpy as np
import hvplot.pandas

from scipy.stats import ttest_ind
from scipy.stats import linregress
from scipy import stats
from pathlib import Path
```
```
#import files and read the data
main_data_path = Path("Resources/projectdata.csv")
main_data = pd.read_csv(main_data_path)
main_data

```

# Danik
## Temperature & energy consumption 
##### 1 Visualization

### graph plot showing energy consumption per country
![bar graph - renewable](https://github.com/yosieph/Project1/assets/100168693/e0e30478-260f-43e9-bd4d-d30f3d3f7351)
### scatter plot showing the correlation between temp and primary energy consumption
![Energy Consumption vs  Average Temperature (2019)](https://github.com/yosieph/Project1/assets/100168693/cad689fd-eb6f-411b-8c11-468c4e66f841)

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
<img width="960" alt="image" src="https://github.com/yosieph/Project1/assets/100168693/46b0c6e9-c025-4d54-9df3-f0f7772f4c79">

##### Analysis
##### The r-squared is: 0.40616752081275864 so There is a weak correlation between energy consumption and average temperature, after removing outliers.

##### Final Analysis: Based on the data provided, there is a weak correlation between energy consumption and temperature for all countries (outliers removed). The correlation is non-existant when all countries are included in the data. 
However, for countries with an average temperature of 10 or lower, there is a moderate to strong correlation.
# Add TTest 
Do higher and lower temperatures have an impact on energy consumption?
Null Hypothesis: Average country temperatures above 25 degress celsius and below 10 degress celsius have no impact on energy consumption.
Alternative Hypothesis: Average country temperatures above 25 degress celsius and below 10 degress celsius might play a factor in energy consumption.
```
#ttest
#define samples
group1 = main_data.loc[main_data['Average Temp'] >= 25]
group2 = main_data.loc[main_data['Average Temp'] <= 10]

#perform independent two sample t-test
ttest_ind(group1['Primary energy consumption per capita (kWh/person)'], group2['Primary energy consumption per capita (kWh/person)'])
```
### Result 
```
Ttest_indResult(statistic=-2.2483778025923717, pvalue=0.028435494666494792)
```
### Analysis 
Since the p-value is less than .05, we reject the null hypothesis of the t-test and conclude that there is sufficient evidence to say that temperatures might play an impact on energy consumption.

# Khadija
## Temperature and low-carbon electricity
### What is the relation betweeen  the  low-carbon electricity % produce  and the Average of Temperature on the 10 hotest  and coldest countries 
#### Map plot of Low-carbon electricity (% electricity)
```
%%capture --no-display

# Configure the map plot
map_plot_2 = main_data.hvplot.points("Longitude","Latitude", geo = True, tiles = "OSM", frame_width=800, frame_height=400, size="Low-carbon electricity (% electricity)", scale=2, color="Country")

# Display the map
map_plot_2
```
![image](https://github.com/yosieph/Project1/assets/100168693/ec26b932-32ab-45fb-976b-a29c7f0c7ce2)

#### #graph plot showing Low-carbon electricity (% electricity) values per country
![country low-carb](https://github.com/yosieph/Project1/assets/100168693/f2b7a51b-83e7-4706-8c94-aafc54a5d7ad)
```
# Find the country with the highest temperature
country_with_highest_temp = main_data[main_data['Average Temp'] == main_data['Average Temp'].max()]
# Get the low-carbon electricity percentage for the country with the highest temperature
low_carbon_percentage_highest_temp = country_with_highest_temp['Low-carbon electricity (% electricity)'].values[0]
# Find the country with the lowest temperature
country_with_lowest_temp = main_data[main_data['Average Temp'] == main_data['Average Temp'].min()]
# Get the low-carbon electricity percentage for the country with the lowest temperature
low_carbon_percentage_lowest_temp = country_with_lowest_temp['Low-carbon electricity (% electricity)'].values[0]
# Print the results
print(f'The low carbon electricity percentage in the country with the highest temperature is {low_carbon_percentage_highest_temp:.2f}%')
print(f'The low carbon electricity percentage in the country with the lowest temperature is {low_carbon_percentage_lowest_temp:.2f}%')
```
##### result 
```
The low carbon electricity percentage in the country with the highest temperature is 63.34%
The low carbon electricity percentage in the country with the lowest temperature is 100.00%
```

## Create a box plot to compare low-carbon electricity percentage by temperature category we choos 25 as a temperature 
![LC-Electricity(%) Temperature-BoxPlot](https://github.com/yosieph/Project1/assets/100168693/81758f08-875e-4d22-8dac-4ee7d38b2ccd)

### we can now use more data to have a good understanding , we will choose the 10 hotest and coldest countries to do our analysis
##### Develop a code to analyse the relation between average temperature and  Low-carbon electricity (% electricity) production
```
# Sort the main_data by 'Average Temp' in ascending order to get the lowest temperature countries
lowest_temp_countries = main_data.sort_values(by='Average Temp', ascending=True).head(10)[['Country', 'Average Temp', 'Low-carbon electricity (% electricity)']]
lowest_temp_countries.head(5)
# Sort the main_data by 'Average Temp' in descending order to get the highest temperature countries
highest_temp_countries = main_data.sort_values(by='Average Temp', ascending=False).head(10)[['Country', 'Average Temp', 'Low-carbon electricity (% electricity)']]
highest_temp_countries.head(5)
# Concatenate the two main_dataFrames to get the final result
result_df = pd.concat([lowest_temp_countries, highest_temp_countries])
# Reset the index of the resulting main_dataFrame
result_df.reset_index(drop=True, inplace=True)
# Display the result main_dataFrame
result_df.head(20)
```
##### Analysis
##### the coldest country are Iceland, canada,finland and others make a very high percentage of Low carbon electricity above belarus and estonia ,irland The highest countries are Sudan ,Niger ,Djibouti and others dont produce high carbon electricity pourcentage except Sudan with 63.3% and Cambodia with 53.37% and little be for Mali with 35.24%

#### Create subplots for the visualizations
```
# Visualization 1: Scatter Plot for Lowest Temperature Countries with linear regression and calcul of r-squared
# Visualization 2: Scatter Plot for Highest Temperature Countries with linear regression and calcul of r-squared
# Visualization 3: Combined Scatter Plot for All Countries with linear regression and calcul of r-squared
```
####  Result and Interpretation 
```
The r-squared for Coldest countries is: 0.354
The r-squared for Highest countries is: 0.057
The r-squared for all countries is: 0.244
Linear Regression for Lowest Temperature Countries: Slope (Coefficient) = -13.9328
Linear Regression for Highest Temperature Countries: Slope (Coefficient) = 4.6044
Linear Regression for All Countries: Slope (Coefficient) = -2.0688
```
##### 1 Visualization
![Combined-Scatter-Plot-with-linear-regression-for-All-Countries](https://github.com/yosieph/Project1/assets/100168693/008aa9bd-1c03-420a-8844-fd32623bfc2e)
##### Analysis
##### 1-Linear Regression for Lowest Temperature Countries: Slope (Coefficient) = -13.9328 so Colder countries tend to rely more heavily on low-carbon electricity sources production but they have a higher percentage of lc production
#####  2-Linear Regression for Highest Temperature Countries: Slope (Coefficient) = 4.6044 so hotter countries in this group demonstrate a evolutif production of low-carbon electricity
#####   3-Linear Regression for All Countries: Slope (Coefficient) = -2.07 so this indicate that as the average temperature increases, the percentage of low-carbon electricity decreases

### After our first analysis about the relation between Temperature average and Low Carbon electricity % produce , to deepdive our analysis , we decide to see others Factor related to  Renewable energy share in the total final energy consumption (%)  and it impact on Temperature

## What is the relation betweeen  the  Renewable energy consumption (%) and the Average of Temperature on the 10 hotest  and coldest countries 
```
##graph plot showing Renewable energy share in the total final energy consumption (%)  per country
```
##### Visualization
![country renew](https://github.com/yosieph/Project1/assets/100168693/1ec16f49-45ee-4c7d-9128-19197782c8f8)

#### Create subplots for the visualizations
```
# Visualization 1: Scatter Plot for renewable energy on  Lowest Temperature Countries with linear regression and calcul of r-squared
# Visualization 2: Scatter Plot for renewable energy on  Highest Temperature Countries with linear regression and calcul of r-squared
# Visualization 3: Combined Scatter Plot for renewable energy on  All Countries with linear regression and calcul of r-squared
```
####  Result and Interpretation 
```
The r-squared for Coldest countries is: 0.351
The r-squared for Highest countries is: 0.355
The r-squared for all countries is: 0.028
Linear Regression for Lowest Temperature Countries: Slope (Coefficient) = -9.2526
Linear Regression for Highest Temperature Countries: Slope (Coefficient) = 15.5854
Linear Regression for All Countries: Slope (Coefficient) = 0.5805
```
##### 1 Visualization
![Combined-Scatter-Plot-with-linear-regression-Renewable -for-All-Countries](https://github.com/yosieph/Project1/assets/100168693/e2209134-263a-4d15-a4d9-b2dbe70f0104)

##### Analysis
##### Analysis : we have a negative coefficient -9.25 so the coldest countries tend to rely more heavily on renewables energy pourcentage  or the highest countries with a strong correlation coefficient 15,58 tend to use more renewable energy source .the percentage of renewable energy used have a positif regression with the average temperature on global countries

# Add TTest 
Develop a TTest to check our Hypotisis 
Null Hypothesis : there is no difference between renewable energy used in the 10 Coldest countries and the 10 hotest country 
Alternative Hypothesis : there is a significant difference between the two groups in term of consumption of renewable energies

```
#ttest code
#define groupes
Hotest_countries = main_data.loc[main_data['Average Temp'] >= 28.70]
coldest_countries = main_data.loc[main_data['Average Temp'] <= 10]

#perform independent two sample t-test
ttest_ind(Hotest_countries['Renewable energy share in the total final energy consumption (%)'], coldest_countries['Renewable energy share in the total final energy consumption (%)'])
```
### Result 
```
Ttest_indResult(statistic=0.3185904666968613, pvalue=0.7533402039975953)
```
### Analysis 
the p-value (0.753) is much larger than 0.05 (a common significance level).so we  do not have enough evidence to reject the null hypothesis. we conclude that there is no significant difference between the two groups.

### Final  Analysis

##### The analysis of our results for the top ten countries with the highest and the lowest average temperatures indicates that temperature may indeed play a significant role in influencing the choice of electricity sources in different countries. 
##### The coldest countries, which are happen to be more developed, exhibit the highest usage of low-carbon electricity sources.
##### Colder climates may drive the adoption of low-carbon electricity sources as a more efficient and sustainable option, while hotter regions may also be moving in the same direction. 
##### Additionally, the higher usage of low-carbon electricity in colder, more developed countries highlights the potential correlation between economic development and the adoption of low carbon  energy sources.


# Yoseiph
## Use of low-carbon electricity sources and CO2 emissions 

#####  Visualization
```
# bar graph - co2 emissions
```
![bar graph - co2 emissions](https://github.com/yosieph/Project1/assets/100168693/2ec91443-b8b9-46ca-9547-79f88bcaea5c)

#####  code
```
# List the main_data by co2 emission  in descending order to get the co2 emssion countries
highest_Co2_Emission_countries = main_data.sort_values(by='co2 Emissions (metric tons per capita)', ascending=False).head(10)[['Country', 'co2 Emissions (metric tons per capita)', 'Renewable energy share in the total final energy consumption (%)']]
print (highest_Co2_Emission_countries)

```
#### Analysis
##### Analysis:The High co2 emission  country  are China ,United States , india , Japan and Germany ..ect. Industrial economy major factor in co2 emission and popilation alos one factor . 

##### Lowest co2 emission countries per renewable energy consumption
![bar graph - highest](https://github.com/yosieph/Project1/assets/100168693/8190252a-e773-466d-b52f-09947128011c)

#### Analysis
##### The resulting plot will show a bar chart with each country's name on the x-axis and the corresponding CO2 emissions per capita (expressed as "low-carbon electricity (% electricity)") on the y-axis. 
##### Each bar will represent a country, and its height will indicate the value of CO2 emissions per capita. The blue color is used to distinguish the bars.
##### This chart should help visualize and compare the low CO2 emission countries in terms of their CO2 emissions per capita,allowing for easy identification of which countries have lower emissions in relation to their electricity production.
##### highest co2 emission Country per renewable energy consumption
![bar graph - lowest](https://github.com/yosieph/Project1/assets/100168693/49e48c63-7da7-4458-a826-87ea51069c88)

#### Analysis
##### We have a correlation between low CO2 emissions and higher use of renewable energy, The countries that produce more renewable energy generate less CO2 .it's essential to remember that each country's energy mix and emissions profile are influenced by unique factors, including geography, natural resources, economic conditions, and government policies.If the average low-carbon electricity percentage is higher for countries with "Low CO2 Emissions," it would suggest that these countries tend to use more low-carbon electricity sources.

#### list of high carbon 
![piechart - highest](https://github.com/yosieph/Project1/assets/100168693/6c6d71b8-9bf3-4560-b12f-1936fe3b5672)
#### CO2 Emissions for Lowest CO2 Countries
![piechart - lowest](https://github.com/yosieph/Project1/assets/100168693/c1a7d226-43f7-4623-8ec3-4959ea987e6c)




# Summary:

The final analysis about our primary objective :

## 1 - Temperature & energy consumption
There is a strong correlation between Temperature and energy consumption in countries with an average temperature of 10 degrees or less. Overall, there is a weak correlation. 
## 2 - Temperature &  the low-carbon electricity sources 
The Coldest countries tend to generate a greater proportion of low-carbon electricity compared to their warmer countries with some exceptions.
## 3 - Co2 Emission & renewable energy produced
The countries that produce more renewable energy generate less Co2 .
   
===========================================

#  Recommendations

Our recommendations or insights for future research in this area are:
Exploration of Other Factors:
Further analysis considered additional factors like population and economic indicators, energy consumption over the years, revealing potential relationships between these variables and energy consumption.

# Team Members: Danik Lafrance, Khadija Fahr, Yosieph Fissuh
