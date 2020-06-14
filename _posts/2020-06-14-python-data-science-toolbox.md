---
layout: article
title: Python Data Science Toolbox
key: 20200614
tags: Programming
modify_date: 2020-06-14
pageview: false
aside:
  toc: true
---


Base on DataCamp.

<!--more-->

## Write function

### Functions that return single values
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

### Multiple parameters and return values
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

### Twitter dataframe analysis

```py
# The dataset contains Twitter data and you will iterate over entries in a column to build a dictionary in which the keys are the names of languages and the values are the number of tweets in the given language.
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

## Default arguments, variable-length arguments and scope

### Scope

```py
# when we reference a name, first the local scope is searched, then the global. If the name is in neither, then the built-in scope is searched.
# LEGB rule,L for local, E for enclosing functions,G for global and B for built-in.
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

### Nested functions

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