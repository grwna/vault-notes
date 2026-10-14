Link to Notebook: [Colab](https://colab.research.google.com/drive/1NXA7L95Pug2tpieUvnTH8RRQxhf2ijfZ)
# Pandas
Data science has 5 stages OSEMN:
- Obtain  <-- Pandas are used here (these are 80% of data analysis work, 20% is M and N)
- Scrub    <--|
- Explore < --|
- Model
- Interpret

Pandas is focused on **structured data**

## **Data Structures**
- Series (single-column)
	- Can have custom indices (series.index)
	- Can have multiindex
		- Multiindex can be unstacked, turning series into dataframe
- DataFrame
	- Can be initialized using dictionary syntax (column-rows pair), then pass to `DataFrame(dict)`
	- Made up of three elements: `values`, `index`, and `columns`
	- `pd.set_option('display.max_columns', 50)`
	- `pd.set_option('display.max_rows', 10)`

**Keywords**
- Data selection and assignment
- Extraction
- Value Sorting
- Merging
- Deletion
- Aggregation & Group operations
- Hierarchical indexing
- Handling missing values

**Useful DF Methods**
- `head()`
- `info()`
- `describe()`

## **DataFrame Basics**
- `.T` <- not a method
-  Getting a column: `df['column_name']`.
- Getting columns: `df[['column_name1', 'column_name2']]`.
- Getting rows: `df[0:3]` (index slicing).
- Data Fetching:
	- Label specification: `df.loc[row_name:column_name]`, this works like indexing/slicing.
	- Index specification: `df.iloc[rows,[columns]]`, this works like indexing/slicing.
	- Use `loc` to get data by column names
	- These return a DF or Series
- Single Element Fetching:
	- `at[row:col]`
	- `iat`
- Assigning and Replacing
	- Assigning: create a new column like adding a new key to dict, with a data object assigned as the value
	- Replacing: assign a value at a specific point, can be done using `at[]`
	- Use `replace()` for a programmatic way to replace many elements at once
![[Pasted image 20260429123921.png|600]]

**Extraction with Specific Conditions**
Example:
```python
dataset[dataset['column_name'] != 'Unknown']
dataset[(dataset['column_name'] != 'Unknown') | (dataset['column_name'] != 'Known')]
dataset[dataset['column_name'].isin(['Unknown', 'Known'])]
dataset[~dataset['column_name'].isin(['Unknown', 'Known'])]
```

**Handling of Missing Values** 
- Missing values can be extracted using `.isnull()`, which returns a boolean DF object with all NaN points as true.
- Use `isnull().sum()` to count all missing values, which are grouped by columns

**Sorting Values**
- Sort by Index: `.sort_index()`
- Sort by Value: `.sort_values(by='column_name', ascending=False/True)`
- Default is ascending

## Merging and Concatenating Data
- `pd.merge(df1, df2, ..., on='key_column', how='left/right/outer')` - SQL like joins
	- If key names are different, use `left_on` and `right_on`
- `pd.concat()` -  Stitch together along an axis
- `df.join()` - Like merge, but for 2 dataframes, joined by index
- `df.append()` - for adding rows to dataframe

**Merge**
(1) Inner join (INNER JOIN): Joins data when both have keys.
(2) Left outer join (LEFT JOIN): Joins when the data on the left side has a key.
(3) Right outer join (RIGHT JOIN): Joins when the key of the data is on the right side.
(4) Full outer join (FULL JOIN): Joins when the key exists on either side.

![[Pasted image 20260429133210.png|200]]

Based on the image, you can see some characteristics, like:
- Inner join can reduce rows
- Left Outer keeps all left data, right data can be lost
- Right is opposite of left
- Full Outer keeps rows form both intact

![[Pasted image 20260429133612.png|500]]

![[Pasted image 20260429140048.png|500]]

![[Pasted image 20260429140357.png|500]]

**Concat**
Doesn't combine, but just stack two dataframes.
By default: stack vertically (add as new rows)
```python
pd.concat([df1, df2], sort=False, ignore_index=True, axis={0/1})
```
![[Pasted image 20260429140736.png|500]]

![[Pasted image 20260429140757.png|500]]


## Manipulating and Transforming Data
**Deleting Data**
Use `.drop()`, creates a new dataframe.
```python
df.drop(index=[0,1,4], axis=0)
df.drop(['name', 'age'], axis=1)
```
Use `.reset_index()` to defragment non-sequential indices.

**Duplicated Data**
`.duplicated()`
`.drop_duplicates()`

Keep in mind the difference of Series vs DataFrame (it's not that different)

**Mapping**
You can map values using the `.map(dict)`. For example, if you have a numeric watching status column, you can add a label to these status and add it as column.
```python
status_map = {
	1: 'watching',
	2: 'dropped',
	3: 'backlog',
}
df['status_label'] = df['watching_status'].map(status_map)
```

You can also use lambda functions as map argument:
```python
anime_data_extracted['ScoreCategory'] = anime_data_extracted['Score'].map(
    lambda x: 'Low' if x < 5 else ('Average' if x <= 7 else 'High')
)
```

**Bin Splitting**
Convert continuous numerical data into categories (called bins). Use `pd.cut()` for equal range/interval or `pd.qcut()` for equal count in each bin.

```python
binning = [2,4,6,8,10]
binned = pd.cut(data['col'], binning)

# or using equal ranges automatically
binned = pd.cut(data['col'], bins=5)
# or equal counts
binned = pd.qcut(data['col'], q=5)
# the data will be divided into 5 bins, each containing the same number of elements
```

If you print it, it could come out as `(8,10]`, which means 8 is excluded, but 10 is included.
You can also add labels `pd.cut(labels=[]` to label each bin instead of using the `(]`.
use `right=False` to make the cut open interval.

>[!tip]
>Use `pd.value_counts()` to calculate the occurences of each bins (or any value for that matter).

## Aggregating Data
- `.groupby()`
- `.mean()`, `.max()`, etc.
- `.agg()`
Use `.groupby()` to group a dataset by a column's values.
```python
data = df.groupby('Type_of_transport')
data = df.groupby(['transport', 'age'])
mean_time_by_transport = data['time'].mean()

# do multiple aggregations at once
funcs = ['count', 'mean', 'max']
data.agg(funcs)
```

The method `.groupby()` is an iterator, which means you can use `for group in df.groupby()`.

**Hierarchical Grouping**
Example:
group by gender and country:

| F     | **zh** |
| ----- | ------ |
| **F** | **jp** |
| **M** | **zh** |
| **M** | **jp** |

## Handling Anomalies
**Missing Values**
A more proper and careful way to handle missing values.

Empty values can be represented by NaN, or a custom value set by the data (e.g. 'Unknown'). You can turn these custom values into NaN using `.replace('Unknown', np.nan)`.

Approaches:
- Listwise Deletion: Drop rows that contain empty value, can remove too much data.
	- `.dropna()`
- Pairwise Deletion: Ignore rows with missing values when calculating, nothing is deleted permanently. When you don't need a certain column's value, it being empty is fine.
	- `.dropna(subset=['col1', 'col2'])`
	- Aggregate functions like `mean`, `sum` ignore NaN by default
- Fill in: `.fillna(value)`: replace empty with a certain value.
	- the value to use should be carefully chosen (e.g. mean, max, min, etc.)
	- for timeseries: do not use future data to fill in past data (can use `.ffill())

**Outliers**
Use box plots to visualize data spreald (extreme values).
Approaches:
- Trimming/Capping based on bounds.
- Based on standard deviations.
Practice on many datasets to get an intuition on which approach are best.
# Summary
**Summary of Functions** 
- `pd.merge()`
- `pd.concat()`
- `pd.cut()`
- `pd.qcut()`
- `pd.value_counts()`

**Summary of Methods** 
- `.head()`
- `.info()`
- `.describe()`
- `.isin()`
- `.isnull()`
- `.join()`
- `.append()`
- `.drop()`
- `.dropna()`
- `.reset_index()`
- `.fillna()`
- `.ffill()`
- `.sort_index()`
- `.sort_values()`
- `.assign()` <- create new DataFrame
- `.groupby()` <- usually used for aggregating

**Summary of Attributes** 
- `.loc .iloc`
- `.at .iat`


>[!tip]  Conclusion
>PRACTICE, PRACTICE, PRACTICE.
