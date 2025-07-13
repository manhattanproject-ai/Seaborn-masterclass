<div align="left">
  <h1> Seaborn Cheatsheet

  ## Seaborn

Seaborn is a powerful and popular Python library specifically designed for creating attractive and informative statistical graphics. Built on top of Matplotlib, it offers a higher-level interface that simplifies the process of generating complex visualizations, especially when working with Pandas DataFrames. Seaborn excels at helping users explore and understand their data by providing a wide array of specialized plot types for visualizing relationships between variables, distributions, and categorical data, often incorporating statistical estimations like regression lines or confidence intervals automatically. Its appealing default styles, color palettes, and concise syntax make it a go-to tool for data scientists and analysts seeking to effectively communicate insights from their data with minimal coding effort.

### 1. Build in Datasets

```shell
tips
iris
penguins
flights
diamonds
titanic
exercise
mpg
planets
anagrams
anscombe
attention
brain_networks
car_crashes
dots
dowjones
fmri
geyser
glue
healthexp
seaice
taxis
```

### 2. Load the dataset

```py
import seaborn as sns

# Load the tips dataset
tips = sns.load_dataset('tips')
```

### 3. Customizing Seaborn Styles

Seaborn styles are predefined aesthetic settings that quickly change the overall look and feel of your Matplotlib plots to make them more visually appealing and suitable for statistical graphics.

```shell
darkgrid : A dark background and white gridlines
whitegrid : A light background  with white gridline
dark :  A dark background style without gridlines
white : A light background style without gridlines
ticks : A variation of the white style that adds ticks to the axes
```

```py

# Set the style
sns.set_style("style_name")
```

### 4. Adjusting Plot Context

In Seaborn, plot context refers to the scaling of plot elements (like labels, lines, and markers) to make them appropriate for different types of output (e.g., paper, notebook, talk, poster) without changing the data itself.

```shell
paper: Designed for plots that will be included in academic papers or reports. It's the smallest context, with smaller font sizes and thinner lines, suitable for compact figures.
notebook: This is the default context in Seaborn. It's balanced for interactive work in Jupyter notebooks and general data exploration.
talk: Optimized for presentations, like a talk or a slideshow. Elements are larger than in notebook to be easily visible from a distance.
poster: The largest context, ideal for large-format posters or displays where elements need to be highly visible from far away.
```

```py

# Set the context
 sns.set_context("preset_name")
```
### 5. Color Palettes

```shell
1. Qualitative Palettes (for categorical data): These palettes use distinct hues to differentiate categories where there's no inherent order.

deep (default)
muted
pastel
bright
dark
colorblind
tab10 (Matplotlib default, also available in Seaborn)
tab20, tab20b, tab20c
hls
husl
Set1, Set2, Set3
Paired
Accent
Dark2
Pastel1, Pastel2
```

```shell
2. Sequential Palettes (for numerical data with an ordered progression, e.g., low to high): These palettes typically use variations in lightness and/or saturation, often within a single hue or a limited range of hues.

rocket (perceptually uniform)
mako (perceptually uniform)
flare (perceptually uniform)
crest (perceptually uniform)
viridis (perceptually uniform, Matplotlib colormap)
plasma (perceptually uniform, Matplotlib colormap)
inferno (perceptually uniform, Matplotlib colormap)
magma (perceptually uniform, Matplotlib colormap)
cividis (perceptually uniform, Matplotlib colormap)
Greys, Reds, Greens, Blues, Oranges, Purples (single-hue Brewer palettes)
BuGn, BuPu, GnBu, OrRd, PuBu, PuRd, RdPu, YlGn, PuBuGn, YlGnBu, YlOrBr, YlOrRd (multi-hue Brewer palettes)
```

```shell
3. Diverging Palettes (for numerical data with a critical central value, e.g., deviations from zero, positive/negative values): These palettes typically use two contrasting hues that diverge from a neutral central color.

RdBu
RdGy
PRGn
PiYG
BrBG
RdYlBu
RdYlGn
Spectral
coolwarm (often used as a diverging palette)
bwr
```

```shell
4. Miscellaneous/Matplotlib Colormaps: Seaborn also makes many standard Matplotlib colormaps easily accessible. Some examples include:

afmhot
autumn
binary
bone
brg
cool
copper
cubehelix
flag
gist_earth
gist_gray
gist_heat
gist_ncar
gist_rainbow
gist_stern
gist_yarg
gnuplot
gnuplot2
jet
nipy_spectral
ocean
prism
rainbow
terrain
turbo
Wistia
```

```py

# Set the build in palette
 sns.set_palette("palette_name")   # Apply a built-in palett
```

### 6.  Line Plot

 It visualizes the change in a trend over time or another continuous variable. 

![Screenshot 2025-06-09 003312](https://github.com/user-attachments/assets/75df6b3b-3803-43fc-855b-981f42885948)

```py

import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the line plot
sns.lineplot(x="day", y="size", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Average Party Size by Day")
plt.xlabel("Day of the Week")
plt.ylabel("Average Party Size")

plt.show()
```

### 7. Scatter Plot

Examines relationships and distributions of two variables

![Screenshot 2025-06-09 003540](https://github.com/user-attachments/assets/4179965c-99a3-4733-95cd-02ca1816f629)

```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the scatter plot
sns.scatterplot(x="total_bill", y="tip", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Total Bill vs. Tip Amount")
plt.xlabel("Total Bill ($)")
plt.ylabel("Tip Amount ($)")

plt.show()
```

### 8. RelPlot

Visualizes statistical relationships across different categories

![Screenshot 2025-06-09 004028](https://github.com/user-attachments/assets/063d5b84-18ed-442b-a5fd-9651fd53dee2)

```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the relplot (relational plot)
# By default, kind='scatter', so this is similar to scatterplot but can also do line plots.
sns.relplot(x="total_bill", y="tip", data=tips , kind = "line")

# Optional: Add a title for clarity (relplot creates a FacetGrid, so suptitle is often used)
plt.suptitle('Relational Plot: Total Bill vs. Tip Amount', y=1.02) # y adjusts title position

plt.show()
```
![Screenshot 2025-06-09 004225](https://github.com/user-attachments/assets/0fcf0a51-22dd-43d4-82c6-02b31bc1249f)

```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Example with 'hue'  to show more relationships
sns.relplot(x="total_bill", y="tip", hue="smoker", data=tips)
plt.suptitle('Relational Plot: Total Bill vs. Tip (by Smoker)', y=1.02)
plt.show()
```
### 9. Heatmap

 Displays complexity in multivariate data, often in matrix format

![Screenshot 2025-06-09 004409](https://github.com/user-attachments/assets/d06ab3bb-dd46-49fc-9e0a-fdb6c1b233c2)

```py
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd # Ensure pandas is imported for pivot_table

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create a pivot table with average total_bill by day and time
# Using 'day' as index and 'time' as columns, and 'total_bill' for values.
# This creates a 2D grid suitable for a heatmap.
pivot_table = tips.pivot_table(index='day', columns='size', values='tip',
aggfunc='mean')

# Create a heatmap showing the average total_bill by day and time
plt.figure(figsize=(8, 6)) # Optional: control the figure size
ax = sns.heatmap(pivot_table, annot=True, fmt=".2f", cmap="coolwarm", linewidths=.5)

# Optional: Add a title
plt.title('Average Tips by Day and Size')
plt.xlabel('Size') # Update xlabel as columns is now 'size'
plt.ylabel('Day of the Week')

plt.show()
```
### 10. clustermap

Visualizes structures in matrix data where similar clusters are grouped

![Screenshot 2025-06-09 004742](https://github.com/user-attachments/assets/842bd4fc-c135-4b99-96c6-4c725aa58d58)

```py
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd # Ensure pandas is imported if not already

# Load the tips dataset
tips = sns.load_dataset('tips')

# Select only numerical columns (as per your request)
# Ensure these columns exist in your tips dataset.
# The 'tips' dataset has 'total_bill', 'tip', and 'size' as numerical.
numerical_tips = tips[['total_bill', 'tip', 'size']]

# Generate the clustermap
plt.figure(figsize=(8, 7)) # Optional: controls the overall figure size
sns.clustermap(numerical_tips, cmap='coolwarm', standard_scale=1)

# Note: clustermap manages its own figure and axes, so plt.show() is still needed
plt.show()
```
### 11. Box Plot

 Visualizes distributions with quartiles and outliers

![Screenshot 2025-06-09 004951](https://github.com/user-attachments/assets/2fbe7202-44bd-4d1d-a7c3-7766f6ddf316)

```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the box plot
plot = sns.boxplot(x="day", y="total_bill", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Total Bill Distribution by Day of the Week")
plt.xlabel("Day of the Week")
plt.ylabel("Total Bill ($)")

plt.show()
```

### 12. Violin Plot

Visualizes the distribution and probability density of data

![Screenshot 2025-06-09 005143](https://github.com/user-attachments/assets/d8dc30cc-4e17-4158-870c-115433defe00)


```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the box plot
plot = sns.violinplot(x="day", y="total_bill", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Total Bill Distribution by Day of the Week")
plt.xlabel("Day of the Week")
plt.ylabel("Total Bill ($)")

plt.show()
```
### 13. Bar Plot

Compares numerical values across different categories

![Screenshot 2025-06-09 005344](https://github.com/user-attachments/assets/a515cbab-350d-4ddd-82d2-78263509eb94)

```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the box plot
plot = sns.barplot(x="day", y="total_bill", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Total Bill Distribution by Day of the Week")
plt.xlabel("Day of the Week")
plt.ylabel("Total Bill ($)")

plt.show()
```

### 14. Count Plot

Displays the counts of observations or frequency of categories

![Screenshot 2025-06-09 005531](https://github.com/user-attachments/assets/756d1a2b-924b-41db-8834-c0403b8744d2)


```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the count plot
# A count plot shows the counts of observations in each category using bars.
sns.countplot(x="day", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Number of Observations per Day of the Week")
plt.xlabel("Day of the Week")
plt.ylabel("Count")

plt.show()
```
### 15. Point Plot

Displays point estimates with error bars, emphasizing differences between groups

![Screenshot 2025-06-09 005758](https://github.com/user-attachments/assets/e5311526-590c-4965-947e-55282a3b3818)


```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the point plot
plot = sns.pointplot(x="day", y="total_bill", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Average Total Bill by Day with Confidence Intervals")
plt.xlabel("Day of the Week")
plt.ylabel("Average Total Bill ($)")

plt.show()
```
### 16. Swarm Plot

Displays distribution of categorical data, avoiding overlapping points

![Screenshot 2025-06-09 005958](https://github.com/user-attachments/assets/e1c479e3-2f05-45ee-990e-1251b3e28de0)


```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the swarm plot
# Swarm plots show each individual observation, avoiding overlap.
sns.swarmplot(x="day", y="total_bill", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Total Bill Distribution by Day of the Week (Swarm Plot)")
plt.xlabel("Day of the Week")
plt.ylabel("Total Bill ($)")

plt.show()
```
### 17. Strip Plot

Represents individual data points in a categorical scatterplot

![Screenshot 2025-06-09 010325](https://github.com/user-attachments/assets/9ab60afe-3907-4301-89ed-69c43a226c90)

```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the strip plot
sns.stripplot(x="day", y="total_bill", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Total Bill Distribution by Day of the Week")
plt.xlabel("Day of the Week")
plt.ylabel("Total Bill ($)")

plt.show()
```

### 18. Cat Plot

All-in-one method for creating various categorical plots

![Screenshot 2025-06-09 010541](https://github.com/user-attachments/assets/84a25a66-8f66-4288-ac74-6c0b607d0654)


```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the catplot (categorical plot)
# By default, kind='strip', but it can also be 'box', 'violin', 'bar', 'count', 'point', 'swarm'
sns.catplot(x="day", y="total_bill", data=tips, kind="box")

# Optional: Add a title for clarity (catplot creates a FacetGrid, so suptitle is often used)
plt.suptitle('Total Bill Distribution by Day of the Week (Box Plot)', y=1.02)

plt.show()
```

### 19. Reg Plot

Visualizes a simple linear relationship between two variables

![Screenshot 2025-06-09 010953](https://github.com/user-attachments/assets/5e24ee8d-9dbc-437e-be4d-76d9d0b818db)


```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the regplot (regression plot)
sns.regplot(x="total_bill", y="tip", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Regression Plot: Total Bill vs. Tip Amount")
plt.xlabel("Total Bill ($)")
plt.ylabel("Tip Amount ($)")

plt.show()
```

### 20. Lm Plot

Displays multiple regression plots for subsets of a dataset

![Screenshot 2025-06-09 011348](https://github.com/user-attachments/assets/a986e362-3c5f-4a88-bb5b-e756566bd79e)


```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the lmplot (linear model plot)
# This plots scatter data with a linear regression model fit
sns.lmplot(x="total_bill", y="tip", data=tips)

# Optional: Add a title (lmplot creates a FacetGrid, so suptitle is often used)
plt.suptitle('Linear Model Plot: Total Bill vs. Tip Amount', y=1.02) # y adjusts title position

plt.show()
```

### 21. Displot 

Summarizes the distribution of a dataset

![Screenshot 2025-06-09 011530](https://github.com/user-attachments/assets/0e3be974-de01-4973-9b77-38a13f2ac60c)


```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the displot (distribution plot)
# By default, kind='hist' (histogram)
sns.displot(x="total_bill", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Distribution of Total Bill Amounts")
plt.xlabel("Total Bill ($)")
plt.ylabel("Count")

plt.show()
```
### 22. KDE Plot

Visualizes the distribution of a dataset

![Screenshot 2025-06-09 011709](https://github.com/user-attachments/assets/ceb28384-ba9f-48c2-ba7c-48ef74d17470)


```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the KDE plot for the distribution of 'total_bill'
sns.kdeplot(x="total_bill", data=tips)

# Optional: Add a title and labels for clarity
plt.title("KDE Plot of Total Bill Distribution")
plt.xlabel("Total Bill ($)")
plt.ylabel("Density")

plt.show()
```

### 23. Hist Plot

Displays the frequency distribution of a numerical variable

![Screenshot 2025-06-09 012037](https://github.com/user-attachments/assets/9cd9ed1a-fdc3-48ed-a855-6ec8e5b95ef2)

```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the histogram plot (histplot)
# 'x' specifies the column for which to plot the distribution
plot = sns.histplot(x="total_bill", data=tips, kde=True) # kde=True adds a Kernel Density Estimate line

# Optional: Add a title and labels for clarity
plt.title("Distribution of Total Bill Amounts")
plt.xlabel("Total Bill ($)")
plt.ylabel("Count")

plt.show()
```

### 24. ECDF Plot

Assesses the probability distribution of a dataset

![Screenshot 2025-06-09 012223](https://github.com/user-attachments/assets/51ae5124-69ef-431b-a8dd-6367893186c9)

```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the ECDF plot
# ECDF (Empirical Cumulative Distribution Function) plots show the proportion of observations
# that fall below each value in a dataset.
sns.ecdfplot(x="total_bill", data=tips)

# Optional: Add a title and labels for clarity
plt.title("ECDF of Total Bill Amount")
plt.xlabel("Total Bill ($)")
plt.ylabel("Proportion")

plt.show()
```

### 25. Rug Plot

Displays individual observations along an axis

![Screenshot 2025-06-09 012425](https://github.com/user-attachments/assets/cf989d84-f97a-47ef-98e8-b13cb8c09b6f)


```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the rug plot
sns.rugplot(x="total_bill", data=tips)

# Optional: Add a title and labels for clarity
plt.title("Distribution of Total Bill Amounts (Rug Plot)")
plt.xlabel("Total Bill ($)")

plt.show()
```

### 26. Joint Plot

Displays the relationship between two variables and their marginal distributions

![Screenshot 2025-06-09 012607](https://github.com/user-attachments/assets/b5f0d65b-d864-41b0-a057-9eaedd9a642c)


```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create the joint plot
sns.jointplot(x="total_bill", y="tip", data=tips)

# Optional: Add a title (jointplot returns a JointGrid object, not an Axes object)
# plt.suptitle('Joint Plot: Total Bill vs. Tip Amount', y=1.02) # This doesn't work directly for jointplot's title

plt.show()
```

### 27. FacetGrid

Creates a grid of plots based on a dataset’s features to compare distributions

![Screenshot 2025-06-09 013004](https://github.com/user-attachments/assets/014a940e-2652-49ff-9f8d-6422a3a92eb2)

```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create a FacetGrid
# We want 'day' on the x-axis for each plot, 'total_bill' on y.
# 'col' will create separate columns for each 'time' (Lunch/Dinner).
g = sns.FacetGrid(tips, col="time", height=4, aspect=0.8)

# Map a plotting function to the FacetGrid
# Here, we're mapping sns.barplot to each subplot
g.map(sns.barplot, "day", "total_bill")

# Add titles and adjust layout
g.set_axis_labels("Day of the Week", "Total Bill ($)")
# Correct way to set titles using a template string
g.set_titles("Time: {col_name}")
g.add_legend()

# Optional: Adjust the overall title if needed
plt.suptitle('Total Bill Distribution by Day and Time (using FacetGrid)', y=1.02)

plt.show()
```

### 28. PairGrid 

Explores pairwise relationships in a dataset



```py
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create a PairGrid
# You define the variables you want to plot on the x and y axes.
g = sns.PairGrid(tips, x_vars=["smoker", "time", "day"], y_vars=["total_bill", "tip", "size"])

# Map different plot types to the upper, lower, and diagonal parts of the grid
# For example, scatter plots on the lower triangle
g.map_lower(sns.scatterplot)
# KDE plots (Kernel Density Estimate) or Histograms on the diagonal
g.map_diag(sns.histplot, kde=True)
# Boxplots or Barplots on the upper triangle
g.map_upper(sns.boxplot)

# You can also add hue to a PairGrid for coloring by a categorical variable
# g = sns.PairGrid(tips, hue="sex", x_vars=["total_bill", "tip"], y_vars=["total_bill", "tip"])
# g.map_diag(sns.histplot)
# g.map_offdiag(sns.scatterplot)
# g.add_legend()

# Optional: Add a title for the entire figure
plt.suptitle('PairGrid of Tips Dataset Features', y=1.02) # Adjust y to prevent overlap

plt.show()
```

### 29. JointGrid

Creates custom joint and marginal plot

```py
import seaborn as sns
import matplotlib.pyplot as plt

# Load the tips dataset
tips = sns.load_dataset('tips')

# Create a JointGrid instance
# We specify the data and the x, y variables
g = sns.JointGrid(data=tips, x="total_bill", y="tip")

# Plot a scatter plot on the main axes
g.plot_joint(sns.scatterplot)

# Plot histograms on the marginal axes
g.plot_marginals(sns.histplot)

# Optional: Add a title to the JointGrid
g.fig.suptitle('Joint Distribution of Total Bill and Tip', y=1.02) # y adjusts title position

plt.show()
```
