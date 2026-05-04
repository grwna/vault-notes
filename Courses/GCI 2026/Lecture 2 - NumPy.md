Link to notebook: [Colab](https://colab.research.google.com/drive/1svWRLsRZG_C9xAU-u4yiE83RfCYIvKDG)

**Attendance Survey:**
In this lecture, I learned a few new things about NumPy as well as reviewing some concepts that I've previously have learned. NumPy is used over native python list because of it's speed and convenience. NumPy is written in C which makes the calculations faster than those written natively in Python. Concepts such as Ufuncs also make using numpy way easier than python list since you don't need to write loops to do operations on every element. I also learned about 1D and multidimensional numpy arrays, their uses, and operations that can be done with them.

**Topic**: Data Manipulation using NumPy

## N-D Arrays
### 1D Array 
Advantage of numpy.ndarray over python list:
- Homogenous data types
- Efficient handling of multi-dimension using axes
- Universial functions (ufunc), perform element wise operations with one call

**Comparison Operators**
Operators like `==`, `<`, etc. returns a new np.array of boolean for each element-wise comparison.

**Broadcasting**
Automatically adjust shapes so element wise operations can be performed. Example:
`a + 3`, here, 3 will be extended into an array of with `a`'s dimensions. Note that automatic broadcasting only works for scalars.

**Fancy Indexing**
In np, you can index using an array to return an array  containing the indexed number.
```python
a = np.array(11,12,13,14,15)
print(a[[0, 2, 4]])
# output
# [11, 13, 15]
```

**Interval Slicing**
```python
a[1:4:2]
# From index 1 to index 7, take every 2 element
# [12, 14]
```
Also, omitted indices in slices like `a[:7]`, means the non-omitted index is used, and the omitted part goes to the extremes (start/end). You can omit the start, end, or step.
All of these are valid
- `a[::2]`
- `a[:7:]`
- `a[1::2]`
- `a[1:]`
>[!tip]
>End index are usually exclusive

**Boolean Indexing**
You can use boolean operators for indexing.
```python
jan_prcp_no_missing = jan_prcp[jan_prcp < 999.9
cold_and_not_rainy = (jan_tmax < -10) & (jan_prcp == 0
```
Uses `&, |, ~`


### 2D & Multi-D Arrays 
- Multidimensional arrays can also be calculated easily using ufunc.
- Broadcasting also applies for scalars, aswell as 1D array with matching dimension.
	- Broadcasting can be done for left operand or right operand or both, depending on the dimensions operated.
- Aggregation can work on specific axes or the entire multi-d arrays
- Indexing can be done with respect to certain axes
	- `a[[0,2][1,3]]` gets the elements at (0,1) and (2,3) - this is not switched up!
	- Notice how the indices are paired by axis, not coordinates.
	- Learn the usage of `np.ix_`
	- Boolean indexing returns a 1D array
- Slicing works similarly, with respect to indexing rules


**Axis** 
- 0 represents rows
- 1 represents columns 