---
layout: article
title: Merging DataFrames with pandas
key: 20200630
tags: Programming Python pandas
modify_date: 2020-06-30
pageview: false
aside:
  toc: true
---

Base on DataCamp.

<!--more-->

[Pandas Cheat Sheet](https://datacamp-community-prod.s3.amazonaws.com/9f0f2ae1-8bd8-4302-a67b-e17f3059d9e8)

## Preparing data

### Reading multiple data files

#### Reading DataFrames from multiple files in a loop
```py
# Import pandas
import pandas as pd

# Create the list of file names: filenames
filenames = ['Gold.csv', 'Silver.csv', 'Bronze.csv']

# Create the list of three DataFrames: dataframes
dataframes = []
for filename in filenames:
    dataframes.append(pd.read_csv(filename))

# Print top 5 rows of 1st DataFrame in dataframes
print(dataframes[0].head(5))
>    NOC         Country   Total
  0  USA   United States  2088.0
  1  URS    Soviet Union   838.0
  2  GBR  United Kingdom   498.0
  3  FRA          France   378.0
  4  GER         Germany   407.0
```

#### Combining DataFrames from multiple data files

In this exercise, you'll combine the three DataFrames from earlier exercises - `gold`, `silver`, & `bronze` - into a single DataFrame called `medals`. 

```py
# Import pandas
import pandas as pd

# Make a copy of gold: medals
medals = gold.copy()

# Create list of new column labels: new_labels
new_labels = ['NOC', 'Country', 'Gold']

# Rename the columns of medals using new_labels
medals.columns = new_labels

# Add columns 'Silver' & 'Bronze' to medals
medals['Silver'] = silver['Total']
medals['Bronze'] = bronze['Total']

# Print the head of medals
print(medals.head())
>        NOC         Country    Gold  Silver  Bronze
      0  USA   United States  2088.0  1195.0  1052.0
      1  URS    Soviet Union   838.0   627.0   584.0
      2  GBR  United Kingdom   498.0   591.0   505.0
      3  FRA          France   378.0   461.0   475.0
      4  GER         Germany   407.0   350.0   454.0
```

### Reindexing DataFrames

#### Sorting DataFrame with the Index & columns

`.sort_index()`, `.sort_values()`

```py
# Import pandas
import pandas as pd

# Read 'monthly_max_temp.csv' into a DataFrame: weather1
weather1 = pd.read_csv('monthly_max_temp.csv', index_col='Month')

# Sort the index of weather1 in alphabetical order: weather2
weather2 = weather1.sort_index()

# Sort the index of weather1 in reverse alphabetical order: weather3
weather3 = weather1.sort_index(ascending=False)

# Sort weather1 numerically using the values of 'Max TemperatureF': weather4
weather4 = weather1.sort_values('Max TemperatureF')
```

#### Reindexing DataFrame from a list

```py
# Import pandas
import pandas as pd

# Reindex weather1 using the list year: weather2
weather2 = weather1.reindex(year)

# Print weather2
print(weather2)

# Reindex weather1 using the list year with forward-fill: weather3
weather3 = weather1.reindex(year).ffill()

# Print weather3
print(weather3)
```

#### Reindexing using another DataFrame Index

Use the DataFrame `.reindex()` and `.dropna()` methods to make a DataFrame common_names counting names from 1881 that were still popular in 1981.

```py
> Shape of names_1981 DataFrame: (19455, 1)
> Shape of names_1881 DataFrame: (1935, 1)
# Import pandas
import pandas as pd

# Reindex names_1981 with index of names_1881: common_names
common_names = names_1981.reindex(names_1881.index)

# Print shape of common_names
print(common_names.shape)
> (1935, 1)

# Drop rows with null counts: common_names
common_names = common_names.dropna()

# Print shape of new common_names
print(common_names.shape)
> (1587, 1)
```

### Arithmetic with Series & DataFrames

#### Adding unaligned DataFrames

```py
january
                  Units
Company                
Acme Corporation     19
Hooli                17
Initech              20
Mediacore            10
Streeplex            13

february
                  Units
Company                
Acme Corporation     15
Hooli                 3
Mediacore            13
Vandelay Inc         25

>  print(january + february)
                  Units
Company                
Acme Corporation   34.0
Hooli              20.0
Initech             NaN
Mediacore          23.0
Streeplex           NaN
Vandelay Inc        NaN
```

#### Broadcasting in arithmetic formulas

```py
# Extract selected columns from weather as new DataFrame: temps_f
temps_f = weather[['Min TemperatureF', 'Mean TemperatureF', 'Max TemperatureF']]

# Convert temps_f to celsius: temps_c
temps_c = (temps_f - 32) * 5/9

# Rename 'F' in column names with 'C': temps_c.columns
temps_c.columns = temps_c.columns.str.replace('F', 'C')

# Print first 5 rows of temps_c
print(temps_c.head())
>           Min TemperatureC  Mean TemperatureC  Max TemperatureC
Date                                                             
2013-01-01         -6.111111          -2.222222          0.000000
2013-01-02         -8.333333          -6.111111         -3.888889
2013-01-03         -8.888889          -4.444444          0.000000
2013-01-04         -2.777778          -2.222222         -1.111111
2013-01-05         -3.888889          -1.111111          1.111111
```

#### Computing percentage growth of GDP

`.pct_change()`   
`.resample()`,`.last()`   
[resample tricks](https://zhuanlan.zhihu.com/p/35016415)

```py
# Read 'GDP.csv' into a DataFrame: gdp
gdp = pd.read_csv('GDP.csv', parse_dates=True, index_col='DATE')

# Slice all the gdp data from 2008 onward: post2008
post2008 = gdp.loc['2008'::]

# Print the last 8 rows of post2008
print(post2008.tail(8))

# Resample post2008 by year, keeping last(): yearly
yearly = post2008.resample('A').last()

# Print yearly
print(yearly)

# Compute percentage growth of yearly: yearly['growth']
yearly['growth'] = yearly.pct_change()*100

# Print yearly again
print(yearly)
```

#### Converting currency of stocks

`.multiply()`

```py
# Import pandas
import pandas as pd

# Read 'sp500.csv' into a DataFrame: sp500
sp500 = pd.read_csv('sp500.csv',parse_dates=True, index_col='Date')

# Read 'exchange.csv' into a DataFrame: exchange
exchange = pd.read_csv('exchange.csv', parse_dates=True, index_col='Date')

# Subset 'Open' & 'Close' columns from sp500: dollars
dollars = sp500[['Open', 'Close']]

# Print the head of dollars
print(dollars.head())

# Convert dollars to pounds: pounds
pounds = dollars.multiply(exchange['GBP/USD'], axis='rows')

# Print the head of pounds
print(pounds.head())
```