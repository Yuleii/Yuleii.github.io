---
layout: article
title: Introduction to Data Visualization with Matplotlib
key: 20200702
tags: Python Matplotlib DataAnalysis
modify_date: 2020-07-03
pageview: false
aside:
  toc: true
---

Base on DataCamp.

<!--more-->

[Matplotlib Cheat Sheet](https://datacamp-community-prod.s3.amazonaws.com/28b8210c-60cc-4f13-b0b4-5b4f2ad4790b)

## Introduction to Matplotlib

### Introduction to data visualization with Matplotlib

#### Using the matplotlib.pyplot interface

```py
# Import the matplotlib.pyplot submodule and name it plt
import matplotlib.pyplot as plt

# Create a Figure and an Axes with plt.subplots
fig, ax = plt.subplots()

# Call the show function to show the result
plt.show() # an empty set of axes
```

#### Adding data to an Axes object

```py
# Import the matplotlib.pyplot submodule and name it plt
import matplotlib.pyplot as plt

# Create a Figure and an Axes with plt.subplots
fig, ax = plt.subplots()

# Plot MLY-PRCP-NORMAL from seattle_weather against the MONTH
ax.plot(seattle_weather["MONTH"], seattle_weather['MLY-PRCP-NORMAL'])

# Plot MLY-PRCP-NORMAL from austin_weather against MONTH
ax.plot(austin_weather["MONTH"], austin_weather['MLY-PRCP-NORMAL'])

# Call the show function
plt.show()
```

### Customizing your plots

#### Customizing data appearance

```py
# Plot Seattle data, setting data appearance
ax.plot(seattle_weather["MONTH"], seattle_weather["MLY-PRCP-NORMAL"], color='b', marker='o', linestyle='--') # circle markers ('o')

# Plot Austin data, setting data appearance
ax.plot(austin_weather["MONTH"], austin_weather["MLY-PRCP-NORMAL"], color='r', marker='v', linestyle='--') # triangles pointing downwards ('v')

# Call show to display the resulting plot
plt.show()
```

#### Customizing axis labels and adding titles

```py
ax.plot(seattle_weather["MONTH"], seattle_weather["MLY-PRCP-NORMAL"])
ax.plot(austin_weather["MONTH"], austin_weather["MLY-PRCP-NORMAL"])

# Customize the x-axis label
ax.set_xlabel("Time (months)")

# Customize the y-axis label
ax.set_ylabel("Precipitation (inches)")

# Add the title
ax.set_title("Weather patterns in Austin and Seattle")

# Display the figure
plt.show()
```

### Small multiples

#### Creating small multiples with plt.subplots

```py
# Create a Figure and an array of subplots with 2 rows and 2 columns
fig, ax = plt.subplots(2, 2)

# Addressing the top left Axes as index 0, 0, plot month and Seattle precipitation
ax[0, 0].plot(seattle_weather['MONTH'], seattle_weather['MLY-PRCP-NORMAL'])

# In the top right (index 0,1), plot month and Seattle temperatures
ax[0, 1].plot(seattle_weather['MONTH'], seattle_weather['MLY-TAVG-NORMAL'])

# In the bottom left (1, 0) plot month and Austin precipitations
ax[1, 0].plot(austin_weather['MONTH'], austin_weather['MLY-PRCP-NORMAL'])

# In the bottom right (1, 1) plot month and Austin temperatures
ax[1, 1].plot(austin_weather['MONTH'], austin_weather['MLY-TAVG-NORMAL'])
plt.show()
```

#### Small multiples with shared y axis

This can be configured by setting the `sharey` key-word to `True`.

```py
# Create a figure and an array of axes: 2 rows, 1 column with shared y axis
fig, ax = plt.subplots(2, 1, sharey=True)

# Plot Seattle precipitation data in the top axes. Plot Seattle's "MLY-PRCP-NORMAL" in a solid blue line in the top Axes. Add Seattle's "MLY-PRCP-25PCTL" and "MLY-PRCP-75PCTL" in dashed blue lines to the top Axes.
ax[0].plot(seattle_weather['MONTH'], seattle_weather['MLY-PRCP-NORMAL'], color = 'b')
ax[0].plot(seattle_weather['MONTH'], seattle_weather["MLY-PRCP-25PCTL"], color = 'b', linestyle = '--')
ax[0].plot(seattle_weather['MONTH'], seattle_weather['MLY-PRCP-75PCTL'], color = 'b', linestyle = '--')

# Plot Austin precipitation data in the bottom axes. Plot Austin's "MLY-PRCP-NORMAL" in a solid red line in the top Axes and the "MLY-PRCP-25PCTL" and "MLY-PRCP-75PCTL" in dashed red lines.
ax[1].plot(austin_weather['MONTH'], austin_weather['MLY-PRCP-NORMAL'], color = 'r')
ax[1].plot(austin_weather['MONTH'], austin_weather['MLY-PRCP-25PCTL'], color = 'r', linestyle = '--')
ax[1].plot(austin_weather['MONTH'], austin_weather['MLY-PRCP-75PCTL'], color = 'r', linestyle = '--')

plt.show()
```

## Plotting time-series

### Plotting time-series data

#### Read data with a time index

```py
# Import pandas as pd
import pandas as pd

# Read the data from file using read_csv
climate_change = pd.read_csv('climate_change.csv', parse_dates=True, index_col="date") # Use the parse_dates key-word argument to parse the "date" column as dates. Use the index_col key-word argument to set the "date" column as the index.
```

#### Plot time-series data

```py
import matplotlib.pyplot as plt
fig, ax = plt.subplots()

# Add the time-series for "relative_temp" to the plot. Use the DataFrame index for the x value and the "relative_temp" column for the y values.
ax.plot(climate_change.index, climate_change["relative_temp"])

# Set the x-axis label to 'Time'.
ax.set_xlabel('Time')

# Set the y-axis label to 'Relative temperature (Celsius)'.
ax.set_ylabel('Relative temperature (Celsius)')

# Show the figure
plt.show()
```

#### Using a time index to zoom in

```py
import matplotlib.pyplot as plt

# Use plt.subplots to create fig and ax
fig, ax = plt.subplots()

# Create variable seventies with data from "1970-01-01" to "1979-12-31"
seventies = climate_change["1970-01-01":"1979-12-31"]

# Add the time-series for "co2" data from seventies to the plot
ax.plot(seventies.index, seventies["co2"])

# Show the figure
plt.show()
```

### Plotting time-series with different variables

` .twinx()`

```py
import matplotlib.pyplot as plt

# Initalize a Figure and Axes
fig, ax = plt.subplots()

# Plot the CO2 variable in blue
ax.plot(climate_change.index, climate_change["co2"], color='b')

# Create a twin Axes that shares the x-axis
ax2 = ax.twinx()

# Plot the relative temperature in red
ax2.plot(climate_change.index, climate_change["relative_temp"], color='r')

plt.show()
```

#### Defining a function that plots time-series data

```py
# Define a function called plot_timeseries that takes as input an Axes object (axes), data (x,y), a string with the name of a color and strings for x- and y-axis labels.
def plot_timeseries(axes, x, y, color, xlabel, ylabel):

  # Plot the inputs x,y in the provided color
  axes.plot(x, y, color=color)

  # Set the x-axis label
  axes.set_xlabel(xlabel)

  # Set the y-axis label
  axes.set_ylabel(ylabel, color=color)

  # Set the colors tick params for y-axis
  axes.tick_params('y', colors=color)
```

#### Using a plotting function

```py
fig, ax = plt.subplots()

# Plot the CO2 levels time-series in blue
plot_timeseries(ax, climate_change.index, climate_change["co2"], "blue", "Time (years)", "CO2 levels")

# Create a twin Axes object that shares the x-axis
ax2 = ax.twinx()

# Plot the relative temperature data in red
plot_timeseries(ax2, climate_change.index, climate_change["relative_temp"], "red", "Time (years)", "Relative temperature (Celsius)")

plt.show()
```

### Annotating time-series data

#### Annotating a plot of time-series data

```py
fig, ax = plt.subplots()

# Plot the relative temperature data
ax.plot(climate_change.index, climate_change['relative_temp'])

# Use the annotate method to add the text '>1 degree' in the location (pd.Timestamp('2015-10-06'), 1).
ax.annotate('>1 degree', xy=(pd.Timestamp('2015-10-06'), 1))

plt.show()
```

#### Plotting time-series: putting it all together

```py
fig, ax = plt.subplots()

# Use the plot_timeseries function to plot CO2 levels against time. Set xlabel to "Time (years)" ylabel to "CO2 levels" and color to 'blue'.
plot_timeseries(ax, climate_change.index, climate_change['co2'], 'blue', "Time (years)", "CO2 levels")

# Create an Axes object that shares the x-axis
ax2 = ax.twinx()

# In ax2, plot temperature against time, setting the color ylabel to "Relative temp (Celsius)" and color to 'red'.
plot_timeseries(ax2, climate_change.index, climate_change['relative_temp'], 'red', "Time (years)", "Relative temp (Celsius)")

# Annotate the data using the ax2.annotate method. Place the text ">1 degree" in x=pd.Timestamp('2008-10-06'), y=-0.2 pointing with a gray thin arrow to x=pd.Timestamp('2015-10-06'), y = 1.
ax2.annotate(">1 degree", xy=(pd.Timestamp('2015-10-06'), 1), xytext=(pd.Timestamp('2008-10-06'), -0.2), arrowprops={"arrowstyle":"->", "color":"gray"})

plt.show()
```

## Quantitative comparisons and statistical visualizations

### bar-charts

`ax.bar()`

#### Creating bar chart

```py
fig, ax = plt.subplots()

# Plot a bar-chart of gold medals as a function of country
ax.bar(medals.index, medals["Gold"])

# Set the x-axis tick labels to the country names
ax.set_xticklabels(medals.index, rotation=90) # rotate the x-axis tick labels by 90 degrees

# Set the y-axis label
ax.set_ylabel("Number of medals")

plt.show()
```

#### Stacked bar chart

``` py
# Add bars for "Gold" with the label "Gold"
ax.bar(medals.index, medals["Gold"], label="Gold")

# Stack bars for "Silver" on top with label "Silver"
ax.bar(medals.index, medals["Silver"], bottom=medals["Gold"], label="Silver") # the bottom of the bars will be on top of the gold medal bars

# Stack bars for "Bronze" on top of that with label "Bronze"
ax.bar(medals.index, medals["Bronze"], bottom=medals["Gold"]+medals["Silver"], label="Bronze")

# Display the legend
ax.legend()

plt.show()
```

### histograms

`ax.hist()`

#### Creating histograms

```py
fig, ax = plt.subplots()
# Plot a histogram of "Weight" for mens_rowing
ax.hist(mens_rowing["Weight"])

# Compare to histogram of "Weight" for mens_gymnastics
ax.hist( mens_gymnastics["Weight"])

# Set the x-axis label to "Weight (kg)"
ax.set_xlabel("Weight (kg)")

# Set the y-axis label to "# of observations"
ax.set_ylabel("# of observations")

plt.show()
```

#### "Step" histogram

`ax.hist()`

```py
fig, ax = plt.subplots()

# Use the hist method to display a histogram of the "Weight" column from the mens_rowing DataFrame, label this as "Rowing"
ax.hist(mens_rowing["Weight"], label="Rowing", histtype='step', bins=5)  # use 'step' type and set the number of bins to use to 5.

# Use hist to display a histogram of the "Weight" column from the mens_gymnastics DataFrame, and label this as "Gymnastics"
ax.hist(mens_gymnastics["Weight"], label="Gymnastics", histtype='step', bins=5)

ax.set_xlabel("Weight (kg)")
ax.set_ylabel("# of observations")

# Add the legend and show the Figure
ax.legend()
plt.show()
```

### Statistical plotting

#### Adding error-bars to a bar chart

```py
fig, ax = plt.subplots()

# Add a bar with size equal to the mean of the "Height" column in the mens_rowing DataFrame and an error-bar of its standard deviation
ax.bar("Rowing", mens_rowing["Height"].mean(), yerr=mens_rowing["Height"].std())

# Add another bar for the mean of the "Height" column in mens_gymnastics with an error-bar of its standard deviation.
ax.bar("Gymnastics", mens_gymnastics["Height"].mean(), yerr=mens_gymnastics["Height"].std())

# Label the y-axis
ax.set_ylabel("Height (cm)")

plt.show()
```

#### Adding error-bars to a plot

`ax.errorbar()`

```py
fig, ax = plt.subplots()

# Add Seattle temperature data in each month with error bars
ax.errorbar(seattle_weather["MONTH"], seattle_weather["MLY-TAVG-NORMAL"], yerr=seattle_weather["MLY-TAVG-STDDEV"])

# Add Austin temperature data in each month with error bars
ax.errorbar(austin_weather["MONTH"], austin_weather["MLY-TAVG-NORMAL"], yerr=austin_weather["MLY-TAVG-STDDEV"])

# Set the y-axis label
ax.set_ylabel("Temperature (Fahrenheit)")

plt.show()
```

#### Creating boxplots

`ax.boxplot()`

```py
fig, ax = plt.subplots()

# Create a boxplot that contains the "Height" column for mens_rowing on the left and mens_gymnastics on the right.
ax.boxplot([mens_rowing["Height"], mens_gymnastics["Height"]])

# Add x-axis tick labels:
ax.set_xticklabels(["Rowing", "Gymnastics"])

# Add a y-axis label
ax.set_ylabel("Height (cm)")

plt.show()
```

### Quantitative comparisons: scatter plots

`ax.scatter()`

#### Simple scatter plot

```py
fig, ax = plt.subplots()

# Add data: "co2" on x-axis, "relative_temp" on y-axis
ax.scatter(climate_change["co2"], climate_change["relative_temp"])

# Set the x-axis label to "CO2 (ppm)"
ax.set_xlabel("CO2 (ppm)")

# Set the y-axis label to "Relative temperature (C)"
ax.set_ylabel("Relative temperature (C)")

plt.show()
```

#### Encoding time by color

```py
fig, ax = plt.subplots()

# Add data: "co2", "relative_temp" as x-y, index as color
ax.scatter(climate_change["co2"], climate_change["relative_temp"], c=climate_change.index) # Use the c key-word argument to pass in the index of the DataFrame as input to color each point according to its date.

# Set the x-axis label to "CO2 (ppm)"
ax.set_xlabel("CO2 (ppm)")

# Set the y-axis label to "Relative temperature (C)"
ax.set_ylabel("Relative temperature (C)")

plt.show()
```

## Sharing visualizations with others

### Preparing your figures to share with others

#### Switching between styles

```py
# Use the "ggplot" style and create new Figure/Axes
plt.style.use('ggplot')
fig, ax = plt.subplots()
ax.plot(seattle_weather["MONTH"], seattle_weather["MLY-TAVG-NORMAL"])
plt.show()

# Use the "Solarize_Light2" style and create new Figure/Axes
plt.style.use('Solarize_Light2')
fig, ax = plt.subplots()
ax.plot(austin_weather["MONTH"], austin_weather["MLY-TAVG-NORMAL"])
plt.show()
```

### Saving your visualizations

#### Saving a file several times

```py
# Show the figure
plt.show()

# Save as a PNG file
fig.savefig('my_figure.png')

# Save as a PNG file with 300 dpi
fig.savefig('my_figure_300dpi.png', dpi=300)
```

#### Save a figure with different sizes

```py
# Set the figure size as width of 3 inches and height of 5 inches and save it as 'figure_3_5.png' with default resolution.
fig.set_size_inches([3, 5])
fig.savefig('figure_3_5.png')

# Set the figure size to width of 5 inches and height of 3 inches and save it as 'figure_5_3.png' with default settings.
fig.set_size_inches([5, 3])
fig.savefig('figure_5_3.png')
```

### Automating figures from data

#### Unique values of a column

```py
# Create a variable called sports_column that holds the data from the "Sport" column of the DataFrame object.
sports_column = summer_2016_medals["Sport"]

# Use the unique method of this variable to find all the unique different sports that are present in this data, and assign these values into a new variable called sports
sports = sports_column.unique()

# Print out the unique sports values
print(sports)
> ['Rowing' 'Taekwondo' 'Handball' 'Wrestling' 'Gymnastics' 'Swimming'
 'Basketball' 'Boxing' 'Volleyball' 'Athletics']
```

#### Automate your visualization

```py
fig, ax = plt.subplots()

# Loop over the different sports branches. Iterate over the values of sports setting sport as your loop variable.
for sport in sports:
  # Extract the rows only for this sport. In each iteration, extract the rows where the "Sport" column is equal to sport.
  sport_df = summer_2016_medals[summer_2016_medals["Sport"]==sport]
  # Add a bar for the "Weight" mean with std y error bar
  ax.bar(sport, sport_df["Weight"].mean(), yerr=sport_df["Weight"].std())

ax.set_ylabel("Weight")
ax.set_xticklabels(sports, rotation=90)

# Save the figure to file
fig.savefig("sports_weights.png")
```