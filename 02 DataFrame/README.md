# Topic 2: pandas DataFrame

# What is a DataFrame?

A **DataFrame** is a two-dimensional data structure in Pandas.

It looks like a table with:

- Rows
- Columns

Think of it like:

- Excel sheet
- SQL table
- Google Sheets

---

# Real Life Example

| Name | Age | Marks |
|------|-----|-------|
| Laksh | 20 | 90 |
| Aryan | 21 | 85 |
| Parth | 22 | 95 |

This entire table is called a **DataFrame**.

---

# Why DataFrame is Important

Almost all real-world data analysis is done using DataFrames.

Examples:

- Student databases
- Sales reports
- IPL statistics
- Netflix datasets
- Customer records

---

# Structure of DataFrame

A DataFrame contains:

1. Rows
2. Columns
3. Index

---

# Creating Your First DataFrame

```python
import pandas as pd

data = {
    "Name": ["Laksh", "Aryan", "Parth"],
    "Age": [20, 21, 22],
    "Marks": [90, 85, 95]
}

df = pd.DataFrame(data)

print(df)
```

### Output

```text
    Name   Age  Marks
0  Laksh   20     90
1  Aryan   21     85
2  Parth   22     95
```

---

# Understanding Output

| Part | Meaning |
|--------|---------|
| 0,1,2 | Row indexes |
| Name, Age, Marks | Columns |
| Laksh, 20, 90 | Data |

---

# Important Point

A DataFrame is made up of multiple Series.

Each column is internally a Series.

---

# Checking Data Type

```python
print(type(df))
```

### Output

```text
<class 'pandas.core.frame.DataFrame'>
```

---

# DataFrame Attributes

## shape

Shows:

```text
(rows, columns)
```

```python
print(df.shape)
```

### Output

```text
(3, 3)
```

Meaning:

- 3 rows
- 3 columns

---

## columns

Shows column names.

```python
print(df.columns)
```

---

## index

Shows row indexes.

```python
print(df.index)
```

---

## dtypes

Shows data types.

```python
print(df.dtypes)
```

---

# Viewing Data

## head()

Shows first 5 rows.

```python
print(df.head())
```

---

## tail()

Shows last rows.

```python
print(df.tail())
```

---

## sample()

Shows random rows.

```python
print(df.sample(2))
```

---

# Selecting Columns

## Single Column

```python
print(df["Name"])
```

### Output

```text
0    Laksh
1    Aryan
2    Parth
```

This returns a **Series**.

---

## Multiple Columns

```python
print(df[["Name", "Marks"]])
```

This returns another DataFrame.

---

# Adding New Column

```python
df["City"] = ["Mumbai", "Pune", "Delhi"]

print(df)
```

---

# Updating Column Values

```python
df["Marks"] = [95, 88, 99]
```

---

# Deleting Columns

```python
df.drop("City", axis=1, inplace=True)
```

---

# Understanding axis

| axis | Meaning |
|------|---------|
| 0 | Rows |
| 1 | Columns |

---

# Accessing Rows

## loc[] → Label Based

```python
print(df.loc[0])
```

Gets row with label/index 0.

---

## iloc[] → Position Based

```python
print(df.iloc[1])
```

Gets second row.

---

# Selecting Specific Rows & Columns

```python
print(df.loc[0, "Name"])
```

### Output

```text
Laksh
```

---

# Filtering Data

## Students with Marks > 90

```python
print(df[df["Marks"] > 90])
```

---

## Multiple Conditions

```python
print(df[(df["Marks"] > 85) & (df["Age"] > 20)])
```

---

# Sorting Data

## Ascending

```python
print(df.sort_values("Marks"))
```

---

## Descending

```python
print(df.sort_values("Marks", ascending=False))
```

---

# Basic Information Functions

## info()

```python
print(df.info())
```

Shows:

- Columns
- Data types
- Missing values

---

## describe()

```python
print(df.describe())
```

Shows:

- Mean
- Count
- Min
- Max
- Standard deviation

---

# Renaming Columns

```python
df.rename(columns={"Marks": "Score"}, inplace=True)
```

---

# Changing Index

```python
df.set_index("Name", inplace=True)
```

### Output

```text
        Age  Score
Name
Laksh    20     95
Aryan    21     88
Parth    22     99
```

---

# Reset Index

```python
df.reset_index(inplace=True)
```

---

# Missing Values

Real-world datasets often contain missing data.

### Example

| Name | Marks |
|------|-------|
| Laksh | 90 |
| Aryan | NaN |

---

# Detect Missing Values

```python
print(df.isnull())
```

---

# Count Missing Values

```python
print(df.isnull().sum())
```

---

# Removing Missing Values

```python
df.dropna()
```

---

# Filling Missing Values

```python
df.fillna(0)
```

---

# Saving DataFrame

## Save as CSV

```python
df.to_csv("students.csv", index=False)
```

---

## Save as Excel

```python
df.to_excel("students.xlsx", index=False)
```

---

# Reading Files

## CSV File

```python
df = pd.read_csv("students.csv")
```

---

## Excel File

```python
df = pd.read_excel("students.xlsx")
```

---

# Real Life Example Workflow

Suppose a school gives you:

```text
students.csv
```

You can:

1. Load the file
2. Clean the data
3. Find toppers
4. Calculate averages
5. Save reports

All using Pandas.

---

# Difference Between Series & DataFrame

| Series | DataFrame |
|---------|-----------|
| One-dimensional | Two-dimensional |
| Single column | Multiple columns |
| Simpler | More powerful |

---

# Common Beginner Mistakes

## 1. Forgetting `axis=1`

### Wrong

```python
df.drop("Marks")
```

### Correct

```python
df.drop("Marks", axis=1)
```

---

## 2. Confusing `loc[]` and `iloc[]`

| loc[] | iloc[] |
|--------|---------|
| Label based | Position based |

---

## 3. Forgetting `inplace=True`

Without it, changes may not be saved.

---

# Mini Project Idea

## Student Management System

### Features

- Add students
- Filter toppers
- Calculate averages
- Save reports

---

# Summary

You learned:

✅ What is a DataFrame

✅ Creating a DataFrame

✅ Rows & Columns

✅ Selecting data

✅ Filtering

✅ Sorting

✅ Missing values

✅ Reading and Saving files

✅ `loc[]` and `iloc[]`

---

# Key Takeaway

A **DataFrame** is the most important data structure in Pandas. Almost every data analysis, machine learning, and data cleaning task starts with loading data into a DataFrame and manipulating it efficiently.