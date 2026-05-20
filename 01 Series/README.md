# Topic 1: Pandas Series

# What is a Series?

A **Series** is a one-dimensional data structure in Pandas.

It stores:

* Data
* Index

Think of it like:

* A single column in Excel
* A list with labels

---

# Real Life Example

Suppose you store student marks:

| Index | Marks |
| ----- | ----- |
| 0     | 90    |
| 1     | 85    |
| 2     | 95    |

This is a Series.

---

# Creating Your First Series

```python id="qkhlgf"
import pandas as pd

marks = pd.Series([90, 85, 95])

print(marks)
```

Output:

```python id="2v4w3z"
0    90
1    85
2    95
dtype: int64
```

---

# Understanding Output

| Part     | Meaning   |
| -------- | --------- |
| 0,1,2    | Index     |
| 90,85,95 | Values    |
| dtype    | Data type |

---

# Important Point

A Series has:

1. Values
2. Indexes

Both are important.

---

# Accessing Values

## By Index

```python id="2m8x4u"
print(marks[0])
```

Output:

```python id="0q5f5u"
90
```

---

# Multiple Values

```python id="qv5sdp"
print(marks[[0, 2]])
```

Output:

```python id="7gktq9"
0    90
2    95
```

---

# Custom Index

Instead of 0,1,2 you can create your own labels.

```python id="8x9nho"
marks = pd.Series(
    [90, 85, 95],
    index=["Laksh", "Aryan", "Parth"]
)

print(marks)
```

Output:

```python id="7zh5t8"
Laksh    90
Aryan    85
Parth    95
```

---

# Accessing Custom Index Values

```python id="m7q7el"
print(marks["Laksh"])
```

Output:

```python id="0i3bdi"
90
```

---

# Series from Dictionary

```python id="1yq1ov"
data = {
    "Laksh": 90,
    "Aryan": 85,
    "Parth": 95
}

marks = pd.Series(data)

print(marks)
```

---

# Checking Data Type

```python id="v5c0xa"
print(type(marks))
```

Output:

```python id="3m4zqr"
<class 'pandas.core.series.Series'>
```

---

# Series Attributes

---

## index

Shows indexes.

```python id="n8h1me"
print(marks.index)
```

---

## values

Shows actual values.

```python id="w7bq7y"
print(marks.values)
```

---

## dtype

Shows data type.

```python id="khvj43"
print(marks.dtype)
```

---

# Series Operations

Pandas supports mathematical operations.

---

## Addition

```python id="m20f04"
numbers = pd.Series([1, 2, 3])

print(numbers + 10)
```

Output:

```python id="0b5t9p"
0    11
1    12
2    13
```

---

## Multiplication

```python id="svryh7"
print(numbers * 2)
```

---

# Filtering in Series

```python id="xsvm0u"
print(numbers[numbers > 1])
```

Output:

```python id="s2mx4j"
1    2
2    3
```

---

# Checking Missing Values

Pandas uses `NaN` for missing values.

```python id="7l3k0v"
data = pd.Series([10, 20, None, 40])

print(data)
```

Output:

```python id="3w7n1u"
0    10.0
1    20.0
2     NaN
3    40.0
```

---

# Detect Missing Values

```python id="u0bp0d"
print(data.isnull())
```

Output:

```python id="x6d8c1"
0    False
1    False
2     True
3    False
```

---

# Basic Functions on Series

---

## sum()

```python id="5rz1wa"
print(marks.sum())
```

---

## mean()

```python id="5tljnd"
print(marks.mean())
```

---

## max()

```python id="kv5zz7"
print(marks.max())
```

---

## min()

```python id="e2p7va"
print(marks.min())
```

---

## count()

```python id="9yrqqm"
print(marks.count())
```

---

# Sorting Series

---

## Sort by Values

```python id="pc3q80"
print(marks.sort_values())
```

---

## Descending

```python id="mvh0ny"
print(marks.sort_values(ascending=False))
```

---

# Sorting by Index

```python id="ejzq1x"
print(marks.sort_index())
```

---

# Checking Conditions

```python id="7v9uhm"
print(marks > 90)
```

Output:

```python id="jlwmn8"
Laksh    False
Aryan    False
Parth     True
```

---

# Real Life Use Cases of Series

Series are used for:

* Student marks
* Product prices
* Daily temperatures
* Monthly sales
* Sensor readings

---

# Difference Between Python List and Series

| Python List       | Pandas Series       |
| ----------------- | ------------------- |
| No labels         | Has index           |
| Basic operations  | Advanced operations |
| Less powerful     | More powerful       |
| Limited filtering | Easy filtering      |

---

# Important Interview Questions

## Q1. What is a Series?

A one-dimensional labeled array in Pandas.

---

## Q2. Can Series store mixed data?

Yes, but not recommended.

---

## Q3. What is index in Series?

Labels used to identify values.

---