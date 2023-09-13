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

### Temperature & energy consumption developed by Danik
##### 1 Visualization
### graph plot showing temp values per country
![Country Temp](https://github.com/yosieph/Project1/assets/100168693/7de185ba-1b5f-4777-a468-504a06fe9777)
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





## Use of low-carbon electricity sources and average temperatures developed by Khadija

#### Map plot of Average Temperature

#### Map plot of Renewable energy share in the total final energy consumption (%)

#### Map plot of Low-carbon electricity (% electricity)

##### 1 Visualization
-![image](output_data/Country-Energy.png)
```
#Perform a code to visualize the scatter plot and linear regression about  relation between average temperature and  Renewable energy share in the total final energy consumption (%)

output_data/Scatter-Plot-with-linear-regression-for-Lowest-Temperature-Countries.png
output_data/Scatter-Plot-with-linear-regression-for-highest-Temperature-Countries.png
output_data/Combined-Scatter-Plot-with-linear-regression-for-All-Countries.png
```
##### Analysis
##### we have a negative coefficient -9.25 so the coldest countries tend to rely more heavily on renewables energy pourcentage  or the highest countries with a strong correlation coefficient 15,58 tend to use more renewable energy source .the percentage of renewable energy used have a positif regression with the average temperature on global countries 


####  Interpretation and Analysis 
```
#Perform code to show The low carbon electricity percentage in the highest & lowest  temperature countries
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

![Combined-Scatter-Plot-with-linear-regression-Renewable -for-All-Countries](https://github.com/yosieph/Project1/assets/100168693/dd699849-9f8b-44e6-92b6-ef94c7703fbb)

##### 6 Visualization
```
# Combined Scatter Plot for All Countries
# Perform Linear Regression for All Countries
output_data/Combined-Scatter-Plot-with-linear-regression-for-All-Countries.png

```
-![image](https://github.com/yosieph/Project1/blob/main/output_data/Combined-Scatter-Plot-with-linear-regression-for-All-Countries.png)
##### Analysis
##### Linear Regression for All Countries: Slope (Coefficient) = -2.07 so this indicate that as the average temperature increases, the percentage of low-carbon electricity decreases

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
The coldest countries, which are happen to be more developed, exhibit the highest usage of low-carbon electricity sources.
Colder climates may drive the adoption of low-carbon electricity sources as a more efficient and sustainable option, while hotter regions may also be moving in the same direction. 
Additionally, the higher usage of low-carbon electricity in colder, more developed countries highlights the potential correlation between economic development and the adoption of low carbon  energy sources.



### Use of low-carbon electricity sources and CO2 emissions developed by Yoseiph

#####



##### 7 Visualization
```
# 
```
<img width="960" alt="image" src="https://github.com/yosieph/Project1/assets/100168693/841eaec8-1a97-40e0-b754-8dc2df52196a">
##### Analysis
##### 

We have a correlation between low CO2 emissions and higher use of renewable energy, 
The countries that produce more renewable energy generate less CO2 . 
it's essential to remember that each country's energy mix and emissions profile are influenced by unique factors, including geography, natural resources, economic conditions, and government policies.


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
