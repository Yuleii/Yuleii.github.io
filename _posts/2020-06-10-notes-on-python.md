---
layout: article
title: Notes on Python
key: 20200610
tags: Python
pageview: false
modify_date: 2020-06-11
aside:
  toc: true
---


Based on DataCamp.

<!--more-->

## Lists

### Create Lists

```py
# Create list areas
hall = 11.25
kit = 18.0
liv = 20.0
bed = 10.75
bath = 9.50
areas = [hall,kit,liv,bed,bath]

# Create list with different types
areas = ["hallway",hall, "kitchen",kit, "living room", liv, "bedroom",bed, "bathroom", bath]

# List of lists
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
print(x[1] + x[3])
> bd

# Slicing and dicing. (The start index will be included, while the end index is not)
my_list[start:end]

x[1:3]  
> ['b', 'c']
x[:2]  
> ['a', 'b']
x[2:]  
> ['c', 'd']
x[:]  
> ["a", "b", "c", "d"]

# Subsetting lists of lists
x = [["a", "b", "c"],
     ["d", "e", "f"],
     ["g", "h", "i"]]
x[2][0]
> 'g'
x[2][:2]
> ['g', 'h']
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

### Inner Workings of Lists

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

## Functions and Packages

### [Built-in Functions](https://docs.python.org/3/library/functions.html#bool)

```py
# Familiar functions
print()
type()

# switch between data types
str()
int()
bool()
float()

# Help!
help(max)
?max
```

### Methods

- string Methods

```py
place = "poolhouse"
place_up=place.upper()
> POOLHOUSE
print(place.count('o')) # Print out the number of o's in place (3)
```

- List Methods
  
>```py
> index() # to get the index of the first element of a list that matches its input
> count() # to get the number of times an element appears in a list
> append() # that adds an element to the list it is called on
> remove() # remove the first element of a list that matches the input
> reverse() # reverse the order of the elements in the list it is called on.
> ```

```py
areas = [11.25, 18.0, 20.0, 10.75, 9.50]
# Print out the index of the element 20.0
print(areas.index(20.0))

# Print out how often 9.50 appears in areas
print(areas.count(9.50))

# Use append twice to add poolhouse and garage size
areas.append(24.5)
areas.append(15.45)

# Reverse the orders of the elements in areas
areas.reverse()
```

### Packages

```py
# Import package
## Import the math package
import math
r = 0.43 # Definition of radius
C = 2*math.pi*r # Calculate C=2πr
A = math.pi*r**2 # Calculate A=πr^2

# Selective import
## Import radians function of math package
from math import radians
r = 192500 # Definition of radius
dist=r*radians(12) # Travel distance of Moon over 12 degrees. Store in dist.
```

## NumPy

### NumPy Array

```py
# Import the numpy package as np
import numpy as np

# Create a numpy array
baseball = [180, 215, 210, 210, 188, 176, 209, 200]
np_baseball=np.array(baseball)

# Calculate the BMI: bmi
np_height_m = np.array(height_in) * 0.0254
np_weight_kg = np.array(weight_lb) * 0.453592
bmi = np_weight_kg / np_height_m ** 2

# Boolean numpy arrays
x = [4 , 9 , 6, 3, 1]
import numpy as np
y = np.array(x)
high = y > 5
> array([False,  True,  True, False, False])
y[high]  
> array([9, 6])

# type coercion. (Numpy arrays cannot contain elements with different types. If you try to build such a list, some of the elements' types are changed to end up with a homogeneous list.)
np.array([True, 1, 2]) + np.array([3, 4, False])
np.array([4, 3, 0]) + np.array([0, 2, 2]) # same result!
```

### 2D NumPy Array

- Create 2D NumPy Arrays

```py
# Create baseball, a list of lists
baseball = [[180, 78.4],
            [215, 102.7],
            [210, 98.5],
            [188, 75.2]]

# Import numpy
import numpy as np

# Create a 2D numpy array from baseball: np_baseball
np_baseball=np.array(baseball)
print(type(np_baseball))
> <class 'numpy.ndarray'>  
print(np_baseball.shape)
> (4, 2)
```

- Subsetting 2D NumPy Arrays
  
```py
## Create np_baseball (2 cols)
np_baseball = np.array(baseball)

## Print out the 50th row of np_baseball
print(np_baseball[49,:])

## Select the entire second column of np_baseball: np_weight_lb
np_weight_lb=np_baseball[:,1]

## Print out height of 124th player
print(np_baseball[123,0])
```

- 2D Arithmetic

```py
# numpy was able to perform all calculations element-wise.
import numpy as np
np_mat = np.array([[1, 2],
                   [3, 4],
                   [5, 6]])
np_mat * 2
>  array([[ 2,  4],
>         [ 6,  8],
>         [10, 12]])  
np_mat + np.array([10, 10])  
>array([[11, 12],
>      [13, 14],
>      [15, 16]])
```

### Basic Statistics

```py
import numpy as np
x = [1, 4, 8, 10, 12]
np.mean(x) # 7.0
np.median(x) # 8.0
np.std(x)
np.corrcoef(x,y)
```

## Matplotlib

[Python for data science Cheat Sheet](https://datacamp-community-prod.s3.amazonaws.com/e30fbcd9-f595-4a9f-803d-05ca5bf84612)

### Dataset

- [Gapminder](https://assets.datacamp.com/production/repositories/287/datasets/5b1e4356f9fa5b5ce32e9bd2b75c777284819cca/gapminder.csv)  
- [Car](https://assets.datacamp.com/production/repositories/287/datasets/79b3c22c47a2f45a800c62cae39035ff2ea4e609/cars.csv)  
- [BRICS](https://assets.datacamp.com/production/repositories/287/datasets/b60fb5bdbeb4e4ab0545c485d351e6ff5428a155/brics.csv)  

### Line Plot

> ```py
> import matplotlib.pyplot as plt
> plt.plot(x,y)
> plt.show(
> ```

```py
# Import matplotlib.pyplot as plt
import matplotlib.pyplot as plt

# Make a line plot: year on the x-axis, pop on the y-axis
plt.plot(year,pop)

# Display the plot with plt.show()
plt.show()
```

```py
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

## Logic, Control Flow and Filtering

### Comparison Operators

`>`, `<`, `>=`, `<=`, `==`, `!=`

```py
# Equality
True == False # return False
-5 * 15 != 75 # return True
"pyscript" == "PyScript" # return False
True == 1 # return True

# Greater and less than
x = -3 * 6
x >= -10 # return False

y = "test"
"test"<=y # return True
True > False # return True

# Compare arrays(element-wise)
## Create arrays
import numpy as np
my_house = np.array([18.0, 20.0, 10.75, 9.50])
your_house = np.array([14.0, 24.0, 14.25, 9.0])

## my_house greater than or equal to 18
print(my_house >= 18)
> [ True  True False False]

## my_house less than your_house
print(my_house <= your_house)
> [ True  True False False]
```

### Boolean Operators

- `and`, `or`, `not`

```py
# Define variables
my_kitchen = 18.0
your_kitchen = 14.0

# my_kitchen bigger than 10 and smaller than 18?
print(my_kitchen > 10 and my_kitchen < 18)

# my_kitchen smaller than 14 or bigger than 17?
print(my_kitchen < 14 or my_kitchen > 17)

# Double my_kitchen smaller than triple your_kitchen?
print(my_kitchen * 2 < your_kitchen * 3)
```

- Boolean operators with Numpy

> ```py
> np.logical_and(,)
> np.logical_or(,)
> np.logical_not(,)
>
> np.logical_and(my_house > 13,
>               your_house < 15)
> ```

### if, elif, else

```py
# 记得冒号！！
# if
area = 14.0
if area > 15 :
    print("big place!")

# Add else
if area > 15 :
    print("big place!")
else :
    print("pretty small." )

# Customize further: elif
if area > 15 :
    print("big place!")
elif area > 10 :
    print("medium size, nice!")
else :
    print("pretty small.")
```

### Filtering pandas DataFrames

```py
# Driving right
## Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

## Extract drives_right column as Series: dr
dr = cars['drives_right'] # panda series of boolen
> US      True
> AUS    False
> JPN    False
> IN     False
> RU      True
> MOR     True
> EG      True
> Name: drives_right, dtype: bool

## Use dr to subset cars: sel
sel = cars[dr] # drives_right=True的国家的各项信息

## or in one line
sel = cars[cars['drives_right']]

# Cars per capita
## Create car_maniac: observations that have a cars_per_cap over 500
cpc=cars['cars_per_cap']
many_cars=cpc>500  # panda series of boolen
car_maniac = cars[many_cars]

## Create medium: observations with cars_per_cap between 100 and 500
cpc = cars['cars_per_cap']
between = np.logical_and(cpc > 100, cpc < 500)
medium=cars[between]
```

## Loops

### While Loop

> ```py
> while condition :
>    expression
> ```

```py
# Initialize offset
offset = 8

# Code the while loop
while offset != 0 :
    print("correcting...")
    offset = offset - 1
    print(offset)

# Add conditionals
## Initialize offset
offset = -6

## Code the while loop
while offset != 0 :
    print("correcting...")
    if offset > 0 :
      offset = offset - 1
    else :
      offset = offset + 1
    print(offset)

```

### For Loop

- Loop over a list
  
```py
areas = [11.25, 18.0, 20.0, 10.75, 9.50]
for area in areas:
    print(area)
# areas list
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

# Change for loop to use enumerate() and update print()
for index,a in enumerate(areas) :
    print('room' + str(index) + ':' + str(a))

# Change for loop to use enumerate() and update print()
## 需要索引的时候用
for index,a in enumerate(areas) :
    print('room' + str(index) + ':' + str(a))
```

- Loop over list of lists

```py
# house list of lists
house = [["hallway", 11.25],
         ["kitchen", 18.0],
         ["living room", 20.0],
         ["bedroom", 10.75],
         ["bathroom", 9.50]]

# Build a for loop from scratch
## 注意空格！！
for [x,y] in house:
    print('the ' + x + ' is ' + str(y) +' sqm')
```

### Loop Data Structures

- Loop over dictionary

```py
# Use method items()
# Definition of dictionary
europe = {'spain':'madrid', 'france':'paris', 'germany':'berlin',
          'norway':'oslo', 'italy':'rome', 'poland':'warsaw', 'austria':'vienna' }

# Iterate over europe
for x, y in europe.items() :
    print("the capital of " + x + " is " + y)
```

- Loop over Numpy array
  
> ```py
> # 1D Numpy array
> for x in my_array :
>   ...
>
> # 2D Numpy array
> ## 用np.nditer()这个方程才是elementwise循环，不然是array-wise
> for x in np.nditer(my_array) :
>   ...
>```

- Loop over DataFrame
  
> ```py
> # every observation is iterated over and on every iteration the row label and actual row contents are available:
> for lab, row in brics.iterrows() :
>     ...
> ```

```py
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Iterate over rows of cars
for label,row in cars.iterrows() :
    print(label)
    print(row)

# select variables from the Pandas Series using square brackets
for lab, row in cars.iterrows() :
    print(lab + ': ' + str(row['cars_per_cap']))
> US: 809
> AUS: 731
> JPN: 588
> IN: 18
> RU: 200
> MOR: 70
> EG: 45
```

- Add column

```py
# Code for loop that adds COUNTRY column that contains a uppercase version of the country names in the "country" column.
for lab, row in cars.iterrows() :
    cars.loc[lab, "COUNTRY"] = row['country'].upper()

# .apply(str.upper) give the same result
cars["COUNTRY"] = cars["country"].apply(str.upper)
```

## Case Study: Hacker Statistics

### Random Numbers

> ```py
> seed() # sets the random seed, so that your results are reproducible between simulations. As an argument, it takes an integer of your choosing. If you call the function, no output will be generated.
> rand() # if you don't specify any arguments, it generates a random float between zero and one.
> ```

- Random float
  
```py
# Import numpy as np
import numpy as np

# Set the seed
np.random.seed(123)

# Generate and print random float
print(np.random.rand())

# Starting step
step = 50

# Roll the dice
dice = np.random.randint(1,7)

# Finish the control construct
if dice <= 2 :
    step = step - 1
elif dice <= 5 :
    step = step + 1
else :
    step = step + np.random.randint(1,7)

# Print out dice and step
print(dice)
> 3
print(step)
> 51
```

### Random Walk

```py
# Initialize random_walk
random_walk = [0]

# Finish the for loop
for x in range(100) :
    # Set step: last element in random_walk
    # 基于上一步确定走到哪里
    step = random_walk[-1]

    # Roll the dice
    dice = np.random.randint(1,7)

    # Determine next step
    if dice <= 2:
         # Replace below: use max to make sure step can't go below 0
        step = max(0, step - 1)
    elif dice <= 5:
        step = step + 1
    else:
        step = step + np.random.randint(1,7)

    # append next_step to random_walk
    random_walk.append(step)

# Print random_walk
print(random_walk)
```

- Visualize the walk

```py
# Import matplotlib.pyplot as plt
import matplotlib.pyplot as plt

# Plot random_walk
plt.plot(random_walk)

# Show the plot
plt.show()
```

### Distribution

- Simulate multiple walks

```py
# Initialize all_walks (don't change this line)
all_walks = []

# Simulate random walk 10 times
for i in range(10) :

    # Code from before
    random_walk = [0]
    for x in range(100) :
        step = random_walk[-1]
        dice = np.random.randint(1,7)

        if dice <= 2:
            step = max(0, step - 1)
        elif dice <= 5:
            step = step + 1
        else:
            step = step + np.random.randint(1,7)
         # Implement clumsiness.You're a bit clumsy and you have a 0.1% chance of falling down
        if np.random.rand() <= 0.001 :
            step = 0
        random_walk.append(step)

    # Append random_walk to all_walks
    all_walks.append(random_walk)

# Print all_walks
print(all_walks)
```

- Visualize all walks

```py
# Convert all_walks to Numpy array: np_aw
np_aw = np.array(all_walks)

# Plot np_aw and show
plt.plot(np_aw)
plt.show()

# Clear the figure
plt.clf()

# Transpose np_aw: np_aw_t
np_aw_t=np.transpose(np_aw)

# Plot np_aw_t and show
plt.plot(np_aw_t)
plt.show()
```

- Plot the distribution

```py
# Select last row from np_aw_t: ends
ends = np_aw_t[-1,:]

# Plot histogram of ends, display plot
plt.hist(ends)
plt.show()
```

- Calculate the odds

```py
#  To calculate the chance that this end point is greater than or equal to 60
np.mean(ends > 30) # gives you the fraction of simulations that ended higher than step 30.
> 0.784
```
