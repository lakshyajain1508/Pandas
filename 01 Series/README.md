# Topic 1: Pandas Series

# What is a Series?

A **Series** is a one-dimensional data structure in Pandas.

It stores:

- Data
- Index

Think of it like:

- A single column in Excel
- A list with labels

---

# Real Life Example

Suppose you store student marks:

| Index | Marks |
|--------|--------|
| 0 | 90 |
| 1 | 85 |
| 2 | 95 |

This is a **Series**.

---

# Creating Your First Series

```python
import pandas as pd

marks = pd.Series([90, 85, 95])

print(marks)
```

### Output

```text
0    90
1    85
2    95
dtype: int64
```

---

# Understanding Output

| Part | Meaning |
|--------|---------|
| 0, 1, 2 | Index |
| 90, 85, 95 | Values |
| dtype | Data Type |

---

# Important Point

A Series has:

1. Values
2. Indexes

Both are important.

---

# Accessing Values

## By Index

```python
print(marks[0])
```

### Output

```text
90
```

---

## Multiple Values

```python
print(marks[[0, 2]])
```

### Output

```text
0    90
2    95
```

---

# Custom Index

Instead of `0, 1, 2`, you can create your own labels.

```python
marks = pd.Series(
    [90, 85, 95],
    index=["Laksh", "Aryan", "Parth"]
)

print(marks)
```

### Output

```text
Laksh    90
Aryan    85
Parth    95
dtype: int64
```

---

# Accessing Custom Index Values

```python
print(marks["Laksh"])
```

### Output

```text
90
```

---

# Series from Dictionary

```python
data = {
    "Laksh": 90,
    "Aryan": 85,
    "Parth": 95
}

marks = pd.Series(data)

print(marks)
```

### Output

```text
Laksh    90
Aryan    85
Parth    95
dtype: int64
```

---

# Checking Data Type

```python
print(type(marks))
```

### Output

```text
<class 'pandas.core.series.Series'>
```

---

# Series Attributes

## index

Shows indexes.

```python
print(marks.index)
```

---

## values

Shows actual values.

```python
print(marks.values)
```

---

## dtype

Shows data type.

```python
print(marks.dtype)
```

---

# Series Operations

Pandas supports mathematical operations.

---

## Addition

```python
numbers = pd.Series([1, 2, 3])

print(numbers + 10)
```

### Output

```text
0    11
1    12
2    13
dtype: int64
```

---

## Multiplication

```python
print(numbers * 2)
```

### Output

```text
0    2
1    4
2    6
dtype: int64
```

---

# Filtering in Series

```python
print(numbers[numbers > 1])
```

### Output

```text
1    2
2    3
dtype: int64
```

---

# Checking Missing Values

Pandas uses **NaN** for missing values.

```python
data = pd.Series([10, 20, None, 40])

print(data)
```

### Output

```text
0    10.0
1    20.0
2     NaN
3    40.0
dtype: float64
```

---

# Detect Missing Values

```python
print(data.isnull())
```

### Output

```text
0    False
1    False
2     True
3    False
dtype: bool
```

---

# Basic Functions on Series

## sum()

```python
print(marks.sum())
```

---

## mean()

```python
print(marks.mean())
```

---

## max()

```python
print(marks.max())
```

---

## min()

```python
print(marks.min())
```

---

## count()

```python
print(marks.count())
```

---

# Sorting Series

## Sort by Values

```python
print(marks.sort_values())
```

---

## Descending Order

```python
print(marks.sort_values(ascending=False))
```

---

## Sort by Index

```python
print(marks.sort_index())
```

---

# Checking Conditions

```python
print(marks > 90)
```

### Output

```text
Laksh    False
Aryan    False
Parth     True
dtype: bool
```

---

# Real-Life Use Cases of Series

Series are used for:

- Student marks
- Product prices
- Daily temperatures
- Monthly sales
- Sensor readings

---

# Difference Between Python List and Series

| Python List | Pandas Series |
|-------------|--------------|
| No labels | Has index |
| Basic operations | Advanced operations |
| Less powerful | More powerful |
| Limited filtering | Easy filtering |

---

# Important Interview Questions

## Q1. What is a Series?

A **Series** is a one-dimensional labeled array in Pandas that stores data along with an index.

---

## Q2. Can a Series Store Mixed Data Types?

Yes, a Series can store mixed data types, but it is generally **not recommended** because it reduces performance and consistency.

Example:

```python
mixed = pd.Series([10, "Laksh", 95.5])
print(mixed)
```

---

## Q3. What is an Index in a Series?

An **Index** is a label used to identify and access values stored in a Series.

Example:

```python
marks = pd.Series(
    [90, 85, 95],
    index=["Laksh", "Aryan", "Parth"]
)

print(marks["Laksh"])
```

Output:

```text
90
```

---

# Summary

You learned:

✅ What is a Series

✅ Creating a Series

✅ Series from Lists

✅ Series from Dictionaries

✅ Custom Indexes

✅ Accessing Values

✅ Series Attributes (`index`, `values`, `dtype`)

✅ Mathematical Operations

✅ Filtering Data

✅ Missing Values (`NaN`)

✅ Basic Statistical Functions

✅ Sorting

✅ Conditions and Boolean Operations

✅ Real-World Use Cases

✅ Interview Questions

---

# Key Takeaway

A **Series** is the foundation of Pandas. Every column in a DataFrame is internally stored as a Series. Understanding Series thoroughly makes learning DataFrames, data analysis, and machine learning preprocessing much easier.