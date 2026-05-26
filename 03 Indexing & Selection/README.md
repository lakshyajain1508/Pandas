# Topic 3: Indexing & Selection Mastery in pandas

This is one of the **most important topics** in Pandas.

### Why?

Because in real-world data analysis:

- 70% of the work involves selecting the correct data
- Analysts constantly filter rows and columns
- Machine Learning preprocessing depends heavily on data selection

If you master indexing, Pandas becomes much easier.

---

# What is Indexing?

Indexing means:

> Accessing specific data from a DataFrame or Series.

### Examples

- Select rows
- Select columns
- Select ranges
- Filter data using conditions

---

# Types of Indexing in Pandas

There are mainly 4 methods:

| Method | Purpose |
|----------|----------|
| `[]` | Basic selection |
| `loc[]` | Label-based selection |
| `iloc[]` | Position-based selection |
| Boolean Masking | Conditional filtering |

---

# Sample DataFrame

We will use this DataFrame throughout the chapter.

```python
import pandas as pd

df = pd.DataFrame({
    "Name": ["Laksh", "Aryan", "Parth", "Riya"],
    "Age": [20, 21, 22, 19],
    "Marks": [90, 85, 95, 88],
    "City": ["Mumbai", "Pune", "Delhi", "Mumbai"]
})

print(df)
```

### Output

```text
     Name   Age  Marks    City
0   Laksh   20     90   Mumbai
1   Aryan   21     85     Pune
2   Parth   22     95    Delhi
3    Riya   19     88   Mumbai
```

---

# 1. Basic Selection Using `[]`

## Select Single Column

```python
df["Name"]
```

### Output

```text
0    Laksh
1    Aryan
2    Parth
3     Riya
```

### Type Returned

**Series**

---

## Select Multiple Columns

```python
df[["Name", "Marks"]]
```

### Type Returned

**DataFrame**

---

## Important Difference

| Syntax | Result |
|----------|----------|
| `df["Name"]` | Series |
| `df[["Name"]]` | DataFrame |

---

## Column Selection Internally

```text
df["Name"]
   ↓
Search column label
   ↓
Return Series
```

---

# 2. `loc[]` (Label-Based Selection)

One of the most used functions in Pandas.

---

## Syntax

```python
df.loc[row_labels, column_labels]
```

---

## Select Single Row

```python
df.loc[0]
```

### Output

```text
Name       Laksh
Age           20
Marks         90
City      Mumbai
```

---

## Select Multiple Rows

```python
df.loc[[0, 2]]
```

---

## Select Specific Rows and Columns

```python
df.loc[[0, 2], ["Name", "Marks"]]
```

### Output

```text
    Name  Marks
0  Laksh     90
2  Parth     95
```

---

## Select Range Using `loc[]`

```python
df.loc[0:2]
```

### Important

`loc[]` includes the ending index.

Result includes:

```text
0, 1, 2
```

---

## Conditional Selection with `loc[]`

```python
df.loc[df["Marks"] > 90]
```

---

## Modify Values Using `loc[]`

```python
df.loc[0, "Marks"] = 99
```

---

## Multiple Updates

```python
df.loc[df["City"] == "Mumbai", "Marks"] = 100
```

---

## Custom Index with `loc[]`

```python
df.index = ["a", "b", "c", "d"]

print(df)
```

Now:

```python
df.loc["a"]
```

---

# 3. `iloc[]` (Position-Based Selection)

`iloc[]` uses integer positions.

---

## Syntax

```python
df.iloc[row_positions, column_positions]
```

---

## Select First Row

```python
df.iloc[0]
```

---

## Select Multiple Rows

```python
df.iloc[[0, 2]]
```

---

## Select Specific Rows and Columns

```python
df.iloc[[0, 2], [0, 2]]
```

### Output

```text
    Name  Marks
0  Laksh     90
2  Parth     95
```

---

## Range Selection

```python
df.iloc[0:2]
```

### Important

`iloc[]` excludes the ending index.

Returns:

```text
0, 1
```

---

# `loc[]` vs `iloc[]` (Very Important)

| `loc[]` | `iloc[]` |
|----------|----------|
| Label-based | Position-based |
| Includes stop index | Excludes stop index |
| Uses column names | Uses column positions |

---

## Example Comparison

### loc

```python
df.loc[0:2]
```

Returns:

```text
0, 1, 2
```

---

### iloc

```python
df.iloc[0:2]
```

Returns:

```text
0, 1
```

---

# 4. Boolean Masking (Super Important)

Used heavily in:

- Data Analysis
- Machine Learning
- Dashboards

---

## Basic Condition

```python
df["Marks"] > 90
```

### Output

```text
0    False
1    False
2     True
3    False
```

This is called a:

> Boolean Mask

---

## Using Boolean Mask

```python
df[df["Marks"] > 90]
```

---

## Multiple Conditions

Use:

| Operator | Meaning |
|-----------|---------|
| `&` | AND |
| `|` | OR |
| `~` | NOT |

---

## AND Condition

```python
df[
    (df["Marks"] > 85) &
    (df["Age"] > 20)
]
```

---

## OR Condition

```python
df[
    (df["City"] == "Mumbai") |
    (df["Marks"] > 90)
]
```

---

## NOT Condition

```python
df[
    ~(df["City"] == "Mumbai")
]
```

---

## Important Rule

Always wrap conditions in brackets.

### Correct

```python
(df["Marks"] > 90)
```

### Wrong (inside combined conditions)

```python
df["Marks"] > 90
```

---

# `isin()` Function

Used to check multiple values.

### Example

```python
df[df["City"].isin(["Mumbai", "Delhi"])]
```

---

# `between()` Function

```python
df[df["Marks"].between(85, 95)]
```

---

# String Filtering

---

## `contains()`

```python
df[df["Name"].str.contains("a")]
```

---

## `startswith()`

```python
df[df["Name"].str.startswith("L")]
```

---

## `endswith()`

```python
df[df["Name"].str.endswith("h")]
```

---

# `query()` Method

Provides a cleaner filtering syntax.

### Example

```python
df.query("Marks > 90")
```

---

## Multiple Conditions

```python
df.query("Marks > 85 and Age > 20")
```

---

## Why `query()` is Useful

Cleaner for:

- Large conditions
- Better readability
- Analytics scripts

---

# Selecting Random Rows

```python
df.sample(2)
```

---

# Selecting Top Rows

```python
df.head(2)
```

---

# Selecting Last Rows

```python
df.tail(2)
```

---

# Index Manipulation

## Set Custom Index

```python
df.set_index("Name", inplace=True)
```

---

## Access with New Index

```python
df.loc["Laksh"]
```

---

## Reset Index

```python
df.reset_index(inplace=True)
```

---

# MultiIndex Introduction

Advanced indexing system.

---

## Example

```python
df.set_index(["City", "Name"], inplace=True)
```

### Output

```text
                 Age  Marks
City    Name
Mumbai  Laksh   20     90
Pune    Aryan   21     85
```

---

## Access MultiIndex

```python
df.loc["Mumbai"]
```

---

# Copy vs View Problem

Very important issue.

---

## Problem Example

```python
filtered = df[df["Marks"] > 90]
```

Sometimes this creates either:

- Copy
- View

This can generate warnings.

---

## Safe Way

```python
filtered = df[df["Marks"] > 90].copy()
```

---

# Chained Indexing Problem

### Bad

```python
df[df["Marks"] > 90]["Age"]
```

### Better

```python
df.loc[df["Marks"] > 90, "Age"]
```

---

# Performance Tips

## Fastest Selection

```python
df.loc[]
```

Preferred over loops.

---

## Avoid `iterrows()`

Slow:

```python
for index, row in df.iterrows():
    pass
```

---

## Use Vectorization

Fast:

```python
df["Marks"] + 5
```

---

# Real-World Use Cases

Indexing is used for:

- Finding top students
- Filtering customers
- Fraud detection
- Sales analysis
- Stock market analysis

---

# Most Important Concepts to Master

✅ `loc[]`

✅ `iloc[]`

✅ Boolean Masking

✅ `query()`

✅ Multi-condition filtering

✅ Index manipulation

✅ `isin()`

✅ String filtering

✅ Copy vs View

---

# Summary

In this chapter, you learned:

- Basic column selection using `[]`
- Label-based selection with `loc[]`
- Position-based selection with `iloc[]`
- Boolean masking and conditional filtering
- String-based filtering
- `isin()` and `between()`
- Query-based filtering
- Index manipulation and MultiIndex
- Copy vs View issues
- Performance optimization techniques

Mastering these concepts is essential for efficient data analysis, data cleaning, feature engineering, and machine learning workflows using Pandas.