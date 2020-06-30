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

## Concatenating data

### Appending and concatenating Series

#### Appending pandas Series

`.append()`

```py
# Import pandas
import pandas as pd

# Load 'sales-jan-2015.csv' into a DataFrame: jan
jan = pd.read_csv('sales-jan-2015.csv', parse_dates=True, index_col='Date') # parse_dates=True: 将csv中的时间字符串转换成日期格式

# Load 'sales-feb-2015.csv' into a DataFrame: feb
feb = pd.read_csv('sales-feb-2015.csv', parse_dates=True, index_col='Date')

# Load 'sales-mar-2015.csv' into a DataFrame: mar
mar = pd.read_csv('sales-mar-2015.csv', parse_dates=True, index_col='Date')

# Extract the 'Units' column from jan: jan_units
jan_units = jan['Units']

# Extract the 'Units' column from feb: feb_units
feb_units = feb['Units']

# Extract the 'Units' column from mar: mar_units
mar_units = mar['Units']

# Append feb_units and then mar_units to jan_units: quarter1
quarter1 = jan_units.append(feb_units).append(mar_units)

# Print the first slice from quarter1
print(quarter1.loc['jan 27, 2015':'feb 2, 2015'])
> Date
  2015-01-27 07:11:55    18
  2015-02-02 08:33:01     3
  2015-02-02 20:54:49     9
  Name: Units, dtype: int64

# Print the second slice from quarter1
print(quarter1.loc['feb 26, 2015':'mar 7, 2015'])
> Date
  2015-02-26 08:57:45     4
  2015-02-26 08:58:51     1
  2015-03-06 10:11:45    17
  2015-03-06 02:03:56    17
  Name: Units, dtype: int64

# Compute & print total sales in quarter1
print(quarter1.sum())
> 642
```

#### Concatenating pandas Series along row axis

`.append()` is a specific case of a concatenation, while `pd.concat()` gives you more flexibility, 

```py
# Initialize empty list: units
units = []

# Build the list of Series
# Use a for loop to iterate over [jan, feb, mar]:
# In each iteration of the loop, append the 'Units' column of each DataFrame to units.
for month in [jan, feb, mar]:
    units.append(month['Units'])

# Concatenate the Series contained in the list units into a longer Series called quarter1 using pd.concat().
quarter1 = pd.concat(units, axis='rows') # set axis='rows' or axis=0 to stack the Series vertically(列对齐). 

# Print slices from quarter1. Verify that quarter1 has the individual Series stacked vertically by printing slices.
print(quarter1.loc['jan 27, 2015':'feb 2, 2015'])
print(quarter1.loc['feb 26, 2015':'mar 7, 2015'])
> 
Date
2015-01-27 07:11:55    18
2015-02-02 08:33:01     3
2015-02-02 20:54:49     9
Name: Units, dtype: int64
Date
2015-02-26 08:57:45     4
2015-02-26 08:58:51     1
2015-03-06 10:11:45    17
2015-03-06 02:03:56    17
Name: Units, dtype: int64
```

### Appending and concatenating DataFrames

#### Appending DataFrames with ignore_index

```py
# Add 'year' column to names_1881 and names_1981
names_1881['year'] = 1881
names_1981['year'] = 1981

# Append names_1981 after names_1881 with ignore_index=True: combined_names
combined_names = names_1881.append(names_1981, ignore_index=True) # ignore_index=True to make a new RangeIndex of unique integers for each row.

# Print shapes of names_1981, names_1881, and combined_names
print(names_1981.shape)
> (19455, 4)
print(names_1881.shape)
> (1935, 4)
print(combined_names.shape)
> (21390, 4)

# Extract all rows from combined_names that have the name 'Morgan'. To do this, use the .loc[] accessor with an appropriate filter. The relevant column of combined_names here is 'name'.
print(combined_names.loc[combined_names['name']=='Morgan'])
>          name gender  count  year
  1283   Morgan      M     23  1881
  2096   Morgan      F   1769  1981
  14390  Morgan      M    766  1981 
```

#### Concatenating pandas DataFrames along column axis

The function `pd.concat()` can concatenate DataFrames horizontally as well as vertically (vertical is the default). To make the DataFrames stack horizontally, you have to specify the keyword argument `axis=1` or `axis='columns'`(行对齐).

```py
# Create a list of weather_max and weather_mean
weather_list = [weather_max, weather_mean]

# Concatenate weather_list horizontally
weather = pd.concat(weather_list, axis=1) # specify the keyword argument axis=1 to stack them horizontally

# Print weather
print(weather,head())
>      Max TemperatureF  Mean TemperatureF
  Apr              89.0          53.100000
  Aug               NaN          70.000000
  Dec               NaN          34.935484
  Feb               NaN          28.714286
  Jan              68.0          32.354839
```

#### Reading multiple files to build a DataFrame

```py
#Initialize an empyy list: medals
medals =[]

for medal in medal_types:
    # Create file_name using string interpolation with the loop variable medal
    file_name = "%s_top5.csv" % medal # evaluates as a string with the value of medal replacing %s in the format string.
    # Create list of column names: columns
    columns = ['Country', medal]
    # Read file_name into a DataFrame: medal_df
    medal_df = pd.read_csv(file_name, header=0, index_col='Country', names=columns)
    # Append medal_df to medals
    medals.append(medal_df)

# Concatenate medals horizontally: medals_df
medals_df = pd.concat(medals, axis='columns')

# Print medals_df
print(medals_df)
>                 bronze  silver    gold
  France           475.0   461.0     NaN
  Germany          454.0     NaN   407.0
  Italy              NaN   394.0   460.0
  Soviet Union     584.0   627.0   838.0
  United Kingdom   505.0   591.0   498.0
  United States   1052.0  1195.0  2088.0
```


### Concatenation, keys, and MultiIndexes

#### Concatenating vertically to get MultiIndexed rows

`keys` parameter in the call to `pd.concat()`, which generates a hierarchical index with the labels from keys as the outermost index label.

```py
for medal in medal_types:

    file_name = "%s_top5.csv" % medal
    
    # Read file_name into a DataFrame: medal_df. Specify the index to be 'Country'.
    medal_df = pd.read_csv(file_name, index_col='Country')
    
    # Append medal_df to medals
    medals.append(medal_df)
    
# Concatenate medals: medals
medals = pd.concat(medals, keys=['bronze', 'silver', 'gold'], axis=0)

# Print medals in entirety
print(medals)
>                       Total
       Country               
bronze United States   1052.0
       Soviet Union     584.0
       United Kingdom   505.0
       France           475.0
       Germany          454.0
silver United States   1195.0
       Soviet Union     627.0
       United Kingdom   591.0
       France           461.0
       Italy            394.0
gold   United States   2088.0
       Soviet Union     838.0
       United Kingdom   498.0
       Italy            460.0
       Germany          407.0
```

#### Slicing MultiIndexed DataFrames

Use the `pd.IndexSlice` to extract specific slices.

```py
# Sort the entries of medals: medals_sorted
medals_sorted = medals.sort_index(level=0)

# Print the number of Bronze medals won by Germany
print(medals_sorted.loc[('bronze','Germany')])
> Total    454.0
Name: (bronze, Germany), dtype: float64

# Print data about silver medals
print(medals_sorted.loc['silver'])
>                  Total
  Country               
  France           461.0
  Italy            394.0
  Soviet Union     627.0
  United Kingdom   591.0
  United States   1195.0

# Create an alias for pd.IndexSlice called idx. A slicer pd.IndexSlice is required when slicing on the inner level of a MultiIndex.
idx = pd.IndexSlice

# Print all the data on medals won by the United Kingdom
print(medals_sorted.loc[idx[:,'United Kingdom'], :])
>                        Total
         Country              
  bronze United Kingdom  505.0
  gold   United Kingdom  498.0
  silver United Kingdom  591.0
```

#### Concatenating horizontally to get MultiIndexed columns

```py
# Construct a new DataFrame february with MultiIndexed columns by concatenating the list dataframes
february = pd.concat(dataframes, axis=1, keys=['Hardware', 'Software', 'Service']) # Use axis=1 to stack the DataFrames horizontally and the keyword argument keys=['Hardware', 'Software', 'Service'] to construct a hierarchical Index from each DataFrame.

# Print february.info()
print(february.info())

# Create an alias called idx for pd.IndexSlice
idx = pd.IndexSlice

# Extract a slice called slice_2_8 from february (using .loc[] & idx) that comprises rows between Feb. 2, 2015 to Feb. 8, 2015 from columns under 'Company'.
slice_2_8 = february.loc['2015-02-02':'2015-02-08', idx[:, 'Company']]

# Print slice_2_8
print(slice_2_8)
```

#### Concatenating DataFrames from a dict

```py
# Make the list of tuples: month_list
month_list = [('january', jan), ('february', feb), ('march', mar)]

# Create an empty dictionary: month_dict
month_dict = {}

for month_name, month_data in month_list:

    # Group month_data: month_dict[month_name]. (Group month_data by 'Company' and use .sum() to aggregate.)
    month_dict[month_name] = month_data.groupby('Company').sum()

# Concatenate data in month_dict: sales
sales = pd.concat(month_dict)

# Print sales
print(sales)
>                           Units
         Company               
february Acme Coporation     34
         Hooli               30
         Initech             30
         Mediacore           45
         Streeplex           37
january  Acme Coporation     76
         Hooli               70
         Initech             37
         Mediacore           15
         Streeplex           50
march    Acme Coporation      5
         Hooli               37
         Initech             68
         Mediacore           68
         Streeplex           40

# Print all sales by Mediacore
idx = pd.IndexSlice
print(sales.loc[idx[:, 'Mediacore'], :])
>                     Units
           Company         
  february Mediacore     45
  january  Mediacore     15
  march    Mediacore     68
```

### Outer and inner joins

#### Concatenating DataFrames with inner join

```py
# Create the list of DataFrames: medal_list
medal_list = [bronze, silver, gold]

# Concatenate medal_list horizontally using an inner join: medals
medals = pd.concat(medal_list, keys=['bronze', 'silver', 'gold'], axis=1, join='inner') # Use the keyword argument  to yield suitable hierarchical indexing. Use axis=1 to get horizontal concatenation. Use join='inner' to keep only rows that share common index labels

# Print medals
print(medals)
>               bronze  silver    gold
                 Total   Total   Total
Country                               
United States   1052.0  1195.0  2088.0
Soviet Union     584.0   627.0   838.0
United Kingdom   505.0   591.0   498.0
```

#### Resampling & concatenating DataFrames with inner join

```py
# Resample and tidy china: china_annual. Make a new DataFrame china_annual by resampling the DataFrame china with .resample('A').last() (i.e., with annual frequency) and chaining two method calls.
china_annual = china.resample('A').last().pct_change(10).dropna() # Chain .pct_change(10) as an aggregation method to compute the percentage change with an offset of ten years. Chain .dropna() to eliminate rows containing null values.

# Resample and tidy us: us_annual
us_annual = us.resample('A').last().pct_change(10).dropna()

# Concatenate china_annual and us_annual: gdp
gdp = pd.concat([china_annual, us_annual], join='inner', axis=1) # join='inner' to perform an inner join and use axis=1 to concatenate horizontally.

# Print the result of resampling gdp every decade (i.e., using .resample('10A')) and aggregating with the method .last()
print(gdp.resample('10A').last())
```