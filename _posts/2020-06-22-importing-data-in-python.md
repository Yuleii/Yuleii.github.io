---
layout: article
title: Importing Data in Python
key: 20200622
tags: Programming
modify_date: 2020-06-24
pageview: false
aside:
  toc: true
---


Base on DataCamp.

<!--more-->

## Introduction and flat files

### Importing Text Files

#### Exploring your working directory

`! ls` will display the contents of your current directory.

#### Importing entire text files

`open()`

```py
# Open a file: file
file = open('moby_dick.txt', mode='r') # r for  read-only

# Print it
print(file.read())

# Check whether file is closed
print(file.closed)
> False

# Close file
file.close()

# Check whether file is closed
print(file.closed)
> True
```

#### Importing text files line by line

context manager: `with open() as `

```py
# Open moby_dick.txt using the with context manager 
with open('moby_dick.txt') as file:
    # Print the first three lines of the file
    print(file.readline())
    print(file.readline())
    print(file.readline())
```

### Importing Flat Files

`np.loadtxt()`

#### Using NumPy to import flat files

```py
# Import package
import numpy as np

# Assign filename to variable: file
file = 'digits.csv'

# Load file as array: digits
digits = np.loadtxt(file, delimiter=',')

# Print datatype of digits
print(type(digits))
> <class 'numpy.ndarray'>
```

#### Customizing your NumPy import

```py
# Import numpy
import numpy as np

# Assign the filename: file
file = 'digits_header.txt'

# Load the data: data
data = np.loadtxt(file, delimiter='\t', skiprows=1,usecols=[0, 2]) # Delimiter is tab-delimited. Skip the first row and you only want to import the first and third columns.

# Print data
print(data)
```

#### Importing different datatypes

```py
# Assign filename: file
file = 'seaslug.txt' # has a text header, consisting of strings, tab-delimited.

# Due to the header, if you tried to import it as-is using np.loadtxt(), Python would throw you a ValueError and tell you that it could not convert string to float. There are two ways to deal with this: firstly, you can set the data type argument dtype equal to str (for string).
data = np.loadtxt(file, delimiter='\t', dtype=str)

# Print the first element of data
print(data[0])

# Alternatively, import data as floats and skip the first row: data_float
data_float = np.loadtxt(file, delimiter='\t', dtype=float, skiprows=1)

# Print the 10th element of data_float
print(data_float[9])
```

### Working with mixed datatypes

Much of the time you will need to import datasets which have different datatypes in different columns; one column may contain strings and another floats, for example. The function `np.loadtxt()` will freak at this. There is another function, `np.genfromtxt()`, which can handle such structures. If we pass `dtype=None` to it, it will figure out what types each column should be.

##### np.genfromtxt()

```py
# Import 'titanic.csv' using the function np.genfromtxt()
data = np.genfromtxt('titanic.csv', delimiter=',', names=True, dtype=None) # the first argument is the filename, the second specifies the delimiter , and the third argument names tells us there is a header

# data is an object called a structured array. Because numpy arrays have to contain elements that are all the same type, the structured array solves this by being a 1D array, where each element of the array is a row of the flat file imported. 
np.shape(data)
> (891,)
```

##### np.recfromcsv()

There is also another function `np.recfromcsv()` that behaves similarly to `np.genfromtxt()`, except that its default dtype is `None`.

```py
# Assign the filename: file
file = 'titanic.csv'

# Import file using np.recfromcsv: d
d = np.recfromcsv(file, delimiter=',', names=True, dtype=None)

# Print out first three entries of d
print(d[:3])
```

### Importing flat files using pandas

`pd.read_csv`

```py
# Assign the filename: file
file = 'digits.csv'

# Read the first 5 rows of the file into a DataFrame: data
data = pd.read_csv(file, nrows=5, header = None) # there is no header in this file

# Build a numpy array from the DataFrame: data_array
data_array = data.values

# Print the datatype of data_array to the shell
print(type(data_array))
> <class 'numpy.ndarray'>
```

#### Customizing your pandas import

```py
# Import matplotlib.pyplot as plt
import matplotlib.pyplot as plt

# Assign filename: file
file = 'titanic_corrupt.txt' # contains comments after the character '#', tab-delimited.

# Import file: data
data = pd.read_csv(file, sep='\t', comment='#', na_values= 'Nothing') # comment takes characters that comments occur after in the file, which in this case is '#'. na_values takes a list of strings to recognize as NA/NaN, in this case the string 'Nothing'

# Print the head of the DataFrame
print(data.head())
```

## Introduction to other file types

