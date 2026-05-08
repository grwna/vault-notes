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

### Types of Plots
- Line plots -> good for timeseries

## Matplotlib Basics: One Variable
- Gives fine grained controls for:
	- Plot types
	- labels - `plt.x/ylabel` 
	- Titles - `plt.title`
	- Colors
	- Legends  - `plt.legend()`
	- Figure size - `figsize(width, height)`
	- Layout
	- Use `grid()` to show grid lines

- A figure is a canvas, one figure can have multiple plots
	- `plt.subplot(2, 3, 1)` - 2 rows, 3 columns, at first index (1) 
	- Index order:
	![[Pasted image 20260508205446.png|300]]
	- Differentiate between subplots (many plots in one figure) and Plotting multiple lines
- Pyplot operates as a state machine.

# Summary 
- `plt.plot()`
- `plt.title()`
- `plt.figure(figsize())`
- `plt.xlabel()`, `plt.ylabel()`
- `plt.grid()`
- `plt.show()`
- `plt.xticks(rotation=)`, `plt.yticks()`

- `plt.yticks()`