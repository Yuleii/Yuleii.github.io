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

### Text Files

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

### Flat Files

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

Customizing your pandas import:

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

- Excel spreadsheets MATLAB files
- SAS files
- Stata files
- HDF5 files
- Pickled files


### os libary

```py
# imports the library os
import os 

#  stores the name of the current directory in a string called wd
wd = os.getcwd()

#  outputs the contents of the directory in a list to the shell
os.listdir(wd)
> ['titanic.txt', 'battledeath.xlsx']
```

### Loading a pickled file

```py
# Import pickle package
import pickle 

# Open pickle file and load data: d
with open('data.pkl', 'rb') as file: #  rb: it is read only for a binary file
    d = pickle.load(file)

# Print d
print(d)
> {'June': '69.4', 'Aug': '85', 'Airline': '8', 'Mar': '84.4'}

# Print datatype of d
print(type(d))
> <class 'dict'>
```

### Excel files

#### Listing sheets in Excel files

```py
# Import pandas
import pandas as pd

# Assign spreadsheet filename: file
file = 'battledeath.xlsx'

# Load spreadsheet: xls
xls = pd.ExcelFile(file)

# Print sheet names
print(xls.sheet_names)
> ['2002', '2004']
```

#### Importing sheets from Excel files

```py
# Load the sheet '2004' into the DataFrame df1 using its name as a string.
df1 = xls.parse('2004')

# Print the head of the DataFrame df1
print(df1.head())

# Load the sheet 2002 into the DataFrame df2 using its index (0).
df2 = xls.parse(0)

# Print the head of the DataFrame df2
print(df2.head())
```

#### Customizing your spreadsheet import

```py
# Parse the first sheet by index. In doing so, skip the first row of data and name the columns 'Country' and 'AAM due to War (2002)' using the argument names. The values passed to skiprows and names all need to be of type list.
df1 = xls.parse(0, skiprows=1, names=['Country','AAM due to War (2002)'])

# Print the head of the DataFrame df1
print(df1.head())

# Parse the second sheet by index. In doing so, parse only the first column with the usecols parameter, skip the first row and rename the column 'Country'. The argument passed to usecols also needs to be of type list.
df2 = xls.parse(1, usecols=[0], skiprows=1, names=['Country'])

# Print the head of the DataFrame df2
print(df2.head())
```

### Importing SAS files using pandas


```py
# Import the module SAS7BDAT from the library sas7bdat.
from sas7bdat import SAS7BDAT

# In the context of the file 'sales.sas7bdat', load its contents to a DataFrame df_sas, using the method to_data_frame() on the object file.
with SAS7BDAT('sales.sas7bdat') as file:
    df_sas = file.to_data_frame()

# Print head of DataFrame
print(df_sas.head())
```

### Importing Stata files using pandas

```py
# Import pandas
import pandas as pd

# Load Stata file into a pandas DataFrame: df
df = pd.read_stata('disarea.dta')

# Print the head of the DataFrame df
print(df.head())
```

### HDF5 files

#### Importing HDF5 files

```py
# Import packages
import numpy as np
import h5py

# Assign filename: file
file = 'LIGO_data.hdf5'

# Load file: data
data = h5py.File(file, 'r')

# Print the datatype of the loaded file
print(type(data))

# Print the keys of the file
for key in data.keys():
    print(key)
```

#### Extracting data from your HDF5 file

```py
# Assign the HDF5 group data['strain'] to group
group = data['strain']

# Check out keys of group
for key in group.keys():
    print(key)

# Assign to the variable strain the values of the time series data data['strain']['Strain'] using the attribute .value
strain = data['strain']['Strain'].value

# et num_samples equal to 10000, the number of time points we wish to sample.
num_samples = 10000

# Set time vector
time = np.arange(0, 1, 1/num_samples)

# Plot data
plt.plot(time, strain[:num_samples])
plt.xlabel('GPS Time (s)')
plt.ylabel('strain')
plt.show()
```

### MATLAB files

#### Loading .mat files

```py
# Import the package scipy.io.
import scipy.io

# Load MATLAB file: mat
mat = scipy.io.loadmat('albeck_gene_expression.mat')

# Print the datatype type of mat
print(type(mat))
> <class 'dict'>
```

#### The structure of .mat in Python

```py
# Use the method .keys() on the dictionary mat to print the keys. Most of these keys (in fact the ones that do NOT begin and end with '__') are variables from the corresponding MATLAB environment.
print(mat.keys())
> > dict_keys(['__header__', '__version__', '__globals__', 'rfpCyt', 'rfpNuc', 'cfpNuc', 'cfpCyt', 'yfpNuc', 'yfpCyt', 'CYratioCyt'])

# Print the type of the value corresponding to the key 'CYratioCyt' in mat. Recall that mat['CYratioCyt'] accesses the value.
print(type(mat['CYratioCyt']))
> <class 'numpy.ndarray'>

# Print the shape of the value corresponding to the key 'CYratioCyt'
print(np.shape(mat['CYratioCyt']))
> (200, 137)
```