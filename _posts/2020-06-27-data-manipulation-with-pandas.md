---
layout: article
title: Data Manipulation with pandas
key: 20200628
tags: Programming
modify_date: 2020-06-27
pageview: false
aside:
  toc: true
---

Base on DataCamp.

<!--more-->

## DataFrames

### Introducing DataFrames

#### Inspecting a DataFrame

- `.head()` returns the first few rows (the “head” of the DataFrame).
- `.info()` shows information on each of the columns, such as the data type and number of missing values.
- `.shape` returns the number of rows and columns of the DataFrame.
- `.describe()` calculates a few summary statistics for each column.

```py
# Print the head of the homelessness data
print(homelessness.head())

# Print information about homelessness
print(homelessness.info())

# Print the shape of homelessness
print(homelessness.shape)

# Print a description of homelessness
print(homelessness.describe())
```

#### Parts of a DataFrame

- `.values`: A two-dimensional NumPy array of values.
- `.columns`: An index of columns: the column names.
- `.index`: An index for the rows: either row numbers or row names.

```py
# Import pandas using the alias pd
import pandas as pd

# Print a 2D NumPy array of the values in homelessness.
print(homelessness.values)

# Print the column names of homelessness
print(homelessness.columns)

# Print the row index of homelessness
print(homelessness.index)
```

### Sorting and subsetting

#### Sorting rows

```py
# Sort homelessness by individual
homelessness_ind = homelessness.sort_values('individuals')

# Sort homelessness by descending family members
homelessness_fam = homelessness.sort_values('family_members',ascending=False)

# Sort homelessness by region, then descending family members
homelessness_reg_fam = homelessness.sort_values(['region','family_members'], ascending = [True, False])
```

#### Subsetting columns

```py
# Select the individuals column
individuals = homelessness['individuals']

# Select the state and family_members columns
state_fam = homelessness[['state','family_members']]

# Select only the individuals and state columns, in that order
ind_state = homelessness[['individuals','state']]
```

#### Subsetting rows

```py
# Filter for rows where individuals is greater than 10000
ind_gt_10k = homelessness[homelessness['individuals']>10000]

# Filter for rows where region is Mountain
mountain_reg = homelessness[homelessness['region']=="Mountain"]

# Filter for rows where family_members is less than 1000 
# and region is Pacific
fam_lt_1k_pac = homelessness[(homelessness['family_members']<1000) & (homelessness['region']=="Pacific")]
```

#### Subsetting rows by categorical variables

`|`, `.isin()`

```py
# Subset for rows in South Atlantic or Mid-Atlantic regions
south_mid_atlantic = homelessness[(homelessness['region']=="South Atlantic") | (homelessness['region']=="Mid-Atlantic")]

# The Mojave Desert states
canu = ["California", "Arizona", "Nevada", "Utah"]

# Filter for rows in the Mojave Desert states
mojave_homelessness = homelessness[homelessness['state'].isin(canu)]
```

### New columns

```py
# Add total col as sum of individuals and family_members
homelessness['total'] = homelessness['individuals'] + homelessness['family_members']

# Add p_individuals col as proportion of individuals
homelessness['p_individuals'] = homelessness['individuals'] / homelessness['total']

# See the result
print(homelessness)
```

### Combo-attack!

```py
# Create indiv_per_10k col as homeless individuals per 10k state pop
homelessness["indiv_per_10k"] = 10000 * homelessness["individuals"] / homelessness["state_pop"]

# Subset rows for indiv_per_10k greater than 20
high_homelessness = homelessness[homelessness['indiv_per_10k']>20]

# Sort high_homelessness by descending indiv_per_10k
high_homelessness_srt = high_homelessness.sort_values('indiv_per_10k', ascending=False)

# From high_homelessness_srt, select the state and indiv_per_10k cols
result = high_homelessness_srt[['state','indiv_per_10k']]

# See the result
print(result)
```