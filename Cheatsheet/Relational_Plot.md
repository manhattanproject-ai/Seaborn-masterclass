<div align="left">
  <h1> 1. Seaborn  Cheatsheet - Relational Plots

  ## Relational Plots

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

### 3. sns.relplot(..., kind='line')
Specifically instructs relplot to draw line plots instead of scatter plots across its facets.

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Needed to display the plot

# Load the titanic dataset
df = sns.load_dataset('titanic')

# Prepare data for the line plot
# Let's visualize the survival rate across different passenger classes.
# 'pclass' is an ordered categorical variable, suitable for an x-axis in a line plot.
# We'll calculate the mean of 'survived' (0 for died, 1 for survived) grouped by 'pclass'
# to get the survival rate for each class.
survival_rate_by_class = df.groupby('pclass')['survived'].mean().reset_index()
survival_rate_by_class.rename(columns={'survived': 'survival_rate'}, inplace=True)

# Create the line plot using sns.relplot with kind='line'
sns.relplot(x='pclass', y='survival_rate', kind='line', data=survival_rate_by_class)

# Optional: Add titles and labels for clarity
plt.title("Survival Rate by Passenger Class")
plt.xlabel("Passenger Class")
plt.ylabel("Survival Rate")
plt.xticks(survival_rate_by_class['pclass']) # Ensure x-axis ticks are distinct classes

# Show the plot
plt.show()
```

### 4. hue='column_name'
In relplot, scatterplot, or lineplot, assigns different colors to data points/lines based on the categorical values in column_name.

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Needed for plot display settings, though not explicitly plt.show() as per instruction

# Load the titanic dataset
df = sns.load_dataset('titanic')

# --- Example for relplot with hue ---
print("\n# --- Example for relplot with hue ---")
# Using 'age' on x-axis, 'fare' on y-axis, and 'sex' to differentiate points by color
sns.relplot(x="age", y="fare", hue="sex", data=df)
plt.title("Relationship between Age and Fare, colored by Sex (relplot)") # Add title for clarity
plt.tight_layout() # Adjust layout to prevent labels overlapping
plt.show()

# --- Example for scatterplot with hue ---
print("\n# --- Example for scatterplot with hue ---")
# Using 'age' on x-axis, 'fare' on y-axis, and 'pclass' to differentiate points by color
sns.scatterplot(x="age", y="fare", hue="pclass", data=df)
plt.title("Relationship between Age and Fare, colored by Passenger Class (scatterplot)")
plt.tight_layout()
plt.show()

# --- Example for lineplot with hue ---
print("\n# --- Example for lineplot with hue ---")
# For lineplot, it's common to aggregate data first to show trends.
# Let's find the mean age per passenger class, separated by sex.
df_agg = df.groupby(['pclass', 'sex'], as_index=False)['age'].mean()

# Using 'pclass' on x-axis, mean 'age' on y-axis, and 'sex' to differentiate lines by color
sns.lineplot(x="pclass", y="age", hue="sex", data=df_agg)
plt.title("Mean Age per Passenger Class, differentiated by Sex (lineplot)")
plt.xlabel("Passenger Class")
plt.ylabel("Mean Age")
plt.tight_layout()
plt.show()
```

### 5. size='column_name'
In relplot, scatterplot, or lineplot, varies the size of markers/lines based on the values in column_name.

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Import for displaying plots

# Load the titanic dataset
df = sns.load_dataset('titanic')

print("\n--- Example with relplot(size='fare') ---")
# relplot creates a FacetGrid, allowing for complex multi-plot figures.
# Here, 'size' will map the 'fare' values to the size of the points.
sns.relplot(x="age", y="fare", size="fare", data=df, kind="scatter", height=5, aspect=1.2)
plt.suptitle("relplot: Age vs Fare, with Point Size by Fare", y=1.02) # Adjust suptitle position
plt.show()

print("\n--- Example with scatterplot(size='fare') ---")
# scatterplot directly creates a scatter plot on the current axes.
# 'size' will map the 'fare' values to the size of the points.
plt.figure(figsize=(8, 6))
sns.scatterplot(x="age", y="fare", size="fare", data=df, sizes=(20, 400)) # Adjust point size range
plt.title("scatterplot: Age vs Fare, with Point Size by Fare")
plt.xlabel("Age")
plt.ylabel("Fare")
plt.show()

print("\n--- Example with lineplot(size='pclass') ---")
# For lineplot, 'size' typically maps to the line thickness and is often used with categorical variables.
# It will draw separate lines for each 'pclass', with varying thickness.
plt.figure(figsize=(10, 6))
sns.lineplot(x="age", y="fare", size="pclass", data=df, estimator=None, errorbar=None, hue="pclass")
# estimator=None plots each individual observation. errorbar=None removes confidence intervals.
# hue="pclass" is added to differentiate lines by color in addition to size.
plt.title("lineplot: Age vs Fare, with Line Thickness by Pclass")
plt.xlabel("Age")
plt.ylabel("Fare")
plt.show()
```

### 6. style='column_name'
In relplot, scatterplot, or lineplot, varies the marker style (for scatter) or line style (for line) based on the categorical values in column_name.

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Import for displaying plots

# Load the titanic dataset
df = sns.load_dataset('titanic')

print("\n--- Example: style='column_name' in `seaborn.relplot` ---")
# relplot creates a FacetGrid and can draw different kinds of relational plots
# Here, 'sex' will determine the style (e.g., marker shape or dash style) of the points.
sns.relplot(x="age", y="fare", hue="pclass", style="sex", data=df)
plt.suptitle("relplot: Age vs Fare by Pclass (Hue) and Sex (Style)", y=1.02) # Add a title above the plot
plt.show()

print("\n--- Example: style='column_name' in `seaborn.scatterplot` ---")
# scatterplot directly plots points.
# 'sex' will determine the style (e.g., marker shape) of the points.
plt.figure(figsize=(8, 6)) # Create a figure to control plot size
sns.scatterplot(x="age", y="fare", hue="who", style="sex", data=df)
plt.title("scatterplot: Age vs Fare by Who (Hue) and Sex (Style)")
plt.show()


print("\n--- Example: style='column_name' in `seaborn.lineplot` ---")
# lineplot draws lines connecting data points.
# 'pclass' will determine the style (e.g., line dash/marker) of the lines.
# We'll plot 'age' vs 'fare' with 'pclass' defining the lines, often with an aggregated y-axis.
plt.figure(figsize=(10, 6))
# For lineplot, 'style' will often result in different dash styles or marker types for each level.
# We'll aggregate by 'age' and show the mean 'fare' for each 'pclass'.
sns.lineplot(x="age", y="fare", hue="pclass", style="pclass", data=df, errorbar=None, estimator='mean') # errorbar=None for simplicity
plt.title("lineplot: Mean Fare by Age and Pclass (Style)")
plt.show()
```

### 7. col='column_name'
In relplot, creates separate columns of plots for each unique value in column_name.

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Needed for plotting

# Load the titanic dataset
df = sns.load_dataset('titanic')

# Generate a relational plot using 'age' on the x-axis, 'fare' on the y-axis,
# and separate columns for each 'sex' (male/female).
sns.relplot(x='age', y='fare', col='sex', data=df)

plt.show() # Display the plot
```

### 8. row='column_name'
In relplot, creates separate rows of plots for each unique value in column_name.

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Required to display the plot

# Load the titanic dataset
df = sns.load_dataset('titanic')

# Generate a scatter plot using relplot, separating plots by 'survived' status
# 'row' creates separate subplots for each unique value in the specified column
sns.relplot(x='age', y='fare', row='survived', data=df, kind='scatter', height=3, aspect=1.5)

# Optional: Add a title for clarity
plt.suptitle("Age vs. Fare by Survival Status", y=1.02) # Adjust y to prevent overlap with subplots

plt.show()
```

### 9. markers=True
In lineplot, adds markers to the data points along the lines.

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Required for displaying the plot

# Load the titanic dataset
df = sns.load_dataset('titanic')

# Generate a line plot with markers=True
# We'll plot the mean age for each passenger class, showing markers at each point.
# Seaborn's lineplot automatically calculates the mean of 'age' for each 'pclass' by default.
sns.lineplot(x="pclass", y="age", data=df, markers=True)

# Optional: Add a title and labels for clarity
plt.title("Mean Age by Passenger Class with Markers")
plt.xlabel("Passenger Class")
plt.ylabel("Mean Age")

plt.show()
```

### 10. dashes=False
In lineplot, draws solid lines rather than dashed lines when style is used.

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Required to display the plot

# Load the titanic dataset
df = sns.load_dataset('titanic')

# Generate a line plot demonstrating dashes=False
# We'll plot the average age per passenger class, separated by sex, without line dashes.
sns.lineplot(x="class", y="age", hue="sex", data=df, dashes=False)

# Optional: Add a title and labels for clarity
plt.title("Average Age by Passenger Class and Sex (No Dashes)")
plt.xlabel("Passenger Class")
plt.ylabel("Average Age")

plt.show()
```

### 11. errorbar='sd'
In lineplot, shows standard deviation as the error band around the line (default is 95% confidence interval). Other options include 'se' (standard error), or None to remove it.

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset
import matplotlib.pyplot as plt # Matplotlib is needed to show the plot

# Load the titanic dataset
df = sns.load_dataset('titanic')

# Create a line plot showing the survival rate by passenger class,
# with the standard deviation as the error bar.
# 'pclass' (passenger class) serves as an ordinal x-axis.
# 'survived' (0 for died, 1 for survived) will have its mean calculated for y,
# representing the survival rate.
sns.lineplot(x="pclass", y="survived", data=df, errorbar='sd')

# Optional: Add titles and labels for clarity if you were to show the plot
plt.title("Survival Rate by Passenger Class with Standard Deviation")
plt.xlabel("Passenger Class")
plt.ylabel("Survival Rate")
plt.show()

```



