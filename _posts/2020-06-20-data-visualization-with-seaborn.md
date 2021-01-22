---
layout: article
title: Data Visualization with Seaborn
key: 20200620
tags: Python Seaborn DataAnalysis
modify_date: 2020-06-21
pageview: false
aside:
  toc: true
---


Base on DataCamp.

<!--more-->

[Seaborn Cheat Sheet ](https://datacamp-community-prod.s3.amazonaws.com/f9f06e72-519a-4722-9912-b5de742dbac4)

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
            # rearrange the categories so that they are in order from lowest study time to highest.
            order=["<2 hours", 
                   "2 to 5 hours", 
                   "5 to 10 hours", 
                   ">10 hours"], 
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
            # Add "caps" to the end of the confidence intervals with size 0.2
            capsize=0.2, 
            # Remove the lines joining the points in each category.
            join=False) 
            
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
            # display the median number of absences instead of the average
            estimator=median) 

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

|---
| FacetGrid | relplot(), catplot()| Can create subplots
|:-:|:-:|:-:
| AxesSubplot | relplot(), catplot() | Can create subplots 
| AxesSubplot |scatterplot(), countplot(),etc. | Only creates a single plot 
|---
  

#### Adding a title to FacetGrid

```py
g = sns.catplot(x="Region", 
                y="Birthrate",
                data=gdp_data,
                kind="box") 
# y: adjust height of title in FacetGrid
g.fig.suptitle("New Title", y=1.03) 
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

## Intermediate Seaborn

### Distribution Plot

#### Plot a histogram

```py
# Create a distplot
sns.distplot(df['Award_Amount'],
            # disable the KDE to get histogram
             kde=False,
             bins=20)

# Display the plot
plt.show()
```

#### Rug plot and kde shading

```py
# Create a distplot of the Award Amount
sns.distplot(df['Award_Amount'],
             hist=False,
             # Add a rug plot above the x axis
             rug=True, 
             # Configure it to show a shaded kde (using the kde_kws dictionary).
             kde_kws={'shade':True})

# Plot the results
plt.show()
```

### Regression Plots in Seaborn

#### regplot()

```py
# Create a regression plot of premiums vs. insurance_losses
sns.regplot(x="insurance_losses", y="premiums", data=df)

# Display the plot
plt.show()
```

#### lmplot()

```py
# Create a regression plot using hue
sns.lmplot(data=df,
           x="insurance_losses",
           y="premiums",
           # Plot a regression line for each Region of the country.
           hue="Region",
           # Create a plot for each Region of the country.
           row="Region")

# Show the results
plt.show()
```

## Customizing Distribution Plot

[python matplotlib中axes与axis的区别](https://www.zhihu.com/question/51745620)

### Using Seaborn Styles

#### Setting the default style

```py
# Set the default seaborn style
sns.set()

# Plot the pandas histogram 
df['fmr_2'].plot.hist()
plt.show()
plt.clf()
```

#### Removing spines

```py
# Set the style to white
sns.set_style('white')

# Create a regression plot
sns.lmplot(data=df,
           x='pop2010',
           y='fmr_2')

# Remove the spines
sns.despine(right=True)

# Show the plot and clear the figure
plt.show()
plt.clf()
```

### Colors in Seaborn

#### Matplotlib color codes

```py
# Set style, enable color code, and create a magenta distplot
sns.set(color_codes=True)
sns.distplot(df['fmr_3'], color='m')

# Show the plot
plt.show()
```

#### Using default palettes

- Circular colors = when the data is not ordered
- Sequential colors = when the data has a consistent range from high to low
- Diverging colors = when both the low and high values are interesting

```py
# Loop through differences between bright and colorblind palettes
for p in ['bright', 'colorblind']:
    sns.set_palette(p)
    sns.distplot(df['fmr_3'])
    plt.show()
    
    # Clear the plots    
    plt.clf()
```

#### Creating Custom Palettes

```py
# Create and display a Purples sequential palette containing 8 colors.
sns.palplot(sns.color_palette( "Purples", 8))
plt.show()

# Create and display a palette with 10 colors using the husl system.
sns.palplot(sns.color_palette( "husl", 10))
plt.show()

# Create and display a diverging palette with 6 colors coolwarm.
sns.palplot(sns.color_palette( "coolwarm", 6))
plt.show()
```

### Customizing with matplotlib

#### Using matplotlib axes

```py
# Create a figure and axes
fig, ax = plt.subplots()

# Plot the distribution of data
sns.distplot(df['fmr_3'], ax=ax)

# Create a more descriptive x axis label
ax.set(xlabel="3 Bedroom Fair Market Rent")

# Show the plot
plt.show()
```

#### Additional plot customizations

```py
# Create a figure and axes
fig, ax = plt.subplots()

# Plot the distribution of 1 bedroom rents
sns.distplot(df['fmr_1'], ax=ax)

# Modify the properties of the plot
ax.set(xlabel="1 Bedroom Fair Market Rent",
       # Change the x axis limits to be between 100 and 1500.
       xlim=(100,1500),
       # Add a descriptive title of "US Rent" to the plot.
       title="US Rent")

# Display the plot
plt.show()
```

#### Adding annotations

```py
# Create a figure and axes. Then plot the data
fig, ax = plt.subplots()
sns.distplot(df['fmr_1'], ax=ax)

# Customize the labels and limits
ax.set(xlabel="1 Bedroom Fair Market Rent", xlim=(100,1500), title="US Rent")

# Add vertical lines for the median and mean
ax.axvline(x=median, color='m', label='Median', linestyle='--', linewidth=2)
ax.axvline(x=mean, color='b', label='Mean', linestyle='-', linewidth=2)

# Show the legend and plot the data
ax.legend()
plt.show()
```

#### Multiple plots

```py
# Create a plot with 1 row and 2 columns that share the y axis label
fig, (ax0, ax1) = plt.subplots(nrows=1, ncols=2, sharey=True)

# Plot the distribution of 1 bedroom apartments on ax0
sns.distplot(df['fmr_1'], ax=ax0)
ax0.set(xlabel="1 Bedroom Fair Market Rent", xlim=(100,1500))

# Plot the distribution of 2 bedroom apartments on ax1
sns.distplot(df['fmr_2'], ax=ax1)
ax1.set(xlabel="2 Bedroom Fair Market Rent", xlim=(100,1500))
```

## Additional Plot Types

### Categorical Plot Types

#### stripplot() and swarmplot()

```py
# Create the stripplot
sns.stripplot(data=df,
         x='Award_Amount',
         y='Model Selected',
         jitter=True)

plt.show()
# Create and display a swarmplot with hue set to the Region
sns.swarmplot(data=df,
         x='Award_Amount',
         y='Model Selected',
         hue='Region')

plt.show()
```

### boxplots, violinplots and lvplots

```py
# Create a boxplot
sns.boxplot(data=df,
         x='Award_Amount',
         y='Model Selected')

plt.show()
plt.clf()

# Create a violinplot with the husl palette
sns.violinplot(data=df,
         x='Award_Amount',
         y='Model Selected',
         palette='husl')

plt.show()
plt.clf()

# Create a lvplot with the Paired palette and the Region column as the hue
sns.lvplot(data=df,
         x='Award_Amount',
         y='Model Selected',
         palette='Paired',
         hue='Region')

plt.show()
plt.clf()
```

#### barplots, pointplots and countplots
```py
# Show a countplot with the number of models used with each region a different color
sns.countplot(data=df,
         y="Model Selected",
         hue="Region")

plt.show()
plt.clf()

# Create a pointplot and include the capsize in order to show bars on the confidence interval
sns.pointplot(data=df,
         y='Award_Amount',
         x='Model Selected',
         # Use a capsize in the pointplot in order to show the confidence interval.
         capsize=.1)

plt.show()
plt.clf()
```

### Regression Plots

#### Regression and residual plots

```py
# Display a regression plot for Tuition
sns.regplot(data=df,
         y='Tuition',
         x="SAT_AVG_ALL",
         marker='^',
         color='g')

plt.show()
plt.clf()

# Display the residual plot
sns.residplot(data=df,
          y='Tuition',
          x="SAT_AVG_ALL",
          color='g')

plt.show()
plt.clf()
```

#### Regression plot parameters

```py
# Plot a regression plot of Tuition and the Percentage of Pell Grants
sns.regplot(data=df,
            y='Tuition',
            x="PCTPELL",
            #  breaks the PCTPELL column into 5 different bins.
            x_bins=5,
            # using a 2nd order polynomial regression line
            order=2)

plt.show()
plt.clf()
```

#### Binning data

```py
# Create a scatter plot by disabling the regression line
sns.regplot(data=df,
            y='Tuition',
            x="UG",
            # disable the regression line
            fit_reg=False) 

plt.show()
plt.clf()

# Create a regplot and bin the data into 8 bins
sns.regplot(data=df,
         y='Tuition',
         x="UG",
         x_bins=8)

plt.show()
plt.clf()
```

### Matrix plots

```py
# Create a crosstab table of the data
pd_crosstab = pd.crosstab(df["Group"], df["YEAR"])
print(pd_crosstab)

# Plot a heatmap of the table with no color bar and using the BuGn palette
sns.heatmap(pd_crosstab, cbar=False, cmap="BuGn", linewidths=0.3)

# Rotate tick marks for visibility
plt.yticks(rotation=0)
plt.xticks(rotation=90)

plt.show()
```

## Creating Plots on Data Aware Grids

### Using FacetGrid, factorplot and lmplot

#### Building a FacetGrid

```py
# Create FacetGrid with Degree_Type and specify the order of the rows using row_order
g2 = sns.FacetGrid(df, 
             row="Degree_Type",
             row_order=['Graduate', 'Bachelors', 'Associates', 'Certificate'])

# Map a pointplot of SAT_AVG_ALL onto the grid
g2.map(sns.pointplot, 'SAT_AVG_ALL')

# Show the plot
plt.show()
plt.clf()
```

#### Using a factorplot

In many cases, Seaborn's `factorplot()` can be a simpler way to create a `FacetGrid`. Instead of creating a grid and mapping the plot, we can use the `factorplot()` to create a plot with one line of code.

```py
# Create a facetted pointplot of Average SAT_AVG_ALL scores facetted by Degree Type 
sns.factorplot(data=df,
        x='SAT_AVG_ALL',
        # shows a pointplot
        kind='point',
        row='Degree_Type',
        # Use row_order to order the degrees from highest to lowest level.
        row_order=['Graduate', 'Bachelors', 'Associates', 'Certificate'])

plt.show()
plt.clf()
```

#### Using a lmplot
The `lmplot` is used to plot scatter plots with regression lines on `FacetGrid` objects. 

```py
# Create a FacetGrid varying by column and columns ordered with the degree_order variable
g = sns.FacetGrid(df, col="Degree_Type", col_order=degree_ord)

# Map a scatter plot of Undergrad Population compared to PCTPELL
g.map(plt.scatter, 'UG', 'PCTPELL')

plt.show()
plt.clf()

# Re-create the plot above as an lmplot
sns.lmplot(data=df,
        x='UG',
        y='PCTPELL',
        col="Degree_Type",
        col_order=degree_ord)

plt.show()
plt.clf()

# Create an lmplot that has a column for Ownership, a row for Degree_Type and hue based on the WOMENONLY column
sns.lmplot(data=df,
        x='SAT_AVG_ALL',
        y='Tuition',
        col="Ownership",
        row='Degree_Type',
        row_order=['Graduate', 'Bachelors'],
        hue='WOMENONLY',
        col_order=inst_ord)

plt.show()
plt.clf()
```

### Using PairGrid and pairplot

#### Building a PairGrid
```py
# Create a PairGrid with a scatter plot for fatal_collisions and premiums
g = sns.PairGrid(df, vars=["fatal_collisions", "premiums"])
g2 = g.map(plt.scatter)

plt.show()
plt.clf()

# Create the same PairGrid but map a histogram on the diag
g = sns.PairGrid(df, vars=["fatal_collisions", "premiums"])
g2 = g.map_diag(plt.hist) #  plot a histogram on the diagonal
g3 = g2.map_offdiag(plt.scatter) # scatter plot on the off diagonal

plt.show()
plt.clf()
```

#### Using a pairplot

The `pairplot()` function is generally a more convenient way to look at pairwise relationships. 

```py
# Plot the same data but use a different color palette and color code by Region
sns.pairplot(data=df,
        vars=["fatal_collisions", "premiums"],
        kind='scatter',
        # using the "Region" to color code the results
        hue='Region',
        # Use the RdBu palette to change the colors of the plot
        palette='RdBu',
        diag_kws={'alpha':.5})

plt.show()
plt.clf()
```

#### Additional pairplots

```py
# Build a pairplot with different x and y variables
sns.pairplot(data=df,
        # define the x_vars and y_vars that you wish to examine
        x_vars=["fatal_collisions_speeding", "fatal_collisions_alc"],
        y_vars=['premiums', 'insurance_losses'],
        kind='scatter',
        # Use the husl palette and color code the scatter plot by Region
        hue='Region',
        palette='husl')

plt.show()
plt.clf()

# plot relationships between insurance_losses and premiums
sns.pairplot(data=df,
             vars=["insurance_losses", "premiums"],
             # Use a reg plot for the the non-diagonal plots
             kind='reg',
             # Use the BrBG palette for the final plot.
             palette='BrBG',
             # diag_kind to control the types of plots shown on the diagonals.
             diag_kind = 'kde',
             hue='Region')

plt.show()
plt.clf()
```

### Using JointGrid and jointplot

#### Building a JointGrid and jointplot
Seaborn's `JointGrid` combines univariate plots such as histograms, rug plots and kde plots with bivariate plots such as scatter and regression plots. 

```py
# Build a JointGrid comparing humidity and total_rentals
sns.set_style("whitegrid") # Use Seaborn's "whitegrid" style for these plots.
g = sns.JointGrid(x="hum",
            y="total_rentals",
            data=df,
            xlim=(0.1, 1.0)) 

# Plot a regplot() and distplot() on the margins.
g.plot(sns.regplot, sns.distplot)

plt.show()
plt.clf()

# Create a jointplot similar to the JointGrid 
sns.jointplot(x="hum",
        y="total_rentals",
        kind='reg',
        data=df)

plt.show()
plt.clf()
```

#### Jointplots and regression

```py
# Plot temp vs. total_rentals as a regression plot
sns.jointplot(x="temp",
         y="total_rentals",
         kind='reg',
         data=df,
         # 2nd order polynomial regression
         order=2,
         xlim=(0, 1))

plt.show()
plt.clf()

# Plot a jointplot showing the residuals to check the appropriateness of the model.
sns.jointplot(x="temp",
        y="total_rentals",
        kind='resid',
        data=df,
        order=2)

plt.show()
plt.clf()
```

#### Complex jointplots

The `jointplot` is a convenience wrapper around many of the `JointGrid` functions. However, it is possible to overlay some of the `JointGrid` plots on top of the standard `jointplot`

```py
# Create a jointplot of temp vs. casual riders
# Include a kdeplot over the scatter plot
g = (sns.jointplot(x="temp",
             y="casual",
             kind='scatter',
             data=df,
             marginal_kws=dict(bins=10, rug=True))
    .plot_joint(sns.kdeplot)) # Overlay a kdeplot on top of the scatter plot.
    
plt.show()
plt.clf()
```