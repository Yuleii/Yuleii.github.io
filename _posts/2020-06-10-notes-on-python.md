---
layout: article
title: Notes on Python
key: 20200610
tags: Programming
pageview: false
aside:
  toc: true
---


Based on Datacamp.

<!--more-->

## Lists

### Python Lists

```py
# Create a list

## area variables (in square meters)
hall = 11.25
kit = 18.0
liv = 20.0
bed = 10.75
bath = 9.50

## Create list areas
areas = [hall,kit,liv,bed,bath]

# Create list with different types
## Adapt list areas
areas = ["hallway",hall, "kitchen",kit, "living room", liv, "bedroom",bed, "bathroom", bath]

# List of lists
## house information as list of lists
house = [["hallway", hall],
         ["kitchen", kit],
         ["living room", liv],
         ["bedroom",bed],
         ["bathroom",bath]]
```

### Subsetting Lists

```py
x = ["a", "b", "c", "d"]
# Subset and conquer
x[1]
x[-3] # same result!

# Subset and calculate
print(x[1] + x[3]) # return 'bd'

# Slicing and dicing
# The start index will be included, while the end index is not
my_list[start:end]

x[1:3] #return ['b', 'c']
x[:2] #return ['a', 'b']
x[2:] #return  ['c', 'd']
x[:]  #return ["a", "b", "c", "d"]

# Subsetting lists of lists 
x = [["a", "b", "c"],
     ["d", "e", "f"],
     ["g", "h", "i"]]
x[2][0] #return 'g'
x[2][:2] #return ['g', 'h']
```

### Manipulating Lists
```py
x = ["a", "b", "c", "d"]
# Replace list elements
x[1] = "r"
x[2:] = ["s", "t"] 

# Extend a list
y = x + ["e", "f"] 

# Delete list elements
del(x[1])
```

### Inner workings of lists
```py
# Create list areas
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Create areas_copy
areas_copy = list(areas)

# Change areas_copy
areas_copy[0] = 5.0

# Print areas
print(areas) # Areas dosen't change.But if use areas_copy = areas, when change areas_copy, areas change as well.
```


## Matplotlib 

### dataset 
[Gapminder](https://assets.datacamp.com/production/repositories/287/datasets/5b1e4356f9fa5b5ce32e9bd2b75c777284819cca/gapminder.csv)  
[Car](https://assets.datacamp.com/production/repositories/287/datasets/79b3c22c47a2f45a800c62cae39035ff2ea4e609/cars.csv)  
[BRICS](https://assets.datacamp.com/production/repositories/287/datasets/b60fb5bdbeb4e4ab0545c485d351e6ff5428a155/brics.csv)  
[Python for data science Cheat Sheet](https://datacamp-community-prod.s3.amazonaws.com/e30fbcd9-f595-4a9f-803d-05ca5bf84612) 

### Line plot

> ```py
> import matplotlib.pyplot as plt
> plt.plot(x,y)
> plt.show(
> ```

```py
# Print the last item from year and pop
print(year[-1])
print(pop[-1])

# Import matplotlib.pyplot as plt
import matplotlib.pyplot as plt

# Make a line plot: year on the x-axis, pop on the y-axis
plt.plot(year,pop)

# Display the plot with plt.show()
plt.show()
```

```
# Make a line plot, gdp_cap on the x-axis, life_exp on the y-axis
plt.plot(gdp_cap,life_exp)

# Display the plot
plt.show()
```

### Scatter Plot

> ```py
> import matplotlib.pyplot as plt
> plt.scatter(x,y)
> plt.show()
> ```

```py
import matplotlib.pyplot as plt

# Make a scatter plot, gdp_cap on the x-axis, life_exp on the y-axis
plt.scatter(gdp_cap, life_exp)

# Put the x-axis on a logarithmic scale
plt.xscale('log')

# Display the plot
plt.show()
```

### Histogram

> ```py
> plt.hist(x)
> ```

```py
# Create histogram of life_exp data(Bin=10 by defualt)
plt.hist(life_exp)

# Display histogram and clean up plot
plt.show()
plt.clf()

# Build histogram with 5 bins
plt.hist(life_exp,bins=5)

# Show and clean up plot
plt.show()
plt.clf()
```

### Customization

```py
# A dictionary is constructed that maps continents onto colors
dict = {
    'Asia':'red',
    'Europe':'green',
    'Africa':'blue',
    'Americas':'yellow',
    'Oceania':'black'
}
gm["colour"] = gm["continent"].map(colourDict)

# Scatter plot assingning size(s), colour(c) and transparency(alpha)
plt.scatter(x = gdp_cap, y = life_exp, s = np.array(pop) * 2, c = col, alpha = 0.8)

# Labels
plt.xscale('log') 
plt.xlabel('GDP per Capita [in USD]')
plt.ylabel('Life Expectancy [in years]')
plt.title('World Development in 2007')

# Ticks
plt.xticks([1000,10000,100000], ['1k','10k','100k'])

# Add the words "India" and "China" in the plot.
plt.text(1550, 71, 'India')
plt.text(5700, 80, 'China')

# Add grid() call
plt.grid(True)

# Show the plot
plt.show()
```

## Dictionaries

### Creating a dictionary

> ```py
> # Make sure use lowercase
> # Keys must be immutable
> my_dict = {
>  "key1": value1,
>  "key2": value2,
> }
> ```

```py
# Definition of countries and capital
countries = ['spain', 'france', 'germany', 'norway']
capitals = ['madrid', 'paris', 'berlin', 'oslo']

# From string in countries and capitals, create dictionary europe
europe = { 'spain':'madrid', 'france': 'paris', 'germany':'berlin', 'norway':'oslo'}
```

### Access dictionary

```py
# Print out the keys in europe
print(europe.keys())

# Print out value that belongs to key 'norway'
print(europe['norway'])
```
### Dictionary Manipulation

```py
# Add italy to europe
europe['italy'] = 'rome'

# Print out italy in europe, output should be true or false
print('italy' in europe)

# Add poland to europe
europe['poland'] = 'warsaw'
```

```py
# Definition of dictionary
europe = {'spain':'madrid', 'france':'paris', 'germany':'bonn',
          'norway':'oslo', 'italy':'rome', 'poland':'warsaw',
          'australia':'vienna' }

# Update capital of germany, bonn to berlin 
europe['germany'] = 'berlin'

# Remove australia
del(europe['australia'])
```

### Dictionariception

```py
# Dictionary of dictionaries(嵌套)
europe = { 'spain': { 'capital':'madrid', 'population':46.77 },
           'france': { 'capital':'paris', 'population':66.03 },
           'germany': { 'capital':'berlin', 'population':80.62 },
           'norway': { 'capital':'oslo', 'population':5.084 } }


# Print out the capital of France
print(europe['france']['capital'])

# Create sub-dictionary data
data = {'capital':'rome', 'population':59.83 }

# Add data to europe under key 'italy'
europe['italy']=data

# Print europe
print(europe)
```

## Pandas

### Dictionary to DataFrame 

```py
# Pre-defined lists
names = ['United States', 'Australia', 'Japan', 'India', 'Russia', 'Morocco', 'Egypt']
dr =  [True, False, False, False, True, True, True]
cpc = [809, 731, 588, 18, 200, 70, 45]

# Import pandas as pd
import pandas as pd

# Create dictionary my_dict with three key:value pairs: my_dict
my_dict = {'country': names,'drives_right': dr,'cars_per_cap':cpc}

# Build a DataFrame cars from my_dict: cars
cars = pd.DataFrame(my_dict)

# Definition of row_labels
row_labels = ['US', 'AUS', 'JPN', 'IN', 'RU', 'MOR', 'EG']

# Specify row labels of cars
cars.index = row_labels
```

### CSV to DataFrame
```py
# Import the cars.csv data: cars
# 括号里的文件名称要打引号
cars = pd.read_csv('cars.csv')

# The first column is used as row labels
cars = pd.read_csv('cars.csv',index_col=0)
```
> ```py
>      cars_per_cap        country  drives_right
> US            809  United States          True
> AUS           731      Australia         False
> JPN           588          Japan         False
> IN             18          India         False
> RU            200         Russia          True
> MOR            70        Morocco          True
> EG             45          Egypt          True
> ```
 
### Square Brackets

> ```py
> # To select only the cars_per_cap column from cars
> # The single bracket version gives a Pandas Series, the double bracket version gives a Pandas DataFrame.
> # 记得引号!
> cars['cars_per_cap'] # 返回Pandas Series，2列，左边列是属性，右边列是值
> cars[['cars_per_cap']] # 返回Pandas DataFrame，2行，第一行是属性，第二行是值
> ```

- Select column
  
```py
# Print out country column as Pandas Series
print(cars['country'])

# Print out country column as Pandas DataFrame
print(cars[['country']])

# Print out DataFrame with country and drives_right columns
print(cars[['country','drives_right']])
```

- Select row
  
```py
# Print out first 3 observations
print(cars[0:4])

# Print out fourth, fifth and sixth observation
print(cars[3:6])
```

### loc and iloc

- loc is label-based  
- iloc is integer index base

```py
# Each pair of commands here gives the same result.
cars.loc['RU']
cars.iloc[4]
 
cars.loc[['RU']]
cars.iloc[[4]]
 
cars.loc[['RU', 'AUS']]
cars.iloc[[4, 1]]
```

- select rows or columns from a DataFrame

```py
# Print out observation for Japan as a Series
print(cars.loc['JPN'])
print(cars.iloc[4])

# Print out observations for Australia and Egypt as DataFrame
print(cars.loc[['AUS','EG']])
print(cars.iloc[[1,6]])
```

- select both rows and columns from a DataFrame

```py
# Each pair of commands here gives the same result.
cars.loc['IN', 'cars_per_cap']
cars.iloc[3, 0]

cars.loc[['IN', 'RU'], 'cars_per_cap']
cars.iloc[[3, 4], 0]

cars.loc[['IN', 'RU'], ['cars_per_cap', 'country']]
cars.iloc[[3, 4], [0, 1]]
```


- select only columns
  
```py
# Each pair of commands here gives the same result.
cars.loc[:, 'country']
cars.iloc[:, 1]

cars.loc[:, ['country','drives_right']]
cars.iloc[:, [1, 2]]
```