---
layout: article
title: Importing Data in Python
key: 20200622
tags: Python DataAnalysis
modify_date: 2020-06-26
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

## Working with relational databases in Python

### Creating a database engine in Python

```py
# Import the function create_engine from the module sqlalchemy
from sqlalchemy import create_engine

# Create an engine to connect to the SQLite database 'Chinook.sqlite' and assign it to engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Using the method table_names() on the engine engine, assign the table names of 'Chinook.sqlite' to the variable table_names.
table_names = engine.table_names()

# Print the table names to the shell
print(table_names)
> ['Album', 'Artist', 'Customer', 'Employee', 'Genre', 'Invoice', 'InvoiceLine', 'MediaType', 'Playlist', 'PlaylistTrack', 'Track']
```

### Querying relational databases in Python

#### The Hello World of SQL Queries!

```py
# Import packages
from sqlalchemy import create_engine
import pandas as pd

# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Open the engine connection as con using the method connect() on the engine.
con = engine.connect()

# Execute the query that selects ALL columns from the Album table. Store the results in rs.
rs = con.execute('select * from Album')

# Store all of your query results in the DataFrame df by applying the fetchall() method to the results rs.
df = pd.DataFrame(rs.fetchall())

# Close connection
con.close()

# Print head of DataFrame df
print(df.head())


# Customizing the Hello World of SQL Queries
# Perform query and save results to DataFrame: df
with engine.connect() as con:
    # Execute the SQL query that selects the columns LastName and Title from the Employee table. Store the results in the variable rs.
    rs = con.execute("SELECT LastName, Title FROM Employee")
    # Apply the method fetchmany() to rs in order to retrieve 3 of the records. Store them in the DataFrame df. 
    df = pd.DataFrame(rs.fetchmany(size=3))
    # Using the rs object, set the DataFrame's column names to the corresponding names of the table columns.
    df.columns = rs.keys()

# Print the length of the DataFrame df
print(len(df))
> 3

# Print the head of the DataFrame df
print(df.head())
```

Filtering your database records using SQL's WHERE

```py
with engine.connect() as con:
    rs = con.execute("SELECT * FROM Employee WHERE EmployeeId >=6")
    df = pd.DataFrame(rs.fetchall())
    df.columns = rs.keys()
```

Ordering your SQL records with ORDER BY

```py
# Open engine in context manager
with engine.connect() as con:
    rs = con.execute("SELECT * FROM Employee ORDER BY BirthDate")
    df = pd.DataFrame(rs.fetchall())
    df.columns = rs.keys()
```

### Querying relational databases directly with pandas

#### Pandas and The Hello World of SQL Queries!

```py
# Import packages
from sqlalchemy import create_engine
import pandas as pd

# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Execute query and store records in DataFrame: df
df = pd.read_sql_query("SELECT * FROM Album", engine)

# Print head of DataFrame
print(df.head())

# Open engine in context manager and store query result in df1
with engine.connect() as con:
    rs = con.execute("SELECT * FROM Album")
    df1 = pd.DataFrame(rs.fetchall())
    df1.columns = rs.keys()

# Confirm that both methods yield the same result
print(df.equals(df1))
> True
```

#### Pandas for more complex querying

```py
# Import packages
from sqlalchemy import create_engine
import pandas as pd

# Create engine: engine
engine = create_engine('sqlite:///Chinook.sqlite')

# Execute query and store records in DataFrame: df
df = pd.read_sql_query("SELECT * FROM Employee WHERE EmployeeId >= 6 ORDER BY BirthDate", engine)

# Print head of DataFrame
print(df.head())
```

### Advanced querying: exploiting table relationships

#### INNER JOIN

```py
# Open engine in context manager
# Perform query and save results to DataFrame: df
with engine.connect() as con:
    # Assign to rs the results from the following query: select all the records, extracting the Title of the record and Name of the artist of each record from the Album table and the Artist table, respectively. To do so, INNER JOIN these two tables on the ArtistID column of both.
    rs = con.execute("SELECT Title,Name FROM Album INNER JOIN Artist on Album.ArtistID = Artist.ArtistID")
    df = pd.DataFrame(rs.fetchall())
    df.columns = rs.keys()

# Filtering your INNER JOIN
# Execute query and store records in DataFrame: df
df = pd.read_sql_query("SELECT * FROM PlaylistTrack INNER JOIN Track on PlaylistTrack.TrackId = Track.TrackId WHERE Milliseconds < 250000", engine)
```

## Importing data from the Internet

### Importing files from the web

#### Importing flat files

```py
# Import the function urlretrieve from the subpackage urllib.request
from urllib.request import urlretrieve

# Import pandas
import pandas as pd

# Assign url of file: url
url = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_1606/datasets/winequality-red.csv'

# Opening and reading flat files from the web
df = pd.read_csv(url, sep = ';')

# Use the function urlretrieve() to save the file locally as 'winequality-red.csv'
urlretrieve(url, 'winequality-red.csv')

# Read file into a DataFrame and print its head
df = pd.read_csv('winequality-red.csv', sep=';')
print(df.head())
```

#### Importing non-flat files

```py
# Import package
import pandas as pd

# Assign url of file: url
url = 'http://s3.amazonaws.com/assets.datacamp.com/course/importing_data_into_r/latitude.xls'

# Read in all sheets of Excel file: xls
xls = pd.read_excel(url, sheet_name=None) #  in order to import all sheets you need to pass None to the argument sheet_name

# Print the names of the sheets in the Excel spreadsheet; these will be the keys of the dictionary xls.
print(xls.keys())

# Print the head of the first sheet (using its name, NOT its index),The sheet name is '1700'.
print(xls['1700'].head())
```

### HTTP requests to import files from the web

```py
# Import the functions urlopen and Request from the subpackage urllib.request.
from urllib.request import urlopen, Request

# Specify the url
url = "http://www.datacamp.com/teach/documentation"

# This packages the request: request
request = Request(url)

# Sends the request and catches the response: response
response = urlopen(request)

# Print the datatype of response
print(type(response))
> <class 'http.client.HTTPResponse'>

# Extract the response: html
html = response.read()

# Print the html request results
print(html)

# Be polite and close the response!
response.close()
```

Performing HTTP requests in Python using  package `requests`

```py
# Import the package requests.
import requests

# Specify the url: url
url = "http://www.datacamp.com/teach/documentation"

# Packages the request, send the request and catch the response: r
r = requests.get(url)

# Extract the response: text. Return the HTML of the webpage as a string; 
text = r.text

# Print the html
print(text)
```

### Scraping the web in Python

#### Parsing HTML with BeautifulSoup

```py
# Import the function BeautifulSoup from the package bs4.
import requests
from bs4 import BeautifulSoup

# Specify url: url
url = 'https://www.python.org/~guido/'

# Package the request, send the request and catch the response: r
r = requests.get(url)

# Extracts the response as html: html_doc
html_doc = r.text

# Create a BeautifulSoup object from the HTML: soup
soup = BeautifulSoup(html_doc)

# Prettify the BeautifulSoup object: pretty_soup
pretty_soup = soup.prettify()

# Print the response
print(pretty_soup)


# Getting the text
# Get the title of Guido's webpage: guido_title
guido_title = soup.title

# Print the title of Guido's webpage to the shell
print(guido_title)

# Get Guido's text: guido_text
guido_text = soup.get_text()

# Print Guido's text to the shell
print(guido_text)


# getting the hyperlinks
# Find all 'a' tags (which define hyperlinks): a_tags
a_tags = soup.find_all('a') # hyperlinks are defined by the HTML tag <a> but passed to find_all() without angle brackets;

# Print the URLs to the shell
# The variable a_tags is a results set: your job now is to enumerate over it, using a for loop and to print the actual URLs of the hyperlinks; to do this, for every element link in a_tags, you want to print() link.get('href').
for link in a_tags:
    print(link.get('href'))
```


## Interacting with APIs to import data from the web

### Loading and exploring a JSON

```py
# use the function json.load() within the context manager.
with open("a_movie.json") as json_file:
    json_data = json.load(json_file)

# Use a for loop to print all key-value pairs in the dictionary json_data
for k in json_data.keys():
    print(k + ': ', json_data[k])


import json
with open("a_movie.json") as json_file:
    json_data = json.load(json_file)
json_data['Title']
> 'The Social Network'
json_data['Year']
> '2010'
```

### APIs and interacting with the world wide web

#### API requests

```py
# Import requests package
import requests

# Assign to the variable url the URL of interest in order to query 'http://www.omdbapi.com' for the data corresponding to the movie The Social Network. The query string should have two arguments: apikey=72bc447a and t=the+social+network. You can combine them as follows: apikey=72bc447a&t=the+social+network
url = 'http://www.omdbapi.com/?apikey=72bc447a&t=the+social+network'

# Package the request, send the request and catch the response: r
r = requests.get(url)

# Print the text of the response
print(r.text)


# JSON–from the web to Python
# Apply the json() method to the response object r and store the resulting dictionary in the variable json_data.
json_data = r.json()

# Print each key-value pair in json_data
for k in json_data.keys():
    print(k + ': ', json_data[k])
```

#### Checking out the Wikipedia API

```py
# Import package
import requests

# Assign URL to variable: url
url = 'https://en.wikipedia.org/w/api.php?action=query&prop=extracts&format=json&exintro=&titles=pizza'


# Package the request, send the request and catch the response: r
r = requests.get(url)

# Decode the JSON data into a dictionary: json_data
json_data = r.json()

# Print the Wikipedia page extract
pizza_extract = json_data['query']['pages']['24768']['extract']
print(pizza_extract)
```

## Diving deep into the Twitter API

### API Authentication

The package `tweepy` is great at handling all the Twitter API OAuth Authentication details for you. All you need to do is pass it your authentication credentials. 

```py
# Import the package tweepy
import tweepy

# Store OAuth authentication credentials in relevant variables
access_token = "1092294848-aHN7DcRP9B4VMTQIhwqOYiB14YkW92fFO8k8EPy"
access_token_secret = "X4dHmhPfaksHcQ7SCbmZa2oYBBVSD2g8uIHXsp5CTaksx"
consumer_key = "nZ6EA0FxZ293SxGNg8g8aP0HM"
consumer_secret = "fJGEodwe3KiKUnsYJC3VRndj7jevVvXbK2D5EiJ2nehafRgA6i"

# Pass OAuth details to tweepy's OAuth handler. Pass the parameters consumer_key and consumer_secret to the function tweepy.OAuthHandler().
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
# Complete the passing of OAuth credentials to the OAuth handler auth by applying to it the method set_access_token(), along with arguments access_token and access_token_secret.
auth.set_access_token(access_token, access_token_secret)
```

### Defined the tweet stream listener class

```py
class MyStreamListener(tweepy.StreamListener):
    def __init__(self, api=None):
        super(MyStreamListener, self).__init__()
        self.num_tweets = 0
        self.file = open("tweets.txt", "w")

    def on_status(self, status):
        tweet = status._json
        self.file.write( json.dumps(tweet) + '\n' )
        self.num_tweets += 1
        if self.num_tweets < 100:
            return True
        else:
            return False
        self.file.close()

    def on_error(self, status):
        print(status)
```

### Streaming tweets

```py
# Initialize Stream listener
l = MyStreamListener()

# Create your Stream object with authentication
stream = tweepy.Stream(auth, l)

# Filter Twitter Streams to capture data by the keywords:
stream.filter(['clinton','trump','sanders','cruz'])
```

### Load and explore your Twitter data

```py
# Import package
import json

# String of path to file: tweets_data_path
tweets_data_path = 'tweets.txt'

# Initialize empty list to store tweets: tweets_data
tweets_data = []

# Open connection to file
tweets_file = open(tweets_data_path, "r")

# Read in tweets and store in list: tweets_data
for line in tweets_file:
    tweet = json.loads(line) #  load each tweet into a variable, tweet, using json.loads()
    tweets_data.append(tweet) # ppend tweet to tweets_data

# Close connection to file
tweets_file.close()

# Print the keys of the first tweet dict
print(tweets_data[0].keys())
```

### Twitter data to DataFrame

```py
# Import package
import pandas as pd

# Build DataFrame of tweet texts and languages. Use pd.DataFrame() to construct a DataFrame of tweet texts and languages; to do so, the first argument should be tweets_data, a list of dictionaries. The second argument to pd.DataFrame() is a list of the keys you wish to have as columns
df = pd.DataFrame(tweets_data, columns=['text','lang'])

# Print head of DataFrame
print(df.head())
```

### A little bit of Twitter text analysis

Defined the following function `word_in_text()`, which will tell you whether the first argument (a word) occurs within the 2nd argument (a tweet).
```py
import re

def word_in_text(word, text):
    word = word.lower()
    text = text.lower()
    match = re.search(word, text)

    if match:
        return True
    return False
```

Iterate over the rows of the DataFrame and calculate how many tweets contain each of our keywords. The list of objects for each candidate has been initialized to 0.

```py
# Initialize list to store tweet counts
[clinton, trump, sanders, cruz] = [0, 0, 0, 0]

# Iterate through df, counting the number of tweets in which
# each candidate is mentioned
for index, row in df.iterrows():
    clinton += word_in_text('clinton', row['text']) #  increases the value of clinton by 1 each time a tweet (text row) mentioning 'Clinton' is encountered; 
    trump += word_in_text('trump', row['text'])
    sanders += word_in_text('sanders', row['text'])
    cruz += word_in_text('cruz', row['text'])
```

### Plotting your Twitter data

```py
# Import packages
import matplotlib.pyplot as plt
import seaborn as sns

# Set seaborn style
sns.set(color_codes=True)

# Create a list of labels:cd
cd = ['clinton', 'trump', 'sanders', 'cruz']

# Plot the bar chart
ax = sns.barplot(cd, [clinton, trump, sanders, cruz]) # The first argument should be the list of labels to appear on the x-axis (created in the previous step). The second argument should be a list of the variables you wish to plot(i.e. a list containing clinton, trump, etc).
ax.set(ylabel="count")
plt.show()
```