---
layout: article
title: Merging DataFrames with pandas
key: 20200627
tags: Python Pandas DataAnalysis
modify_date: 2020-07-01
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

[PANDAS 数据合并与重塑（concat篇）](https://blog.csdn.net/stevenkwong/article/details/52528616)

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

[10分钟带你学会Pandas多层级索引](https://zhuanlan.zhihu.com/p/74461994)

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

## Merging data

### Merging DataFrames

#### Merging company DataFrames

```py
revenue
>         city  revenue
0       Austin      100
1       Denver       83
2  Springfield        4

managers
>      city   manager
0     Austin  Charlers
1     Denver      Joel
2  Mendocino     Brett

combined = pd.merge(revenue, managers, on='city') # 保留City中的重合行, 默认inner join。
>    city  revenue   manager
0  Austin      100  Charlers
1  Denver       83      Joel
```

#### Merging on a specific column

> ```py
> print(revenue)
>         city  branch_id  revenue
> 0       Austin         10      100
> 1       Denver         20       83
> 2  Springfield         30        4
> 3    Mendocino         47      200
>
> print(managers)
>          city  branch_id  manager
> 0       Austin         10  Charles
> 1       Denver         20     Joel
> 2    Mendocino         47    Brett
> 3  Springfield         31    Sally
> ```

```py
# Merge revenue with managers on 'city': merge_by_city
merge_by_city = pd.merge(revenue, managers, on='city')

# Print merge_by_city
print(merge_by_city)
>         city  branch_id_x  revenue  branch_id_y  manager
0       Austin           10      100           10  Charles
1       Denver           20       83           20     Joel
2  Springfield           30        4           31    Sally
3    Mendocino           47      200           47    Brett

# Merge revenue with managers on 'branch_id': merge_by_id
merge_by_id = pd.merge(revenue, managers, on='branch_id')

# Print merge_by_id
print(merge_by_id)
>     city_x  branch_id  revenue     city_y  manager
0     Austin         10      100     Austin  Charles
1     Denver         20       83     Denver     Joel
2  Mendocino         47      200  Mendocino    Brett
```

#### Merging on columns with non-matching labels

> ```py
> In [1]: revenue
> Out[2]: 
>           city  branch_id state  revenue
> 0       Austin         10    TX      100
> 1       Denver         20    CO       83
> 2  Springfield         30    IL        4
> 3    Mendocino         47    CA      200
>
> In [2]: managers
> Out[2]: 
>         branch  branch_id state   manager
> 0       Austin         10    TX  Charlers
> 1       Denver         20    CO      Joel
> 2    Mendocino         47    CA     Brett
> 3  Springfield         31    MO     Sally
>
> In [3]: sales
> Out[3]: 
>         city state  units
> 0    Mendocino    CA      1
> 1       Denver    CO      4
> 2       Austin    TX      2
> 3  Springfield    MO      5
> 4  Springfield    IL      1
>```

```py
# Merge the DataFrames revenue and managers into a single DataFrame called combined using the 'city' and 'branch' columns from the appropriate DataFrames.
combined = pd.merge(revenue, managers, left_on='city', right_on='branch')

# Print combined
print(combined)
>         city  branch_id_x state_x  revenue       branch  branch_id_y state_y   manager
0       Austin           10      TX      100       Austin           10      TX  Charlers
1       Denver           20      CO       83       Denver           20      CO      Joel
2  Springfield           30      IL        4  Springfield           31      MO     Sally
3    Mendocino           47      CA      200    Mendocino           47      CA     Brett
```

#### Merging on multiple columns

```py
# Add 'state' column to revenue: revenue['state']
revenue['state'] = ['TX','CO','IL','CA']

# Add 'state' column to managers: managers['state']
managers['state'] = ['TX','CO','CA','MO']

# Merge the DataFrames revenue and managers using three columns :'branch_id', 'city', and 'state'. Pass them in as a list to the on paramater of pd.merge()
combined = pd.merge(revenue, managers, on=['branch_id', 'city', 'state'])

# Print combined
print(combined)
>       city  branch_id  revenue state   manager
0     Austin         10      100    TX  Charlers
1     Denver         20       83    CO      Joel
2  Mendocino         47      200    CA     Brett
```

### Joining DataFrames

#### Joining by Index

```py
revenue.join(managers, lsuffix='_rev', rsuffix='_mng', how='outer')>                  city state_rev  revenue       branch state_mng   manager
branch_id                                                                 
10              Austin        TX    100.0       Austin        TX  Charlers
20              Denver        CO     83.0       Denver        CO      Joel
30         Springfield        IL      4.0          NaN       NaN       NaN
31                 NaN       NaN      NaN  Springfield        MO     Sally
47           Mendocino        CA    200.0    Mendocino        CA     Brett
```

#### Left & right merging on multiple columns

```py
# Execute a right merge using pd.merge() with revenue and sales to yield a new DataFrame revenue_and_sales
revenue_and_sales = pd.merge(revenue, sales, how='right', on=['city', 'state'])

# Print revenue_and_sales
print(revenue_and_sales)
>         city  branch_id state  revenue  units
0       Austin       10.0    TX    100.0      2
1       Denver       20.0    CO     83.0      4
2  Springfield       30.0    IL      4.0      1
3    Mendocino       47.0    CA    200.0      1
4  Springfield        NaN    MO      NaN      5

# Execute a left merge with sales and managers to yield a new DataFrame sales_and_managers
sales_and_managers = pd.merge(sales, managers, how='left', left_on=['city', 'state'], right_on=['branch', 'state'])

# Print sales_and_managers
print(sales_and_managers)
>         city state  units       branch  branch_id   manager
0    Mendocino    CA      1    Mendocino       47.0     Brett
1       Denver    CO      4       Denver       20.0      Joel
2       Austin    TX      2       Austin       10.0  Charlers
3  Springfield    MO      5  Springfield       31.0     Sally
4  Springfield    IL      1          NaN        NaN       NaN
```

#### Merging DataFrames with outer join

```py
# Perform the first merge: merge_default
merge_default = pd.merge(sales_and_managers, revenue_and_sales)

# Print merge_default
print(merge_default)
>       city state  units     branch  branch_id   manager  revenue
0  Mendocino    CA      1  Mendocino       47.0     Brett    200.0
1     Denver    CO      4     Denver       20.0      Joel     83.0
2     Austin    TX      2     Austin       10.0  Charlers    100.0

# Perform the second merge: merge_outer
merge_outer = pd.merge(sales_and_managers, revenue_and_sales, how='outer')

# Print merge_outer
print(merge_outer)
>         city state  units       branch  branch_id   manager  revenue
0    Mendocino    CA      1    Mendocino       47.0     Brett    200.0
1       Denver    CO      4       Denver       20.0      Joel     83.0
2       Austin    TX      2       Austin       10.0  Charlers    100.0
3  Springfield    MO      5  Springfield       31.0     Sally      NaN
4  Springfield    IL      1          NaN        NaN       NaN      NaN
5  Springfield    IL      1          NaN       30.0       NaN      4.0
6  Springfield    MO      5          NaN        NaN       NaN      NaN


# Perform the third merge: merge_outer_on
merge_outer_on = pd.merge(sales_and_managers, revenue_and_sales, how='outer', on=['city','state'])

# Print merge_outer_on
print(merge_outer_on)
>         city state  units_x       branch  branch_id_x   manager  branch_id_y  revenue  units_y
0    Mendocino    CA        1    Mendocino         47.0     Brett         47.0    200.0        1
1       Denver    CO        4       Denver         20.0      Joel         20.0     83.0        4
2       Austin    TX        2       Austin         10.0  Charlers         10.0    100.0        2
3  Springfield    MO        5  Springfield         31.0     Sally          NaN      NaN        5
4  Springfield    IL        1          NaN          NaN       NaN         30.0      4.0        1
```

### Ordered merges

`pd.merge_ordered()`

```py
austin
        date ratings
0 2016-01-01  Cloudy
1 2016-02-08  Cloudy
2 2016-01-17   Sunny

houston
        date ratings
0 2016-01-04   Rainy
1 2016-01-01  Cloudy
2 2016-03-01   Sunny

# Perform the first ordered merge: tx_weather
tx_weather = pd.merge_ordered(austin, houston) # it is not possible to tell which observation came from which city.

# Print tx_weather
print(tx_weather)
>       date ratings
0 2016-01-01  Cloudy
1 2016-01-04   Rainy
2 2016-01-17   Sunny
3 2016-02-08  Cloudy
4 2016-03-01   Sunny

# Perform the second ordered merge: tx_weather_suff
tx_weather_suff = pd.merge_ordered(austin, houston, on='date', suffixes=['_aus','_hus']) # suffixes make the rows can be distinguished
>       date ratings_aus ratings_hus
0 2016-01-01      Cloudy      Cloudy
1 2016-01-04         NaN       Rainy
2 2016-01-17       Sunny         NaN
3 2016-02-08      Cloudy         NaN
4 2016-03-01         NaN       Sunny

# Print tx_weather_suff
print(tx_weather_suff)

# Perform the third ordered merge: tx_weather_ffill
tx_weather_ffill = pd.merge_ordered(austin, houston, on='date', suffixes=['_aus','_hus'], fill_method='ffill') # use forward-filling to replace NaN entries with the most recent non-null entry,

# Print tx_weather_ffill
print(tx_weather_ffill)
>       date ratings_aus ratings_hus
0 2016-01-01      Cloudy      Cloudy
1 2016-01-04      Cloudy       Rainy
2 2016-01-17       Sunny       Rainy
3 2016-02-08      Cloudy       Rainy
4 2016-03-01      Cloudy       Sunny
```

#### Using merge_asof()

Similar to `pd.merge_ordered()`, the `pd.merge_asof()` function will also merge values in order using the `on` column, but for each row in the left DataFrame, only rows from the right DataFrame whose `'on'` column values are less than the left value will be kept.

```py
In [4]: auto.head()
Out[4]: 
    mpg  cyl  displ   hp  weight  accel         yr origin                       name
0  18.0    8  307.0  130    3504   12.0 1970-01-01     US  chevrolet chevelle malibu
1  15.0    8  350.0  165    3693   11.5 1970-01-01     US          buick skylark 320
2  18.0    8  318.0  150    3436   11.0 1970-01-01     US         plymouth satellite
3  16.0    8  304.0  150    3433   12.0 1970-01-01     US              amc rebel sst
4  17.0    8  302.0  140    3449   10.5 1970-01-01     US                ford torino

In [6]: oil.head()
Out[6]: 
        Date  Price
0 1970-01-01   3.35
1 1970-02-01   3.35
2 1970-03-01   3.35
3 1970-04-01   3.35
4 1970-05-01   3.35

# Merge auto and oil using pd.merge_asof() with left_on='yr' and right_on='Date'. Store the result as merged.
merged = pd.merge_asof(auto, oil, left_on='yr', right_on='Date')

# Print the tail of merged
print(merged.tail())
>     mpg  cyl  displ  hp  weight  ...         yr  origin             name       Date  Price
387  27.0    4  140.0  86    2790  ... 1982-01-01      US  ford mustang gl 1982-01-01  33.85
388  44.0    4   97.0  52    2130  ... 1982-01-01  Europe        vw pickup 1982-01-01  33.85
389  32.0    4  135.0  84    2295  ... 1982-01-01      US    dodge rampage 1982-01-01  33.85
390  28.0    4  120.0  79    2625  ... 1982-01-01      US      ford ranger 1982-01-01  33.85
391  31.0    4  119.0  82    2720  ... 1982-01-01      US       chevy s-10 1982-01-01  33.85 

# Resample merged using 'A' (annual frequency), and on='Date'. Select [['mpg','Price']] and aggregate the mean. Store the result as yearly.
yearly = merged.resample('A', on='Date')[['mpg','Price']].mean()

# Print yearly
print(yearly.head())
>                 mpg  Price
Date                        
1970-12-31  17.689655   3.35
1971-12-31  21.111111   3.56
1972-12-31  18.714286   3.56
1973-12-31  17.100000   3.56
1974-12-31  22.769231  10.11

# print yearly.corr()
print(yearly.corr())
>           mpg     Price
mpg    1.000000  0.948677
Price  0.948677  1.000000
```

## Case Study - Summer Olympics

[The Guardian's Olympic medal dataset](https://www.theguardian.com/sport/datablog/2012/jun/25/olympic-medal-winner-list-data)

### Medals in the Summer Olympics

#### Loading Olympic edition DataFrame

```py
#Import pandas
import pandas as pd

# Create file path: file_path
file_path = 'Summer Olympic medallists 1896 to 2008 - EDITIONS.tsv'

# Load DataFrame from file_path: editions
editions = pd.read_csv(file_path, sep='\t')

# Extract the relevant columns: editions
editions = editions[['Edition','Grand Total','City','Country']]

# Print editions DataFrame
print(editions.head())
>  Edition  Grand Total       City         Country
0     1896          151     Athens          Greece
1     1900          512      Paris          France
2     1904          470  St. Louis   United States
3     1908          804     London  United Kingdom
4     1912          885  Stockholm          Sweden
```

#### Loading IOC codes DataFrame

```py
# Import pandas
import pandas as pd

# Create the file path: file_path
file_path = 'Summer Olympic medallists 1896 to 2008 - IOC COUNTRY CODES.csv'

# Load DataFrame from file_path: ioc_codes
ioc_codes = pd.read_csv(file_path)

# Extract the relevant columns: ioc_codes
ioc_codes = ioc_codes[['Country','NOC']]

# Print first and last 5 rows of ioc_codes
print(ioc_codes.head())
>          Country  NOC
0      Afghanistan  AFG
1          Albania  ALB
2          Algeria  ALG
3  American Samoa*  ASA
4          Andorra  AND
print(ioc_codes.tail())
```

#### Building medals DataFrame

You have a sequence of files `summer_1896.csv`, `summer_1900.csv`, …, `summer_2008.csv`, one for each Olympic edition (year).

You will build up a dictionary `medals_dict` with the Olympic editions (years) as keys and DataFrames as values.

```py
In [8]: pd.read_csv('summer_1896.csv').columns
Out[8]: Index(['Sport', 'Discipline', 'Athlete', 'NOC', 'Gender', 'Event', 'Event_gender', 'Medal'], dtype='object')

# Import pandas
import pandas as pd

# Create empty dictionary: medals_dict
medals_dict = {}

for year in editions['Edition']:

    # Create the file path: file_path
    file_path = 'summer_{:d}.csv'.format(year)
    
    # Load file_path into a DataFrame: medals_dict[year]
    medals_dict[year] = pd.read_csv(file_path)
    
    # Extract relevant columns: medals_dict[year]
    medals_dict[year] = medals_dict[year][['Athlete', 'NOC', 'Medal']]
    
    # Create a new column called 'Edition' in the DataFrame medals_dict[year] whose entries are all year
    medals_dict[year]['Edition'] = year
    
# Concatenate medals_dict: medals
medals = pd.concat(medals_dict, ignore_index=True) # Specify the keyword argument ignore_index=True to prevent repeated integer indices

# Print first and last 5 rows of medals
print(medals.head())
>             Athlete  NOC   Medal  Edition
0       HAJOS, Alfred  HUN    Gold     1896
1    HERSCHMANN, Otto  AUT  Silver     1896
2   DRIVAS, Dimitrios  GRE  Bronze     1896
3  MALOKINIS, Ioannis  GRE    Gold     1896
4  CHASAPIS, Spiridon  GRE  Silver     1896
print(medals.tail())
```

### Quantifying performance

#### Counting medals by country/edition in a pivot table

```py
# Construct a pivot table from the DataFrame medals, aggregating by count (by specifying the aggfunc parameter). Use 'Edition' as the index, 'Athlete' for the values, and 'NOC' for the columns
medal_counts = medals.pivot_table(values='Athlete', index='Edition', columns='NOC', aggfunc='count')

# Print the first & last 5 rows of medal_counts
print(medal_counts.head())
In [1]:
NOC      AFG  AHO  ALG   ANZ  ARG  ...  VIE  YUG  ZAM  ZIM   ZZX
Edition                            ...                          
1896     NaN  NaN  NaN   NaN  NaN  ...  NaN  NaN  NaN  NaN   6.0
1900     NaN  NaN  NaN   NaN  NaN  ...  NaN  NaN  NaN  NaN  34.0
1904     NaN  NaN  NaN   NaN  NaN  ...  NaN  NaN  NaN  NaN   8.0
1908     NaN  NaN  NaN  19.0  NaN  ...  NaN  NaN  NaN  NaN   NaN
1912     NaN  NaN  NaN  10.0  NaN  ...  NaN  NaN  NaN  NaN   NaN

[5 rows x 138 columns]
print(medal_counts.tail())
```

#### Computing fraction of medals per Olympic edition

```py
# Set Index of editions: totals
totals = editions.set_index('Edition')

# Reassign totals['Grand Total']: totals
totals = totals['Grand Total']

# Divide the DataFrame medal_counts by totals along each row.
fractions = medal_counts.divide(totals, axis='rows')

# Print first & last 5 rows of fractions
print(fractions.head())
In [1]:
NOC      AFG  AHO  ALG       ANZ  ARG  ...  VIE  YUG  ZAM  ZIM       ZZX
Edition                                ...                              
1896     NaN  NaN  NaN       NaN  NaN  ...  NaN  NaN  NaN  NaN  0.039735
1900     NaN  NaN  NaN       NaN  NaN  ...  NaN  NaN  NaN  NaN  0.066406
1904     NaN  NaN  NaN       NaN  NaN  ...  NaN  NaN  NaN  NaN  0.017021
1908     NaN  NaN  NaN  0.023632  NaN  ...  NaN  NaN  NaN  NaN       NaN
1912     NaN  NaN  NaN  0.011299  NaN  ...  NaN  NaN  NaN  NaN       NaN
print(fractions.tail())
```

#### Computing percentage change in fraction of medals won

[.expanding():](https://zhuanlan.zhihu.com/p/35988429)

```py
# Create mean_fractions by chaining the methods .expanding().mean() to fraction
mean_fractions = fractions.expanding().mean()

# Compute the percentage change in mean_fractions down each column by applying .pct_change() and multiplying by 100: fractions_change
fractions_change = mean_fractions.pct_change()*100

# Reset the index of fractions_change: fractions_change
fractions_change = fractions_change.reset_index() #  This will make 'Edition' an ordinary column.

# Print first & last 5 rows of fractions_change
print(fractions_change.head())
In [1]:
NOC  Edition  AFG  AHO  ALG        ANZ  ...  VIE  YUG  ZAM  ZIM        ZZX
0       1896  NaN  NaN  NaN        NaN  ...  NaN  NaN  NaN  NaN        NaN
1       1900  NaN  NaN  NaN        NaN  ...  NaN  NaN  NaN  NaN  33.561198
2       1904  NaN  NaN  NaN        NaN  ...  NaN  NaN  NaN  NaN -22.642384
3       1908  NaN  NaN  NaN        NaN  ...  NaN  NaN  NaN  NaN   0.000000
4       1912  NaN  NaN  NaN -26.092774  ...  NaN  NaN  NaN  NaN   0.000000

print(fractions_change.tail())
```

### Reshaping and plotting

#### Building hosts DataFrame

```py
# Import pandas
import pandas as pd

# Left join editions and ioc_codes: hosts
hosts = pd.merge(editions, ioc_codes, how='left')

# Extract relevant columns and set index: hosts
hosts = hosts[['Edition','NOC']].set_index('Edition')

# Fix missing 'NOC' values of hosts. Use the .loc[] accessor to find and assign the missing values to the 'NOC' column in hosts.
print(hosts.loc[hosts.NOC.isnull()])
>         NOC
Edition     
1972     NaN
1980     NaN
1988     NaN
hosts.loc[1972, 'NOC'] = 'FRG'
hosts.loc[1980, 'NOC'] = 'URS'
hosts.loc[1988, 'NOC'] = 'KOR'

# Reset Index of hosts: hosts
hosts = hosts.reset_index()

# Print hosts
print(hosts)
>  Edition  NOC
0     1896  GRE
1     1900  FRA
2     1904  USA
3     1908  GBR
4     1912  SWE
```

#### Reshaping for analysis

`pd.melt()`

```py
# Import pandas
import pandas as pd

# Reshape fractions_change: reshaped
reshaped = pd.melt(fractions_change, id_vars='Edition', value_name='Change') # id_vars='Edition' to set the identifier variable. value_name='Change' to set the measured variables.

# Print reshaped.shape and fractions_change.shape
print(reshaped.shape, fractions_change.shape)
> (3588, 3) (26, 139)

# Extract rows from reshaped where 'NOC' == 'CHN': chn
chn = reshaped[reshaped['NOC']=='CHN']

# Print last 5 rows of chn with .tail()
print(chn.tail())
>    Edition  NOC     Change
567     1992  CHN   4.240630
568     1996  CHN   7.860247
569     2000  CHN  -3.851278
570     2004  CHN   0.128863
571     2008  CHN  13.251332
```

#### Merging to compute influence

```py
# Import pandas
import pandas as pd

# Merge reshaped and hosts using an inner join: merged
merged = pd.merge(reshaped, hosts, how='inner')

# Print first 5 rows of merged
print(merged.head())
>  Edition  NOC     Change
0     1956  AUS  54.615063
1     2000  AUS  12.554986
2     1920  BEL  54.757887
3     1976  CAN  -2.143977
4     2008  CHN  13.251332

# Set the index of merged to be 'Edition' and sort the index.: influence
influence = merged.set_index('Edition').sort_index()

# Print first 5 rows of influence
print(influence.head())
>        NOC      Change
Edition                 
1896     GRE         NaN
1900     FRA  198.002486
1904     USA  199.651245
1908     GBR  134.489218
1912     SWE   71.896226
```

#### Plotting influence of host country

```py
# Import pyplot
import matplotlib.pyplot as plt

# Extract influence['Change']: change
change = influence['Change']

# Make bar plot of change: ax
ax = change.plot(kind='bar') # Save the result as ax to permit further customization.

# Customize the plot to improve readability
ax.set_ylabel("% Change of Host Country Medal Count")
ax.set_title("Is there a Host Country Advantage?")
ax.set_xticklabels(editions['City'])

# Display the plot
plt.show()
```