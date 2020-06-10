---
layout: article
title: Notes on python
permalink: /page/aside.html
key: 20200610
tags: Programming
aside:
  toc: true
---


Based on Datacamp.

<!--more-->


## Matplotlib

[Python for data science Cheat Sheet](https://datacamp-community-prod.s3.amazonaws.com/e30fbcd9-f595-4a9f-803d-05ca5bf84612)  
[Gapminder](https://assets.datacamp.com/production/repositories/287/datasets/5b1e4356f9fa5b5ce32e9bd2b75c777284819cca/gapminder.csv)  
[Car](https://assets.datacamp.com/production/repositories/287/datasets/79b3c22c47a2f45a800c62cae39035ff2ea4e609/cars.csv)  
[BRICS](https://assets.datacamp.com/production/repositories/287/datasets/b60fb5bdbeb4e4ab0545c485d351e6ff5428a155/brics.csv)

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

## Histogram

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

## Customization

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