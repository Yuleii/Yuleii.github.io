---
layout: article
title: Data Visualization with Seaborn
key: 20200620
tags: Programming
modify_date: 2020-06-20
pageview: false
aside:
  toc: true
---


Base on DataCamp.

<!--more-->

##  Introduction to Seaborn

### Scatter and Count Plot

```py
# Making a scatter plot with lists

## Import Matplotlib and Seaborn
import matplotlib.pyplot as plt
import seaborn as sns

## Change this scatter plot to have percent literate on the y-axis
sns.scatterplot(x=gdp, y=percent_literate)

## Show plot
plt.show()

# Making a count plot with a list
## Create count plot with region on the y-axis
sns.countplot(y=region)

## Show plot
plt.show()
```

### Using pandas with Seaborn

#### Making a count plot with a DataFrame

```py
# Import Matplotlib, Pandas, and Seaborn
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Create a DataFrame from csv file
df = pd.read_csv(csv_filepath)

# Create a count plot with "Spiders" on the x-axis
sns.countplot(x="Spiders", data=df)

# Display the plot
plt.show()
```

### Hue

#### Hue and Scatter Plots

```py
# Change the legend order in the scatter plot
sns.scatterplot(x="absences", y="G3", 
                data=student_data, 
                hue="location",
                hue_order=["Rural","Urban"])

# Show plot
plt.show()
```

#### Hue and Count Plots

```py
# Create a dictionary mapping subgroup values to colors
palette_colors = {"Rural": "green", "Urban": "blue"}

# Create a count plot of school with location subgroups
sns.countplot(x="school", data=student_data, hue="location", palette=palette_colors)

# Display plot
plt.show()
```

## Visualizing Two Quantitative Variables

### Relational Plots and Subplots

#### Creating subplots with col and row

```py
# Change to make subplots based on study time
sns.relplot(x="absences", y="G3", 
            data=student_data,
            kind="scatter",
            col="study_time") # or raw

# Show plot
plt.show()
```

#### Creating two-factor subplots

```py
# Adjust further to add subplots based on family support
sns.relplot(x="G1", y="G3", 
            data=student_data,
            kind="scatter", 
            col="schoolsup",
            col_order=['yes','no'],
            row="famsup",
            row_order=["yes", "no"])

# Show plot
plt.show()
```

### Customizing scatter plots

#### Changing the size and style

```py
# size
# Create scatter plot of horsepower vs. mpg
sns.relplot(x="horsepower", y="mpg", 
            data=mpg, kind="scatter", 
            size="cylinders",
            hue="cylinders")

# Show plot
plt.show()

# style
# Create a scatter plot of acceleration vs. mpg
sns.relplot(x="acceleration",y="mpg",
            data=mpg,
            kind='scatter',
            style="origin",
            hue="origin")
```

### Line Plots

#### Interpreting line plots

```py 
# Create line plot
sns.relplot(x="model_year",y="mpg",
            data=mpg,
            kind='line')

# Show plot
plt.show()
```

#### Visualizing standard deviation

```py
# Make the shaded area show the standard deviation
sns.relplot(x="model_year", y="mpg",
            data=mpg, kind="line", ci='sd')

# Show plot
plt.show()
```

#### Plotting subgroups

```py
# Add markers and make each line have the same style
sns.relplot(x="model_year", y="horsepower", 
            data=mpg, kind="line", 
            ci=None, style="origin", 
            hue="origin", 
            markers=True, 
            dashes=False)

# Show plot
plt.show()
```

## Visualizing a Categorical and a Quantitative Variable

### Count Plots 

```py
# Create column subplots based on age category
sns.catplot(y="Internet usage", # Make the bars horizontal instead of vertical.
            data=survey_data,
            kind="count",
            col="Age Category") # column subplots 

# Show plot
plt.show()
```

### Bar Plots 

```py
# Turn off the confidence intervals
sns.catplot(x="study_time", y="G3",
            data=student_data,
            kind="bar",
            order=["<2 hours", 
                   "2 to 5 hours", 
                   "5 to 10 hours", 
                   ">10 hours"], # rearrange the categories so that they are in order from lowest study time to highest.
            ci=None) # no longer displays confidence intervals.

# Show plot
plt.show()
```

### Box Plots

#### Create and interpret a box plot
```py
# Specify the category ordering
study_time_order = ["<2 hours", "2 to 5 hours", 
                    "5 to 10 hours", ">10 hours"]

# Create a box plot and set the order of the categories
sns.catplot(x="study_time", y="G3", 
            data=student_data,
            kind='box',
            order=study_time_order)
```

#### Omitting outliers

```py
# Create a box plot with subgroups and omit the outliers
sns.catplot(x="internet",y="G3",
            data=student_data,
            kind='box',
            hue="location",
            sym='') # Omitting outliers
```
#### Adjusting the whiskers

```py
# Set the whiskers to 0.5 * IQR
sns.catplot(x="romantic", y="G3",
            data=student_data,
            kind="box",
            whis=0.5) # whis=[5,95]/whis=[0, 100]

# Show plot
plt.show()
```

### Point plots

#### Customizing point plots

```py
# Remove the lines joining the points
sns.catplot(x="famrel", y="absences",
			data=student_data,
            kind="point",
            capsize=0.2, # Add "caps" to the end of the confidence intervals with size 0.2
            join=False) #Remove the lines joining the points in each category.
            
# Show plot
plt.show()
```

#### Point plots with subgroups

```py
# Import median function from numpy
from numpy import median

# Plot the median number of absences instead of the mean
sns.catplot(x="romantic", y="absences",
			data=student_data,
            kind="point",
            hue="school",
            ci=None,
            estimator=median) # display the median number of absences instead of the average

# Show plot
plt.show()
```

## Customizing Seaborn Plots

### Changing style and palette

```py
# Set the style to "whitegrid"
sns.set_style("whitegrid")

# Change the color palette to "RdBu"
sns.set_palette("RdBu")
```

### Changing the scale

```py
# Set the context to "paper"
# Option: "paper","notebook","talk","poster",the later the bigger.
sns.set_context("paper")
```

### Using a custom palette

```py
# Set the style to "darkgrid"
sns.set_style("darkgrid")

# Set a custom color palette
custom_color = ["#39A7D0","#36ADA4"]
sns.set_palette(custom_color)
# Create the box plot of age distribution by gender

sns.catplot(x="Gender", y="Age", 
            data=survey_data, kind="box")

# Show plot
plt.show()
```

### Adding titles and labels
|Object Type|Plot Types|Characteristics|
|-----------|----------|---------------|
| FacetGrid |relplot(), catplot()|Can create subplots|
|AxesSubplot|scatterplot(), countplot(),etc.|Only creates a single plot|

#### Adding a title to FacetGrid

```py
g = sns.catplot(x="Region", 
                y="Birthrate",
                data=gdp_data,
                kind="box") 
g.fig.suptitle("New Title", y=1.03) # y: adjust height of title in FacetGrid
plt.show()
```

#### Adding a title to AxesSubplot

```py
g = sns.boxplot(x="Region", 
                y="Birthrate",
                data=gdp_data,) 
g.set_title("New Title", y=1.03)
plt.show()
```

#### Titles for subplots
```py
g = sns.boxplot(x="Region", 
                y="Birthrate",
                data=gdp_data,
                kind="box",
                col="Group") 
# set main title
g.fig.suptitle("New Title", y=1.03)

# set subtitles
g.set_titles("This is {col_name}")

plt.show()
```

#### Adding axis labels
```py
g.set(xlabel="New X Label",
      ylabel="New Y Label")
```

#### Rotating x-axis tick labels

```py
plt.xticks(rotation=90)
```

### Application

#### Box plot with subgroups

```py
# Set palette to "Blues"
sns.set_palette("Blues")

# Adjust to add subgroups based on "Interested in Pets"
g = sns.catplot(x="Gender",
                y="Age", data=survey_data, 
                kind="box", hue="Interested in Pets")

# Set title to "Age of Those Interested in Pets vs. Not"
g.fig.suptitle("Age of Those Interested in Pets vs. Not")

# Show plot
plt.show()
```

#### Bar plot with subgroups and subplots

```py
# Set the figure style to "dark"
sns.set_style("dark")

# Adjust to add subplots per gender
g = sns.catplot(x="Village - town", y="Likes Techno", 
                data=survey_data, kind="bar",
                col="Gender")

# Add title and axis labels
g.fig.suptitle("Percentage of Young People Who Like Techno", y=1.02)
g.set(xlabel="Location of Residence", 
      ylabel="% Who Like Techno")

# Show plot
plt.show()
```