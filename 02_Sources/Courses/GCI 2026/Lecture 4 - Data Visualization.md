> [!caution]
> This lecture is an infodump. It is better to read the notebook directly than to summarize:
> [Collab](https://colab.research.google.com/drive/1YMQ91xbv1OIsQgOnAIeNyH2BoNbS0bBb?usp=sharing)
> 
> Prioritize being able to read plot codes, writing is not as important with the help of AI.


**Data Exploration** a.k.a **Exploratory Data Analysis**
- Spot patterns, biases, and trends
- For this lecture, we focus on speed and iteratively making plots to spot patterns, not to make good/presentable plots.
- Matplotlib (pyplot, simplified), Seaborn

# Understanding Data
- %matplotlib inline <-- specific for jupyter
- data stored as integers can mean categories instead of numeric.

# Plotting
## Plotting Basics
- `plt.plot(df['col'])` <- prepare plot
- `plt.show()` <- draw plot
- How to make good plots (the plot below is hard to interpret)
![[Pasted image 20260508204054.png|300]]
- A good graph should:
	- Clearly answer a question
	- Be easy to interpret
	- Avoid unnecessary clutter
	- Accurately represent the data
	- Guide the viewer's attention to what matters
- Start by creating questions to answer. (e.g. does bad weather affect customer count?)
- A better plot:
![[Pasted image 20260508204401.png|400]]
```python
plt.figure(figsize=(10, 5))

plt.plot(df["cnt"])
plt.title("Daily Bike Rentals Over Time")
plt.xlabel("Day Index")
plt.ylabel("Total Rentals (cnt)")
plt.grid(True)

plt.show()
```


## Matplotlib Basics: One Variable
**Plot Lines**
- Gives fine grained controls for:
	- Plot types
	- labels - `plt.x/ylabel` 
	- Titles - `plt.title`
	- Colors
	- Legends  - `plt.legend()` -> show plot legend
	- Figure size - `figsize(width, height)`
	- Layout
	- Use `grid()` to show grid lines

- A figure is a canvas, one figure can have multiple plots
	- `plt.subplot(2, 3, 1)` - 2 rows, 3 columns, at first index (1) 
	- Index order:
	![[Pasted image 20260508205446.png|300]]
	- Differentiate between subplots (many plots in one figure) and Plotting multiple lines
	- To create multiple plots in one figure, simply use `plt.plot` (or other methods depending on plot type). Then call `plt.show()` only once.
- Pyplot operates as a state machine.
- From the example plots before, there are many outliers, can reduce it by plotting averages (or other aggregate measures).

**Histogram**
- `plt.hist(df['col'], bins=10, edgecolor='black')`
- Can add labels, etc. as usual
- You can use a list of ranges as bins, as well as `np.arange`
	- Adjust bins so you can extract data better/easier
	
![[Pasted image 20260508215403.png|200]]
- Use `range` parameter to adjust how much of the data (in range) to plot.

**Boxplot**
![[Pasted image 20260510222648.png|300]]
- Middle line is median
	- Data is symmteric if median is at the middle of box
	- Positive (Right) Skew
	- Negative (Left) Skew
- Box is the IQR
	- Either ends of the box are 25th and 75th percentile
	- Inside the box is middle 50% of data
	- Bigger box means data vary a lot
- Whiskers are range of typical values
- Dots beyond the whiskers are outliers
- `plt.boxplot(df['col1','col2'], vert=Bool, patch_artist=Bool)`

## Two Variables: Numeric vs Numeric
**Scatter Plots**
- `plt.scatter(df['col1], df['col2'], alpha=float)`
- Draws dots with (x,y) coordinates according to data values.
- You can see relationship/correlations with this

**Bubble Chart**
- `plt.scatter(s=bubble_size)`
- Like scatter plot, but each marker has a size, which represents a third variable
- The size are numeric values from a certain other columns
	- Might have to adjust the data's value size to scale bubble sizes

## Two Variables: Categoric vs Numeric
**Bar Chart**
- `plt.bar(x, y)`
- `plt.barh(x,y)` <- horizontal
- Multiple categories (side-by-side): 
	- `plt.bar(x - width/2, casual_avg.values, width, label="Casual")`
	- `plt.bar(x + width/2, registered_avg.values, width, label="Registered")`
**Stacked Bar Chart**
![[Pasted image 20260519125407.png|300]]
- `plt.bar(x, casual_avg, label="Casual")`
- `plt.bar(x, registered_avg, bottom=casual_avg, label="Registered")`

**Pie Charts**
- `plt.pie()`
- pie charts are controversial (harder to read differences between elements)
- The parameters are a little difficult:
![[Pasted image 20260519130454.png|400]]


## Seaborn
- Seaborn is high level compared to pyplot.
	- Automatically split, process data, add legend, etc. 
- Seaborn integrates easily with pyplot.
- `hue=feature` parameter <- the different cat features, separated with color.

## Correlation Analysis and Heatmaps
- Correlation can be positive, neutral, negative.
- `sns.heatmap(df.corr())` - there are many other parameters
- Limitations:
	- Only for linear relationships
	- Can be influenced by outliers

## Regression and Trend Analysis
- `sns.regplot()`
- `sns.lmplot(hue=)` - add a third categorical feature to compare

## Types of Plots
Visualizations are divided into multiple types:
- By features: (1 or multiple)
- By data (numerical or quantitative)
**One Variable**
- Line plots -> good for timeseries
- Histogram -> data distribution
- Boxplot -> detect spread
**Two Variable Numeric**
- Scatter Plot -> correlation
- Bubble Chart -> correlation extra
**Two Variables Cat vs Num**
- Bar Chart -> Like line plots, but for categories (one of the axes is limited to only a few)


# Summary 
> [!tip]
> In Colab, you can run `?plt.hist` or `help(plt.hist)` (or any other methods) to see help.

- Add label to plot type (as parameter) to use for legends
- 

**Pyplot**
- `plt.plot()`
- `plt.title()`
- `plt.figure(figsize())`
- `plt.xlabel()`, `plt.ylabel()`
- `plt.grid()`
- `plt.show()`
- `plt.xticks(rotation=)`, `plt.yticks()`
- `plt.hist()`
- `plt.tight_layout()` <- makes layouts more readable

**Seaborn**
- `sns.barplot()`
- `sns.scatterplot()`
- `sns.boxplot()`
- `sns.heatmap(data=df.corr())`
- `sns.regplot()`

**Pands**
- `df.rolling(window=)`
- `plt.yticks()`