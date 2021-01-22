---
layout: article
title: Python Data Science Toolbox
key: 20200614
tags: Python DataScience
modify_date: 2020-06-18
pageview: false
aside:
  toc: true
---


Base on DataCamp.

<!--more-->


## Write function

### Functions that Return Single Values
```py
# Define shout with the parameter, word
def shout(word):
    """Return a string with three exclamation marks"""
    # Concatenate the strings: shout_word
    shout_word = word + '!!!'

    # Replace print with return
    return(shout_word)
    # 如果不用return，而是直接在方程里print返回结果会是NoneType

# Pass 'congratulations' to shout: yell
yell = shout('congratulations')

# Print yell
print(yell)
> congratulations!!!
```

### Multiple Parameters and Return Values

```py
# A brief introduction to tuples(immutable!!)
nums = (3, 4, 6)
## Unpack nums into num1, num2, and num3
num1, num2, num3 = nums

## Construct even_nums
even_nums=(2,4,6)

# Define shout_all with parameters word1 and word2
def shout_all(word1, word2):
    
    # Concatenate word1 with '!!!': shout1
    shout1 = word1 + '!!!'
    
    # Concatenate word2 with '!!!': shout2
    shout2 = word2 + '!!!'
    
    # Construct a tuple with shout1 and shout2: shout_words
    shout_words = (shout1,shout2)

    # Return shout_words
    return shout_words

# Pass 'congratulations' and 'you' to shout_all(): yell1, yell2
yell1,yell2=shout_all('congratulations','you')

# Print yell1 and yell2
print(yell1)
print(yell2)
> congratulations!!!
> you!!!
```

### Twitter Dataframe Analysis

[Tweets dataset](https://assets.datacamp.com/production/repositories/463/datasets/82e9842c09ad135584521e293091c2327251121d/tweets.csv)

The dataset contains Twitter data and you will iterate over entries in a column to build a dictionary in which the keys are the names of languages and the values are the number of tweets in the given language.

```py
# Import pandas

import pandas as pd

# Import Twitter data as DataFrame: df
df = pd.read_csv('tweets.csv')

# Define count_entries()
def count_entries(df, col_name):
    """Return a dictionary with counts of 
    occurrences as value for each key."""

    # Initialize an empty dictionary: langs_count
    langs_count = {}
    
    # Extract column from DataFrame: col
    col = df[col_name]
    
    # Iterate over lang column in DataFrame
    for entry in col:

        # If the language is in langs_count, add 1
        if entry in langs_count.keys():
            langs_count[entry]+=1
        # Else add the language to langs_count, set the value to 1
        else:
            langs_count[entry]=1

    # Return the langs_count dictionary
    return(langs_count)

# Call count_entries(): result
result = count_entries(tweets_df,'lang')

# Print the result
print(result)
> {'en': 97, 'et': 1, 'und': 2}
```

## Scope

- LEGB rule,L for local, E for enclosing functions,G for global and B for built-in.

```py
# Assigning name only create or change local names
num = 5
def func1():
    num = 3
    print(num)
func1()    
> 3
print(num)
> 5 

def func2():
    global num
    double_num = num * 2
    num = 6
    print(double_num)
func2()
> 10
print(num)
> 6
```

```py
# Create a string: team
team = "teen titans"

# Define change_team()
def change_team():
    """Change the value of the global variable team."""

    # Use team in global scope
    global team

    # Change the value of team in global: team
    team = "justice league"
    
# Print team
print(team)
> teen titans

# Call change_team()
change_team()

# Print team
print(team)
> justice league
```

## Nested functions

```py
# Define three_shouts
def three_shouts(word1, word2, word3):
    """Returns a tuple of strings
    concatenated with '!!!'."""

    # Define inner
    def inner(word):
        """Returns a string concatenated with '!!!'."""
        return word + '!!!'

    # Return a tuple of strings!!
    return (inner(word1), inner(word2), inner(word3))

# Call three_shouts() and print
print(three_shouts('a', 'b', 'c'))
> ('a!!!', 'b!!!', 'c!!!')
```

```py
# Define echo
def echo(n):
    """Return the inner_echo function."""

    # Define inner_echo
    def inner_echo(word1):
        """Concatenate n copies of word1."""
        echo_word = word1 * n
        return echo_word

    # Return inner_echo
    return inner_echo

# Call echo: twice
twice = echo(2)

# Call echo: thrice
thrice = echo(3)

# Call twice() and thrice() then print
print(twice('hello'), thrice('hello'))
> hellohello hellohellohello
```

```py
# Define echo_shout()
def echo_shout(word):
    """Change the value of a nonlocal variable"""
    
    # Concatenate word with itself: echo_word
    echo_word = word*2
    
    # Print echo_word
    print(echo_word)
    
    # Define inner function shout()
    def shout():
        """Alter a variable in the enclosing scope"""    
        # Use echo_word in nonlocal scope
        nonlocal echo_word
        
        # Change echo_word to echo_word concatenated with '!!!'
        echo_word = echo_word+ '!!!'
    
    # Call function shout()
    shout()
    
    # Print echo_word
    print(echo_word)

# Call function echo_shout() with argument 'hello'
echo_shout('hello')
>> hellohello
   hellohello!!!
```

## Default and Flexible Arguments

### Add a default argument

```py
# Define shout_echo
def power(number, pow=1):
    """Raise number to the power of pow."""
    new_value = number ** pow
    return new_value

power(9, 2)
> 81
power(9, 1)
> 9
power(9)
> 0
```

### Functions with variable-length arguments (*args)

```py
# args is a tuple!!
# 表示函数接收可变长度的非关键字参数列表作为函数的输入
def add_all(*args):
    """Sum all values in *args together."""
    # Initialize sum
    sum_all = 0
    # Accumulate the sum
    for num in args:
    sum_all += num
    return sum_all

add_all(1)
> 1
add_all(1, 2)
> 3 
add_all(5, 10, 15, 20)
> 50
```

### Functions with variable-length keyword arguments (**kwargs)

```py
# kwargs is a dictionary!!
# 表示函数接收可变长度的关键字参数字典作为函数的输入
def print_all(**kwargs):
    """Print out key-value pairs in **kwargs."""
    # Print out the key-value pairs
    for key, value in kwargs.items():
    print(key + \": \" + value)

print_all(name="dumbledore", 
job="headmaster")
> job: headmaster
  name: dumbledore
```

## Lambda Functions

- Map() and lambda functions

```py
# Function map takes two arguments: map(func, seq)
# map() applies the function to ALL elements in the sequence
nums = [48, 6, 9, 21, 1]
square_all = map(lambda num: num ** 2, nums)
print(square_all)
> <map object at 0x103e065c0>
print(list(square_all))
> [2304, 36, 81, 441, 1]
```

- Filter() and lambda functions

```py
# filter() offers a way to filter out elements from a list that don't satisfy certain criteria.
# Create a list of strings: fellowship
fellowship = ['frodo', 'samwise', 'merry', 'pippin', 'aragorn', 'boromir', 'legolas', 'gimli', 'gandalf']

# Use filter() to apply a lambda function over fellowship: result
result = filter(lambda member:len(member)>6 , fellowship)

# Convert result to a list: result_list
result_list=list(result)

# Print result_list
print(result_list)
> ['samwise', 'aragorn', 'boromir', 'legolas', 'gandalf']
```

- Reduce() and lambda functions

```py
# Import reduce from functools
from functools import reduce

# Create a list of strings: stark
stark = ['robb', 'sansa', 'arya', 'brandon', 'rickon']

# Use reduce() to apply a lambda function over stark: result
result = reduce(lambda item1,item2: item1+item2, stark)

# Print the result
print(result)
> robbsansaaryabrandonrickon
```

## Error Handling

### try-except

```py
def sqrt(x):
    """Returns the square root of a number."""
    try:
        return x ** 0.5
    except:
        print('x must be an int or float')

sqrt(10.0)
> 3.1622776601683795
sqrt('hi')
> x must be an int or float
```

### raising an error

```py
def sqrt(x):
    """Returns the square root of a number."""
    if x < 0:
        raise ValueError('x must be non-negative')
    try:
        return x ** 0.5
    except TypeError:
        print('x must be an int or float')       
```

##  Iterators

### Iterators vs Iterables

An iterable is an object that can return an iterator, while an iterator is an object that keeps state and produces the next value when you call next()

- Iterable
    - Examples: lists, strings, dictionaries, le connections
    - An object with an associated iter() method
    - Applying iter() to an iterable creates an iterator

- Iterator
    - Produces next value with next()

```py
# Iterating over iterables: next()
word = 'Da'
it = iter(word)
next(it)
> 'D'
next(it)
> 'a'

# Iterating at once with *
word = 'Data'
it = iter(word)
print(*it)
> D a t a

# Iterating over dictionaries
pythonistas = {'hugo': 'bowne-anderson'
,
'francis': 'castro'}
for key, value in pythonistas.items():
print(key, value)
> francis castro
  hugo bowne-anderson

# Iterating over le connections
file = open('file.txt')
it = iter(file)
print(next(it))
> This is the first line.
print(next(it))
> This is the second line.
```

### enumerate()
enumerate() returns an enumerate object that produces a sequence of tuples, and each of the tuples is an index-value pair.

```py
# Using enumerate()
avengers = ['hawkeye', 'iron man', 'thor', 'quicksilver']
e = enumerate(avengers)
print(type(e))
> <class 'enumerate'>
e_list = list(e)
print(e_list)
> [(0, 'hawkeye'), (1, 'iron man'), (2, 'thor'), (3, 'quicksilver')]

# enumerate() and unpack
avengers = ['hawkeye', 'iron man', 'thor', 'quicksilver']
for index, value in enumerate(avengers):
print(index, value)
> 0 hawkeye
  1 iron man
  2 thor
  3 quicksilver

for index, value in enumerate(avengers, start=10):
print(index, value)
> 10 hawkeye
  11 iron man
  12 thor
  13 quicksilver
```

### zip()

```py
# Using zip()
avengers = ['hawkeye', 'iron man', 'thor', 'quicksilver']
names = ['barton', 'stark', 'odinson', 'maximoff']
z = zip(avengers, names)
print(type(z))
> <class 'zip'>
z_list = list(z)
print(z_list)
> [('hawkeye', 'barton'), ('iron man', 'stark'),
('thor', 'odinson'), ('quicksilver', 'maximoff')]

# zip() and unpack
avengers = ['hawkeye', 'iron man', 'thor', 'quicksilver']    
names = ['barton', 'stark',  'odinson', 'maximoff']
for z1, z2 in zip(avengers, names):
    print(z1, z2)
> hawkeye barton
  iron man stark
  thor odinson
  quicksilver maximoff

# Print zip with *
avengers = ['hawkeye', 'iron man', 'thor', 'quicksilver']
names = ['barton', 'stark', 'odinson', 'maximoff']
z = zip(avengers, names)
print(*z)
> ('hawkeye', 'barton') ('iron man', 'stark')('thor', 'odinson') ('quicksilver', 'maximoff')
```

### Extracting information for large amounts of Twitter data

```py
# Define count_entries()
def count_entries(csv_file,c_size,colname):
    """Return a dictionary with counts of
    occurrences as value for each key."""
    
    # Initialize an empty dictionary: counts_dict
    counts_dict = {}

    # Iterate over the file chunk by chunk
    for chunk in pd.read_csv(csv_file,chunksize=c_size):

        # Iterate over the column in DataFrame
        for entry in chunk[colname]:
            if entry in counts_dict.keys():
                counts_dict[entry] += 1
            else:
                counts_dict[entry] = 1

    # Return counts_dict
    return counts_dict

# Call count_entries(): result_counts
result_counts = count_entries('tweets.csv',10,'lang')

# Print result_counts
print(result_counts)
```

## List comprehensions

- Basic
> ```py
> [output expression for iterator variable in iterable]
> ```

- Advanced
> ```py
> [output expression + conditional on output for iterator variable in iterable + conditional on iterable]
>```

### Nested list comprehensions

```py
# Create list comprehension: squares
squares = [i**2 for i in range(10)]
print(squares)
> [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# Nested list comprehensions
[[output expression] for iterator variable in iterable]
# Create a 5 x 5 matrix using a list of lists: matrix
matrix = [[col for col in range(5)] for row in range(5)]

# Print the matrix
for row in matrix:
    print(row)
> [0, 1, 2, 3, 4]
  [0, 1, 2, 3, 4]
  [0, 1, 2, 3, 4]
  [0, 1, 2, 3, 4]
  [0, 1, 2, 3, 4]
```

### Using conditionals in comprehensions

```py
# Create a list of strings: fellowship
fellowship = ['frodo', 'samwise', 'merry', 'aragorn', 'legolas', 'boromir', 'gimli']

# Create list comprehension with if: 
new_fellowship = [member for member in fellowship if len(member) >= 7]

# Print the new list
print(new_fellowship)
> ['samwise', 'aragorn', 'legolas', 'boromir']

# Create list comprehension with if-else: 
new_fellowship = [member if len(member)>=7 else '' for member in fellowship]

# Print the new list
print(new_fellowship)
> ['', 'samwise', '', 'aragorn', 'legolas', 'boromir', '']
```

### Dict comprehensions

```py
# Create a list of strings: fellowship
fellowship = ['frodo', 'samwise', 'merry', 'aragorn', 'legolas', 'boromir', 'gimli']

# Create dict comprehension: new_fellowship
new_fellowship = {member:len(member) for member in fellowship}

# Print the new dictionary
print(new_fellowship)
> {'frodo': 5, 'samwise': 7, 'merry': 5, 'aragorn': 7, 'legolas': 7, 'boromir': 7, 'gimli': 5}
```

## generator expressions

[Efficient Pandas: Using Chunksize for Large Data Sets](https://medium.com/towards-artificial-intelligence/efficient-pandas-using-chunksize-for-large-data-sets-c66bf3037f93)

```py
# Create generator object: result
result = (num for num in range(31))

# Print the first 5 values
print(next(result))
print(next(result))
print(next(result))
print(next(result))
print(next(result))

# Print the rest of the values
for value in result:
    print(value)
```

- Changing the output in generator expressions

```py
# Create a list of strings: lannister
lannister = ['cersei', 'jaime', 'tywin', 'tyrion', 'joffrey']

# Create a generator object: lengths
lengths = (len(person) for person in lannister)

# Iterate over and print the values in lengths
for value in lengths:
    print(value)
```

- Build a generator

```py
# Create a list of strings
lannister = ['cersei', 'jaime', 'tywin', 'tyrion', 'joffrey']

# Define generator function get_lengths
def get_lengths(input_list):
    """Generator function that yields the
    length of the strings in input_list."""

    # Yield the length of a string
    for person in input_list:
        yield len(person)

# Print the values generated by get_lengths()
for value in get_lengths(lannister):
    print(value)
```

- Wrapping up comprehensions and generators.

```py
# Extract the created_at column from df: tweet_time
tweet_time = df['created_at']

# Extract the clock time: tweet_clock_time.(Access the 12th to 19th characters in the string to extract the time  in which entry[17:19] is equal to '19')
tweet_clock_time = [entry[11:19] for entry in tweet_time if entry[17:19] == '19']

# Print the extracted times
print(tweet_clock_time)
```


## Case study

[Dataset: World Bank World Development Indicators](https://assets.datacamp.com/production/repositories/464/datasets/2175fef4b3691db03449bbc7ddffb740319c1131/world_ind_pop_data.csv)

### Warm up

- Dictionaries for data science

```py
# Zip lists: zipped_lists
zipped_lists = zip(feature_names,row_vals)

# Create a dictionary: rs_dict
rs_dict = dict(zipped_lists)

# Print the dictionary
print(rs_dict)
> {'CountryName': 'Arab World', 'CountryCode': 'ARB', 'IndicatorName': 'Adolescent fertility rate (births per 1,000 women ages 15-19)', 'IndicatorCode': 'SP.ADO.TFRT', 'Year': '1960', 'Value': '133.56090740552298'}
```

- Writing a function to help 

```py
# Define lists2dict()
def lists2dict(list1, list2):
    """Return a dictionary where list1 provides
    the keys and list2 provides the values."""

    # Zip lists: zipped_lists
    zipped_lists = zip(list1, list2)

    # Create a dictionary: rs_dict
    rs_dict = dict(zipped_lists)

    # Return the dictionary
    return dict(rs_dict)

# Call lists2dict: rs_fxn
rs_fxn = lists2dict(feature_names, row_vals)

# Print rs_fxn
print(rs_fxn)
> {'CountryName': 'Arab World', 'CountryCode': 'ARB', 'IndicatorName': 'Adolescent fertility rate (births per 1,000 women ages 15-19)', 'IndicatorCode': 'SP.ADO.TFRT', 'Year': '1960', 'Value': '133.56090740552298'}
```

- Using a list comprehension

```py
# Print the first two lists in row_lists
print(row_lists[0])
print(row_lists[1])

# Turn list of lists into list of dicts: list_of_dicts
list_of_dicts = [lists2dict(feature_names,sublist) for sublist  in row_lists]

# Print the first two dictionaries in list_of_dicts
print(list_of_dicts[0])
print(list_of_dicts[1])
```

- Turning this all into a DataFrame

```py
# Import the pandas package
import pandas as pd

# Turn list of lists into list of dicts: list_of_dicts
list_of_dicts = [lists2dict(feature_names, sublist) for sublist in row_lists]

# Turn list of dicts into a DataFrame: df
df = pd.DataFrame(list_of_dicts)

# Print the head of the DataFrame
print(df.head())
>         print(df.head())
  CountryCode CountryName  ...               Value  Year
0         ARB  Arab World  ...  133.56090740552298  1960
1         ARB  Arab World  ...    87.7976011532547  1960
2         ARB  Arab World  ...   6.634579191565161  1960
3         ARB  Arab World  ...   81.02332950839141  1960
4         ARB  Arab World  ...           3000000.0  1960

[5 rows x 6 columns]
```

### Python generators for streaming data

- Processing data in chunks

```py
# Open a connection to the file
with open('world_dev_ind.csv') as file:

    # Skip the column names
    file.readline()

    # Initialize an empty dictionary: counts_dict
    counts_dict = {}

    # Process only the first 1000 rows
    for j in range(0, 1000):

        # Split the current line into a list: line
        line = file.readline().split(',')

        # Get the value for the first column: first_col
        first_col = line[0]

        # If the column value is in the dict, increment its value
        if first_col in counts_dict.keys():
            counts_dict[first_col] += 1

        # Else, add to the dict and set value to 1
        else:
            counts_dict[first_col] = 1

# Print the resulting dictionary
print(counts_dict)
> {'Arab World': 80, 'Caribbean small states': 77, 'Central Europe and the Baltics': 71, 'East Asia & Pacific (all income levels)': 122, 'East Asia & Pacific (developing only)': 123, 'Euro area': 119, 'Europe & Central Asia (all income levels)': 109, 'Europe & Central Asia (developing only)': 89, 'European Union': 116, 'Fragile and conflict affected situations': 76, 'Heavily indebted poor countries (HIPC)': 18}
```

- Writing a generator to load data in chunks

```py
# Define read_large_file()
def read_large_file(file_object):
    """A generator function to read a large file lazily."""

    # Loop indefinitely until the end of the file
    while True:

        # Read a line from the file: data
        data = file_object.readline()

        # Break if this is the end of the file
        if not data:
            break

        # Yield the line of data
        yield data
        
# Open a connection to the file
with open('world_dev_ind.csv') as file:

    # Create a generator object for the file: gen_file
    gen_file = read_large_file(file)

    # Print the first three lines of the file
    print(next(gen_file))
    print(next(gen_file))
> CountryName,CountryCode,IndicatorName,IndicatorCode,Year,Value
> Arab World,ARB,"Adolescent fertility rate (births per 1,000 women ages 15-19)",SP.ADO.TFRT,1960,133.56090740552298

# Initialize an empty dictionary: counts_dict
counts_dict = {}

# Open a connection to the file
with open('world_dev_ind.csv') as file:

    # Iterate over the generator from read_large_file()
    for line in read_large_file(file):

        row = line.split(',')
        first_col = row[0]

        if first_col in counts_dict.keys():
            counts_dict[first_col] += 1
        else:
            counts_dict[first_col] = 1

# Print            
print(counts_dict)
```

### Writing an iterator to load data in chunks

```py
# Define plot_pop()
def plot_pop(filename, country_code):

    # Initialize reader object: urb_pop_reader
    urb_pop_reader = pd.read_csv(filename, chunksize=1000)

    # Initialize empty DataFrame: data
    data = pd.DataFrame()
    
    # Iterate over each DataFrame chunk
    for df_urb_pop in urb_pop_reader:
        # Check out specific country: df_pop_ceb
        df_pop_ceb = df_urb_pop[df_urb_pop['CountryCode'] == country_code]

        # Zip DataFrame columns of interest: pops
        pops = zip(df_pop_ceb['Total Population'],
                    df_pop_ceb['Urban population (% of total)'])

        # Turn zip object into list: pops_list
        pops_list = list(pops)

        # Use list comprehension to create new DataFrame column 'Total Urban Population'
        df_pop_ceb['Total Urban Population'] = [int(tup[0] * tup[1] * 0.01) for tup in pops_list]
    
        # Append DataFrame chunk to data: data
        data = data.append(df_pop_ceb)

    # Plot urban population data
    data.plot(kind='scatter', x='Year', y='Total Urban Population')
    plt.show()

# Set the filename: fn
fn = 'ind_pop_data.csv'

# Call plot_pop for country code 'CEB'
plot_pop('ind_pop_data.csv','CEB')

# Call plot_pop for country code 'ARB'
plot_pop('ind_pop_data.csv','ARB')
```