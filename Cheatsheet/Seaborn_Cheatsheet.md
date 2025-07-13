
# Seaborn - Cheatsheet for Developers

## Introduction-What-is-Seaborn?

> Seaborn is a powerful and popular Python library specifically designed for creating attractive and informative statistical graphics. Built on top of Matplotlib, it offers a higher-level interface that simplifies the process of generating complex visualizations, especially when working with Pandas DataFrames. Seaborn excels at helping users explore and understand their data by providing a wide array of specialized plot types for visualizing relationships between variables, distributions, and categorical data, often incorporating statistical estimations like regression lines or confidence intervals automatically. Its appealing default styles, color palettes, and concise syntax make it a go-to tool for data scientists and analysts seeking to effectively communicate insights from their data with minimal coding effort.


## 1. Importing Seaborn & Loading Datasets

> This section covers the initial steps of bringing the Seaborn library into your Python script and loading its convenient built-in datasets for quick exploration.

|Command | description|
|----------|-------------|
|`import seaborn as sns`|	Imports the Seaborn library, conventionally aliased as sns.|
|`import matplotlib.pyplot as plt`|	Imports Matplotlib's plotting module, often used in conjunction with Seaborn for displaying plots.|
|`import pandas as pd`|	Imports the Pandas library, essential for working with DataFrames which Seaborn typically uses.|
|`sns.load_dataset('dataset_name')`|	Loads one of Seaborn's built-in example datasets (e.g., 'tips', 'iris', 'flights') as a Pandas DataFrame.
|`pd.read_csv('file.csv')`|	(Pandas command) Loads data from a CSV file into a Pandas DataFrame, a common way to get data into Seaborn.|
|`pd.DataFrame(data_dict)`|	(Pandas command) Creates a DataFrame from a dictionary, useful for creating small sample datasets.|

## 2. Figure-Level vs. Axes-Level Plots

### Understand the key distinction between Seaborn functions that create an entire figure (Figure-level) and those that draw onto a specific part of a figure (Axes-level).

> A. Axes-Level Functions: These functions plot onto a single matplotlib.pyplot.Axes object. They are like direct replacements for Matplotlib plotting functions and return an Axes object. This makes them highly compatible with Matplotlib's object-oriented interface, allowing you to easily combine them with other Matplotlib plots on the same figure or subplot. They accept an ax= argument to specify where to draw.

> B. Figure-Level Functions: These functions are higher-level interfaces that manage their own Matplotlib figure and one or more Axes objects (often arranged in a grid like FacetGrid or JointGrid). They return a Seaborn object (e.g., FacetGrid, JointGrid) which provides methods for further customization. They are designed for quick, aesthetically pleasing plots, especially when faceting data by different categories, and do not accept an ax= argument directly.

|Command | description|
|----------|-------------|
|`sns.scatterplot(x, y, data, ax=...)`|	Axes-Level: Creates a scatter plot on a single Axes object. Returns matplotlib.axes.Axes. Accepts an ax= argument to plot on a specific subplot.|
|`sns.lineplot(x, y, data, ax=...)`|	Axes-Level: Creates a line plot on a single Axes object. Returns matplotlib.axes.Axes. Accepts an ax= argument.|
|`sns.histplot(x, data, ax=...)`|	Axes-Level: Creates a histogram on a single Axes object. Returns matplotlib.axes.Axes. Accepts an ax= argument.|
|`sns.kdeplot(x, data, ax=...)`|	Axes-Level: Creates a Kernel Density Estimate plot on a single Axes object. Returns matplotlib.axes.Axes. Accepts an ax= argument.|
|`sns.boxplot(x, y, data, ax=...)`|	Axes-Level: Creates a box plot on a single Axes object. Returns matplotlib.axes.Axes. Accepts an ax= argument.|
|`sns.barplot(x, y, data, ax=...)`|	Axes-Level: Creates a bar plot on a single Axes object. Returns matplotlib.axes.Axes. Accepts an ax= argument.|
|`sns.lmplot(x, y, data, hue=..., col=..., row=...)`|	Figure-Level: Creates a scatter plot with regression line, often faceted by hue, col, or row. Returns a FacetGrid object. Does NOT accept an ax= argument.|
|`sns.relplot(x, y, data, kind='scatter'/'line', col=..., row=...)`|	Figure-Level: Flexible function for relational plots (scatter or line), often faceted. Returns a FacetGrid object. Does NOT accept an ax= argument.|
|`sns.displot(x, data, kind='hist'/'kde'/'ecdf', col=..., row=...)`|	Figure-Level: Flexible function for distribution plots (hist, kde, ecdf), often faceted. Returns a FacetGrid object. Does NOT accept an ax= argument.|
|`sns.catplot(x, y, data, kind='box'/'violin'/..., col=..., row=...)`|	Figure-Level: Flexible function for categorical plots (box, violin, bar, etc.), often faceted. Returns a FacetGrid object. Does NOT accept an ax= argument.|
|`sns.jointplot(x, y, data, kind='scatter'/'kde'/'reg'...)`|	Figure-Level: Creates a joint plot with marginal distributions. Returns a JointGrid object. Does NOT accept an ax= argument.|
|`sns.pairplot(data, hue=...)`|	Figure-Level: Creates a grid of pairwise relationships in a dataset. Returns a PairGrid object. Does NOT accept an ax= argument.|
|`plt.subplots(rows, cols)`|	Matplotlib command used to create a Figure and a grid of Axes objects, often used with Axes-Level Seaborn functions.|
|`g.ax`|	Attribute of a FacetGrid or JointGrid object (g) to access the main Axes object within the figure-level plot for further customization using Matplotlib commands.|

## 3. Relational Plots

> Explore how to visualize the relationships between two or more variables using scatter plots and line plots.

|Command | description|
|----------|-------------|
|`sns.relplot(x, y, data, ...)`|	Figure-level function for drawing relational plots. By default, it draws a scatter plot (kind='scatter'), but it can also draw line plots (kind='line'). Highly flexible for creating multi-panel figures with col, row, hue, size, and style arguments.|
|`sns.scatterplot(x, y, data, ...)`|	Axes-level function for drawing scatter plots. Useful for showing the relationship between two continuous variables. Can map hue, size, and style to different aspects of the data.|
|`sns.lineplot(x, y, data, ...)`|	Axes-level function for drawing line plots. Ideal for showing trends or changes over time, or between two continuous variables where order matters. Can map hue, size, and style, and automatically performs aggregation (e.g., mean and confidence interval).|
|`sns.relplot(..., kind='line')`|	Specifically instructs relplot to draw line plots instead of scatter plots across its facets.|
|`hue='column_name'`|	In relplot, scatterplot, or lineplot, assigns different colors to data points/lines based on the categorical values in column_name.|
|`size='column_name'`|	In relplot, scatterplot, or lineplot, varies the size of markers/lines based on the values in column_name.|
|`style='column_name'`|	In relplot, scatterplot, or lineplot, varies the marker style (for scatter) or line style (for line) based on the categorical values in column_name.|
|`col='column_name'`|	In relplot, creates separate columns of plots for each unique value in column_name.|
|`row='column_name'`|	In relplot, creates separate rows of plots for each unique value in column_name.|
|`markers=True`|	In lineplot, adds markers to the data points along the lines.|
|`dashes=False`|	In lineplot, draws solid lines rather than dashed lines when style is used.|
|`errorbar='sd'`|	In lineplot, shows standard deviation as the error band around the line (default is 95% confidence interval). Other options include 'se' (standard error), or None to remove it.|

## 4. Distribution Plots

> Learn to depict the spread and frequency of single or multiple variables, including histograms, kernel density estimates, and empirical cumulative distributions.

|Command | description|
|----------|-------------|
|`sns.histplot(data=df, x='column_name')`|	Plots a histogram showing the distribution of a single numerical variable. Can include y for 2D histograms, hue for categories, kde=True for density curve.|
|`sns.kdeplot(data=df, x='column_name')`|	Plots a Kernel Density Estimate (KDE) to visualize the probability density of a numerical variable. Can use y for 2D KDEs, hue for categories, fill=True to shade the area.|
|`sns.displot(data=df, x='column_name', kind='hist')`|	A figure-level function that provides a flexible interface to draw various types of distribution plots (histogram, KDE, ECDF) with optional faceting (col, row). kind='hist' for histogram.|
|`sns.displot(data=df, x='column_name', kind='kde')`|	A figure-level function for KDE plots with faceting options. kind='kde' for KDE.|
|`sns.displot(data=df, x='column_name', kind='ecdf')`|	A figure-level function for Empirical Cumulative Distribution Function (ECDF) plots. Shows the proportion of observations less than or equal to a value.|
|`sns.rugplot(data=df, x='column_name')`|	Draws a "rug" plot, which is a series of small vertical lines at each data point along an axis, indicating the distribution. Often used as an addition to other distribution plots.|
|`sns.ecdfplot(data=df, x='column_name')`|	Plots the Empirical Cumulative Distribution Function (ECDF) of a variable. Similar to displot(kind='ecdf') but is an axes-level function.|
|`sns.boxplot(data=df, x='category_col', y='numeric_col')`|	While often used for categorical data, box plots also show the distribution (median, quartiles, outliers) of a numerical variable broken down by categories.|
|`sns.violinplot(data=df, x='category_col', y='numeric_col')`|	Similar to box plots, but also shows the kernel density estimation of the underlying distribution, providing more insight into the shape.|

## 5. Categorical Plots

> Discover various plot types specifically designed to visualize data across different categories, such as bar plots, box plots, violin plots, and swarm plots.

|Command | description|
|----------|-------------|
|`sns.catplot(x, y, data, kind='strip')`|	A figure-level function that provides a unified interface to several categorical plots. The kind parameter determines the specific plot type (e.g., 'strip', 'swarm', 'box', 'violin', 'boxen', 'point', 'bar', 'count'). Supports col, row, hue for creating grids.|
|`sns.stripplot(x, y, data)`|	Draws a scatter plot where one variable is categorical. It helps visualize the distribution of points within categories, with points "jittered" to avoid overlap.|
|`sns.swarmplot(x, y, data)`|	Similar to stripplot, but adjusts the points along the categorical axis so that they don't overlap, providing a better representation of density.|
|`sns.boxplot(x, y, data)`|	Displays the distribution of quantitative data in a way that facilitates comparisons between categorical variables. Shows quartiles, outliers, and median.|
|`sns.violinplot(x, y, data)`|	Combines aspects of a box plot with a kernel density estimation, showing the probability density of the data at different values.|
|`sns.boxenplot(x, y, data)`|	(Also known as letter-value plot) Similar to a box plot but designed to show more information about the shape of the distribution, particularly for larger datasets.|
|`sns.barplot(x, y, data)`|	Represents the mean (or other estimator) of a numerical variable for each category, along with a confidence interval.|
|`sns.countplot(x, data)`|	Shows the counts of observations in each category using bars. It's essentially a bar plot where the height of the bars corresponds to the number of occurrences.|
|`sns.pointplot(x, y, data)`|	Displays the estimate of a quantitative variable for each category, along with confidence intervals, typically using points and connecting lines. Useful for showing interactions.|

## 6. Regression Plots

> Utilize these plots to visualize linear relationships between variables, often including regression lines and confidence intervals.

|Command | description|
|----------|-------------|
|`sns.regplot(x="feature", y="target", data=df)`|	Plots a scatterplot of x and y with a linear regression model fit. Ideal for visualizing a single relationship between two variables.|
|`sns.lmplot(x="feature", y="target", data=df, hue="category_col")`|	Creates a multi-panel plot (a FacetGrid) where regplot is used for each facet. Excellent for exploring conditional relationships (e.g., how the regression differs across categories defined by hue).|
|`sns.lmplot(x="feature", y="target", data=df, order=2)`|	Fits a polynomial regression model of the specified order (e.g., order=2 for quadratic). Applicable to both regplot and lmplot.|
|`sns.lmplot(x="feature", y="target", data=df, x_estimator=np.mean)`|	Plots conditional means and confidence intervals, rather than individual data points, for x values. Useful when x is categorical or has many overlapping points.|
|`sns.lmplot(x="feature", y="target", data=df, ci=None)`|	Hides the confidence interval around the regression line. By default, it's a 95% confidence interval.|
|`sns.lmplot(x="feature", y="target", data=df, scatter=False)`|	Plots only the regression line and its confidence interval, without the individual scatter points.|
|`sns.residplot(x="feature", y="target", data=df)`|	Plots the residuals of a simple regression model. Useful for checking assumptions of linear regression (e.g., homoscedasticity).|

## 7. Multi-Plot Grids

> Master the creation of grids of plots that display different subsets of your data or different facets of a single relationship.

|Command | description|
|----------|-------------|
|`sns.FacetGrid(data, col='col_name', row='row_name', ...)`|	Creates a multi-plot grid for plotting conditional relationships. col and row define the variables to form the grid.|
|`g.map(plt.scatter, 'x_col', 'y_col')`|	Maps a plotting function (e.g., plt.scatter, sns.histplot) to each facet of the FacetGrid (g).|
|`g.add_legend()`|	Adds a legend to the FacetGrid if hue was used in map.|
|`sns.PairGrid(data, vars=['col1', 'col2'], hue='hue_col')`|	Creates a grid of subplots for visualizing pairwise relationships in a dataset.|
|`g.map_upper(sns.scatterplot)`|	Maps a plotting function to the upper triangle of the PairGrid.|
|`g.map_lower(sns.kdeplot)`|	Maps a plotting function to the lower triangle of the PairGrid.|
|`g.map_diag(sns.histplot)`|	Maps a plotting function to the diagonal plots of the PairGrid.|
|`sns.jointplot(x='x_col', y='y_col', data=df, kind='scatter')`|	Draws a plot of two variables with bivariate and univariate graphs. kind can be 'scatter', 'kde', 'hist', 'hex', 'reg', 'resid'.|
|`sns.jointplot(x='x_col', y='y_col', data=df, kind='kde')`|	Specific jointplot for kernel density estimate.|
|`g = sns.JointGrid(data, x='x_col', y='y_col') <br> g.plot_joint(sns.scatterplot) <br> g.plot_marginals(sns.histplot)`|	Provides more fine-grained control over a joint plot by creating a JointGrid object and then mapping functions to its joint and marginal axes separately.|
|`sns.relplot(x='x_col', y='y_col', data=df, kind='scatter', col='col_name')`|	A figure-level function for relational plots that can draw multiple subplots (facets) based on categorical variables using col, row, or col_wrap. kind can be 'scatter' or 'line'.|
|`sns.displot(data=df, x='col_name', kind='hist', col='col_name')`|	A figure-level function for distribution plots that can draw multiple subplots (facets) based on categorical variables. kind can be 'hist', 'kde', or 'ecdf'.|
|`sns.catplot(x='x_col', y='y_col', data=df, kind='bar', col='col_name')`|	A figure-level function for categorical plots that can draw multiple subplots (facets) based on categorical variables. kind can be 'strip', 'swarm', 'box', 'violin', 'boxen', 'point', 'bar', or 'count'.|
|`sns.lmplot(x='x_col', y='y_col', data=df, hue='hue_col', col='col_name')`|	A figure-level function for drawing linear models on FacetGrids.|
|`g.set_axis_labels('X Label', 'Y Label')`|	Sets the x and y axis labels for all facets in a FacetGrid or PairGrid.|
|`g.set_titles(col_template='{col_name} Value')`|	Customizes the titles of the individual facets in a FacetGrid or PairGrid.|

## 8. Styling and Color Palettes

> Customize the aesthetic appeal of your plots by applying various themes, styles, and predefined or custom color schemes.

|Command | description|
|----------|-------------|
|`sns.set_theme()`|	Sets the overall aesthetic style of the plots (e.g., 'darkgrid', 'whitegrid', 'dark', 'white', 'ticks').|
|`sns.set_style('darkgrid')`|	Sets the matplotlib style parameters. Can be 'darkgrid', 'whitegrid', 'dark', 'white', 'ticks'.|
|`sns.axes_style('white')`|	Temporarily sets the style for a specific block of code or figure context.|
|`sns.set_palette('viridis')`|	Sets the default color palette for all plots. Can be a Matplotlib colormap name or a Seaborn palette name.|
|`sns.color_palette('pastel')`|	Returns a list of colors from a named palette. Useful for custom coloring.|
|`sns.color_palette("rocket", as_cmap=True)`|	Returns a colormap object for sequential data (e.g., for heatmaps).|
|`sns.dark_palette("purple")`|	Generates a sequential palette for quantitative data, starting from a light color and progressing to a dark color.|
|`sns.light_palette("green")`|	Generates a sequential palette for quantitative data, starting from a dark color and progressing to a light color.|
|`sns.diverging_palette(220, 20, as_cmap=True)`|	Generates a diverging palette for data with a meaningful midpoint, with two distinct colors on either side.|
|`sns.set_context('notebook')`|	Adjusts plot elements to scale appropriately for different contexts (e.g., 'paper', 'notebook', 'talk', 'poster').|
|`sns.despine()`|	Removes the top and right spines from plots. Useful for a cleaner aesthetic.|
|`plt.rc(group, **kwargs)`|	(Matplotlib function often used with Seaborn) Allows granular control over various Matplotlib parameters like font sizes.|

## 9. Customizing Plot Elements

> Learn to fine-tune individual components of your plots, such as axis labels, titles, and legends, often by interacting with the underlying Matplotlib objects.

|Command | description|
|----------|-------------|
|`sns.set_style('whitegrid')`|	Sets the aesthetic style of the plots. Options include 'darkgrid', 'whitegrid', 'dark', 'white', 'ticks'.|
|`sns.set_palette('viridis')`|	Sets the default color palette for all plots. Accepts a palette name (e.g., 'deep', 'muted', 'pastel'), a Matplotlib colormap (e.g., 'viridis', 'plasma'), or a list of colors.|
|`sns.despine(left=True, bottom=True)`|	Removes the top and right spines (borders) from the plot. Can remove left or bottom spines as well.|
|`plt.figure(figsize=(width, height))`|	Creates a new Matplotlib figure with specified width and height in inches. Useful for controlling overall plot size.|
|`ax.set_xlim(min_val, max_val)`|	Sets the limits for the x-axis of a specific Axes object.|
|`ax.set_ylim(min_val, max_val)`|	Sets the limits for the y-axis of a specific Axes object.|
|`ax.set(xlabel='New X Label', ylabel='New Y Label', title='New Title')`|	A convenient method to set multiple Axes properties at once.|
|`sns.set_context('notebook')`|	Sets the plotting context parameters (font size, line width, etc.) for different presentation needs. Options: 'paper', 'notebook', 'talk', 'poster'.|
|`ax.tick_params(axis='x', rotation=45)`|	Customizes tick parameters on a specific axis, e.g., rotating labels.|
|`ax.legend(loc='best', frameon=False)`|	Customizes the legend, e.g., its location (loc) or whether it has a frame (frameon).|
|`sns.FacetGrid(...), g.set_axis_labels(...)`|	When working with FacetGrid (from relplot, catplot, displot), this sets common axis labels for all facets.|
|`sns.FacetGrid(...), g.set_titles(col_template='{col_name}')`|	Sets titles for individual subplots in a FacetGrid based on column/row names.|
|`plt.tight_layout()`|	Automatically adjusts plot parameters for a tight layout, preventing labels from overlapping.|

## 10. Statistical Estimates and Aggregation

> Understand how Seaborn automatically calculates and displays statistical summaries like means, medians, or confidence intervals within your visualizations.

|Command | description|
|----------|-------------|
|`sns.barplot(..., estimator=np.mean)`|	Plots the mean (default estimator) of a quantitative variable for each category of a qualitative variable, with confidence intervals. You can specify a different estimator function (e.g., np.median, np.std, len).|
|`sns.pointplot(..., estimator=np.mean)`|	Shows point estimates and confidence intervals using scatter plot markers and lines. Similar to barplot but emphasizes the central tendency and its uncertainty.|
|`sns.countplot(x='category_col', data=df)`|	Shows the counts of observations in each category using bars. Effectively a histogram for categorical data.|
|`sns.lmplot(..., x_estimator=np.mean)`|	Plots a regression line and confidence interval for y as a function of x. x_estimator allows plotting the mean of x at each y value when x is discrete.|
|`sns.relplot(..., kind='line', errorbar='sd')`|	For line plots, errorbar controls the visualization of statistical uncertainty. 'sd' shows standard deviation, 'se' shows standard error, or you can pass a custom function.|
|`sns.histplot(..., stat='density')`|	For histograms, stat controls the normalization of the histogram bars. 'count' (default), 'frequency', 'density', 'probability'.|
|`sns.kdeplot(..., cut=0)`|	For Kernel Density Estimates, cut extends the density beyond the extreme data points. cut=0 means it stops at the data range.|
|`sns.regplot(..., ci=95)`|	Plots a regression line. ci specifies the size of the confidence interval (e.g., 95% is default) around the regression estimate. Set ci=None to remove it.|
|`sns.jointplot(..., kind='reg')`|	Combines a scatter plot with marginal histograms, and can add a regression line with confidence interval to the joint plot.|
|`sns.catplot(..., kind='bar', errorbar='sd')`|	A figure-level function for categorical plots that can use errorbar to show statistical estimates (e.g., standard deviation).|
|`sns.boxplot(..., showmeans=True)`|	Shows the distribution using quartiles. showmeans=True adds a marker for the mean.|
|`sns.violinplot(..., inner='quartile')`|	Shows the distribution and KDE. inner can display 'box', 'quartile', 'point', or 'stick' to show statistical estimates within the violins.|

## 11. Saving Plots

> Find out how to export your high-quality Seaborn figures to various file formats for presentations or publications.

|Command | description|
|----------|-------------|
|`plt.savefig('my_plot.png')`|	Saves the current figure to a file. The file format is inferred from the extension (e.g., .png, .jpg, .pdf, .svg).|
|`plt.savefig('my_plot.pdf', dpi=300)`|	Saves the figure with a specified resolution (dots per inch). Higher dpi means better quality but larger file size.|
|`plt.savefig('my_plot.svg', format='svg')`|	Saves the figure in a specific format explicitly, which is useful for vector graphics.|
|`plt.savefig('my_plot.png', bbox_inches='tight')`|	Saves the figure by automatically trimming whitespace around the plot.|
|`plt.savefig('my_plot.png', transparent=True)`|	Saves the figure with a transparent background.|
|`g.savefig('my_facet_plot.png')`|	If you create a figure-level plot (like sns.relplot, sns.displot, sns.catplot, sns.lmplot, sns.jointplot, sns.pairplot), the returned object g has its own savefig method.|
|`g.figure.savefig('my_grid_plot.png')`|	Alternatively, for figure-level plots, you can access the underlying Matplotlib Figure object via g.figure and then use its savefig method.|
