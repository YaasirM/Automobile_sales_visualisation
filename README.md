<h1 align = "Center"> Automobile Sales Visualisation Analysis </h1>

## Description
In this project I was tasked to create plots to understand the historical trends in automobile sales during the recession period. The data set used for this project contains *historical_automobile_sales* data, representing automobile sales and related variables during the recession and non-recession period. The dataset includes the following columns:


| Date | Year | Month | Recession | Consumer_Confidence | Seasonality_Weight | Price | Advertising_Expenditure | Competition | GDP | Growth_Rate | unemployment_rate | Automobile_Sales | Vehicle_Type | City |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1/31/1980 | 1980 | Jan | 1 | 108.24 | 0.5 | 27483.571 | 1558 | 7 | 60.223 | 0.01 | 5.4 | 456 | Supperminicar | Georgia |


To see the full data set that was used for this project, you can find it [here](https://github.com/YaasirM/Automobile_sales_visualisation/blob/main/assets/historical_automobile_sales.csv)

## Task
The task of this project is to do a few of the following:
1. The affect the recessions had on automobile sales
2. How the sales of different automobile types were affected by the recession
3. To confirm if there was a correlation between the vehicle price and sales during recession
4. How advertisement expenditure was affected by the recession
5. The affect of unemployment rate for vehicle sales

To get started, I initially imported the desired packages (matplotlib, pandas, seaborn and numpy) before importing the dataset. I then confirmed all the columns that were required were present in the imported dataset before starting with the visualisation analysis.

## Automobile Sales vs Recession
I started by creating a line graph which compared the automobile sales and the year:


```python
import numpy as np
import pandas as pd
%matplotlib inline
import matplotlib as mpl
import matplotlib.pyplot as plt
import seaborn as sns
# We will need to group the year and calculate the average on the 'Automobile Sales'
df_line = df.groupby(df['Year'])['Automobile_Sales'].mean()
plt.figure(figsize=(10, 6))
df_line.plot(kind = 'line')
plt.xlabel('Year')
plt.ylabel('Automobile Sales')
plt.title('Automobile Sales Each Year')
plt.show()
```

![Automobile Sales_by_year](https://github.com/YaasirM/Automobile_sales_visualisation/blob/main/assets/images/Sales_vs_recession.png)

*Automobile Sales by Year*

Now from this line graph, we can decipher that there are periods where the total automobile sales dips by an alarming rate. It may be due to the recession periods, so I have included the label on the below graph to highlight the times of the recession:

```python
plt.figure(figsize=(10, 6))
df_line.plot(kind = 'line')
plt.xticks(list(range(1980,2024)), rotation = 75)
plt.xlabel('Year')
plt.ylabel('Automobile Sales')
plt.title('Automobile Sales Each Year')
plt.text(1982, 650, '1981-82 Recession', rotation = 40)
plt.text(1991, 650, '1990-91 Recession', rotation = 40)
plt.text(2001, 650, '2000-2001 Recession', rotation = 40)
plt.text(2009, 650, '2008-2009 Recession', rotation = 40)
plt.legend()
plt.show()
```

![Automobile Sales_by_year2](https://github.com/YaasirM/Automobile_sales_visualisation/blob/main/assets/images/Automobile%20Sales%20by%20Year.png)

*Automobile Sales by Year (2)*

Here we can see that the recession periods directly affect the automobile sales that are made each year, causing the number of sales to decrese by a drastic rate. We can also see from the graph that the recession with the lowest automobile sales was the 2008-09 recession, whilst the highest amount of sales in a recession period was the 2000-01 recession (although not a large difference between the two). 

## Vehicle type by recession period

Now we will try to compare the sales made by each vehice type and see if these changes during the recession period were found in all vehicle types.

```python
recession_data = df[df['Recession'] == 1]
dd=df.groupby(['Recession','Vehicle_Type'])['Automobile_Sales'].mean().reset_index()
plt.figure(figsize=(10, 6))
sns.barplot(x='Recession', y='Automobile_Sales', hue='Vehicle_Type', data=dd)
plt.xticks(ticks=[0, 1], labels=['Non-Recession', 'Recession'])
plt.xlabel('Recession vs Non-Recession')
plt.ylabel('Automobile Sales')
plt.title('Vehicle-Wise Sales during Recession and Non-Recession Period')
plt.show()
```

![Vehicle type by recession period](https://github.com/YaasirM/Automobile_sales_visualisation/blob/main/assets/images/Vehicle%20type%20by%20recession%20period.png)

*Vehicle type by recession period*

I used a bar chart to create this plot as it could be the vehicle types could be grouped beteween non-recession and recession periods. From this plot, we can understand that there is a drastic decline in the overall sales of the automobiles during recession. However, the most affected type of vehicle is *executivecar* and *sports*. This may be because these two categories are considered high-end cars, which many people could not afford to spend on during recession periods.

## Correlation between recession and vehicle price and sales during recession

Now that we have confirmed the large sale decrease overall vehicle sales during the recession period, we wanted to deteremine if the vehicle price was related to a recession and if there would be a decrease in the price of a vehicle every time a recession occurred. I created a scatter plot to identify the relationship between average vehicle price and sales volume during the recession period:

```python
rec_data = df[df['Recession'] == 1]
plt.scatter(recession_data['Price'], rec_data['Automobile_Sales'])
plt.xlabel('Price')
plt.ylabel('Automobile Sales')
plt.title('Relationship between Average Vehicle Price and Sales during Recessions')
plt.show()
```

![Vehicle price and sales during recession](https://github.com/YaasirM/Automobile_sales_visualisation/blob/main/assets/images/Vehicle%20price%20and%20sales%20during%20recession.png)

*Vehicle price and sales during recession*

Here we can see that the scatter plot above shows not much relation between the average vehicle price and sales volume during the recession periods. This suggests that prices do not change in accordance to the recession periods, meaning that automobiles won't necessarily be cheaper or more expensive in recession periods in comparison to non-recession periods.

## Advertisement Expenditure
We also wanted to know if advertising was affected in any way by the recession periods as well. The initial step involved analyzing the advertising expenditure during recession periods compared to non-recession periods:

```python
Rdata = df[df['Recession'] == 1]
NRdata = df[df['Recession'] == 0]
# Calculate the total advertising expenditure for both periods
RAtotal = Rdata['Advertising_Expenditure'].sum()
NRtotal = NRdata['Advertising_Expenditure'].sum()
# Create a pie chart for the advertising expenditure 
plt.figure(figsize=(8, 6))
labels = ['Recession', 'Non-Recession']
sizes = [RAtotal, NRtotal]
plt.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=90)
plt.title('Advertising Expenditure of XYZAutomotives During Recession/Non-Recession Periods')
plt.show()
```

![Advertising expenditure in different periods](https://github.com/YaasirM/Automobile_sales_visualisation/blob/main/assets/images/Advertising%20expenditure%20in%20different%20periods.png)

*Advertising expenditure in different periods*

A pie chart effectively highlights the proportional difference in advertising expenditure between recession and non-recession periods. In the pie chart, it is evident that the non-recession period has almost x2 more advertisement expenditure in comparison to the recession period. This portrays the lack of money being spent on advertising during the recession periods. 

During the recession period we also wanted to identify if there were specific vehicle types that had more advertising expenditure in comparison to others. I also used a pie chart to depict this as it was easier to show the split of advertising expenditure between the different vehicle types:

```python
Rdata = df[df['Recession'] == 1]
# Calculate the sales volume by vehicle type during recessions
VTexpenditure = Rdata.groupby('Vehicle_Type')['Advertising_Expenditure'].sum()
# Create a pie chart for the share of each vehicle type in total expenditure during recessions
plt.figure(figsize=(8, 6))
labels = VTexpenditure.index
sizes = VTexpenditure.values
plt.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=90)
plt.title('Total Advertisement Expenditure per Vehicle Type During Recession')
plt.show()
```

![Advertising expenditure per Vehicle type](https://github.com/YaasirM/Automobile_sales_visualisation/blob/main/assets/images/Advertising%20expenditure%20per%20Vehicle%20type.png)

*Advertising expenditure per Vehicle type*

Here we can see that the *executive car* had the least amount of advertising expenditure, alongside the *sports*. This was also a similar case when comparing the automobile sales during the recession period, maybe the decrease in advertisement expenditure for these cars were a factor in the low sales returned in the recession period. The vehicle type with the largest portion of advertisement expenditure was the *Medium Family Car*.

## Unemployment rate on sales during recession period

Unemployment rates were sky-high during the recession periods as opposed to any other time period (in this dataset). This sets a tone in the number of sales made during the recession period. This now begs the question - does the unemployment rate affect vehicle sales? I created a line graph to identify if the sales of any vehicle type were affected by the unemployment rate:

```python
df_rec = df[df['Recession']==1]
sns.lineplot(data=df_rec, x='unemployment_rate', y='Automobile_Sales', hue='Vehicle_Type', style='Vehicle_Type', markers='o', err_style=None)
plt.ylim(0,850)
plt.legend(loc=(0.05,.3))
```
![Unemployment rate vs sales](https://github.com/YaasirM/Automobile_sales_visualisation/blob/main/assets/images/Unemployment%20rate%20vs%20sales.png)

*Unemployment rate vs sales*

It seems as though during recession, buying pattern changed, the sales of low range vehicle like *Super Mini Car*, *Small Family Car* and *Medium Mini Car* fluctuate between 550 and 800. This fluctuation seems like it is independant of the unemployment rate as it does not have a negative or positive correlation, therefore the unemployment rate does not affect these vehicle types. The vehicle type that visibly does become affeted however is the *Sports Car* as it decreases from roughly 200 to have sales below 100 as the unemployment rate increases. This can be considered a negative correlation, although there aren't many points in the graph to completely confirm this statement.

# Conclusion

From this project we can confirm that there are a variety of factors in Automobile Sales that become affected whenever there is a recession period. Ontop of sales, things advertisement expenditure also become decreased during a period of recession. There are also different vehicle types that become more affected by others in a recession period such as the *Executive* and *Sports* cars.

From this project I was also abe to develop valuable visualisation skills, utilising various python packages in order to portray data in an easily digestible manner.

## Jupyter notebook
The analysis and modelling were performed using Python and Jupyter Notebook. You can find the complete notebook [here](https://github.com/YaasirM/Automobile_sales_visualisation/blob/main/assets/Automobile_sales_visualisation_notebook.ipynb)
