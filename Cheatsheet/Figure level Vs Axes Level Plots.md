<div align="left">
  <h1> 1. Pandas Cheatsheet - Viewing and Inspecting Data

  ## Viewing and Inspecting Data

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

### 3. Top N rows of the dataframe
It returns first n rows of the DataFrame.By default it will return first 5 rows

```py
import seaborn as sns
import pandas as pd # pandas is implicitly used by seaborn's load_dataset

# Load the titanic dataset
df = sns.load_dataset('titanic')

# Display the first 5 rows of the DataFrame
# Replace '5' with any integer 'n' to view the first 'n' rows
print(df.head(5))
```
