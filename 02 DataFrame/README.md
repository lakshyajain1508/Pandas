# Topic 2: pandas DataFrame

# What is a DataFrame?

A **DataFrame** is a two-dimensional data structure in Pandas.

It looks like a table with:

* Rows
* Columns

Think of it like:

* Excel sheet
* SQL table
* Google Sheets

---

# Real Life Example

| Name  | Age | Marks |
| ----- | --- | ----- |
| Laksh | 20  | 90    |
| Aryan | 21  | 85    |
| Parth | 22  | 95    |

This entire table is called a **DataFrame**.

---

# Why DataFrame is Important

Almost all real-world data analysis is done using DataFrames.

Examples:

* Student databases
* Sales reports
* IPL statistics
* Netflix datasets
* Customer records

---

# Structure of DataFrame

A DataFrame contains:

1. Rows
2. Columns
3. Index

---

# Creating Your First DataFrame

```python id="gxjlwm"
import pandas as pd

data = {
    "Name": ["Laksh", "Aryan", "Parth"],
    "Age": [20, 21, 22],
    "Marks": [90, 85, 95]
}

df = pd.DataFrame(data)

print(df)
```

Output:

```python id="w2b9yq"
    Name   Age   Marks
0  Laksh   20      90
1  Aryan   21      85
2  Parth   22      95
```

---

# Understanding Output

| Part             | Meaning     |
| ---------------- | ----------- |
| 0,1,2            | Row indexes |
| Name, Age, Marks | Columns     |
| Laksh, 20, 90    | Data        |

---

# Important Point

A DataFrame is made up of multiple Series.

Each column is internally a Series.

---

# Checking Data Type

```python id="g4m9wr"
print(type(df))
```

Output:

```python id="b4g18k"
<class 'pandas.core.frame.DataFrame'>
```

---

# DataFrame Attributes

---

## shape

Shows:
(rows, columns)

```python id="3oh0b9"
print(df.shape)
```

Output:

```python id="grsl1r"
(3, 3)
```

Meaning:

* 3 rows
* 3 columns

---

## columns

Shows column names.

```python id="7rfu1m"
print(df.columns)
```

---

## index

Shows row indexes.

```python id="n3e7a1"
print(df.index)
```

---

## dtypes

Shows data types.

```python id="uyc0p8"
print(df.dtypes)
```

---

# Viewing Data

---

## head()

Shows first 5 rows.

```python id="9f9eeu"
print(df.head())
```

---

## tail()

Shows last rows.

```python id="1lj6zn"
print(df.tail())
```

---

## sample()

Shows random rows.

```python id="fby46u"
print(df.sample(2))
```

---

# Selecting Columns

---

## Single Column

```python id="j6x5m4"
print(df["Name"])
```

Output:

```python id="ol3g0m"
0    Laksh
1    Aryan
2    Parth
```

This returns a **Series**.

---

## Multiple Columns

```python id="j3clpj"
print(df[["Name", "Marks"]])
```

This returns another DataFrame.

---

# Adding New Column

```python id="ux3n1k"
df["City"] = ["Mumbai", "Pune", "Delhi"]

print(df)
```

---

# Updating Column Values

```python id="4j0c2f"
df["Marks"] = [95, 88, 99]
```

---

# Deleting Columns

```python id="mj71yz"
df.drop("City", axis=1, inplace=True)
```

---

# Understanding axis

| axis | Meaning |
| ---- | ------- |
| 0    | Rows    |
| 1    | Columns |

---

# Accessing Rows

---

# loc[] → Label Based

```python id="c3uhs8"
print(df.loc[0])
```

Gets row with label/index 0.

---

# iloc[] → Position Based

```python id="mv3d4z"
print(df.iloc[1])
```

Gets second row.

---

# Selecting Specific Rows & Columns

```python id="rnyq0l"
print(df.loc[0, "Name"])
```

Output:

```python id="81pwlv"
Laksh
```

---

# Filtering Data

---

## Students with Marks > 90

```python id="szj6xz"
print(df[df["Marks"] > 90])
```

---

## Multiple Conditions

```python id="wdh2p5"
print(df[(df["Marks"] > 85) & (df["Age"] > 20)])
```

---

# Sorting Data

---

## Ascending

```python id="pjlwmr"
print(df.sort_values("Marks"))
```

---

## Descending

```python id="v8k3h9"
print(df.sort_values("Marks", ascending=False))
```

---

# Basic Information Functions

---

## info()

```python id="z9kz0f"
print(df.info())
```

Shows:

* Columns
* Data types
* Missing values

---

## describe()

```python id="wwd2j7"
print(df.describe())
```

Shows:

* Mean
* Count
* Min
* Max
* Standard deviation

---

# Renaming Columns

```python id="vtby9j"
df.rename(columns={"Marks": "Score"}, inplace=True)
```

---

# Changing Index

```python id="0u6zkn"
df.set_index("Name", inplace=True)
```

Output:

```python id="6c9v4s"
        Age   Score
Name
Laksh   20      95
Aryan   21      88
Parth   22      99
```

---

# Reset Index

```python id="x93k6h"
df.reset_index(inplace=True)
```

---

# Missing Values

Real-world datasets often contain missing data.

Example:

| Name  | Marks |
| ----- | ----- |
| Laksh | 90    |
| Aryan | NaN   |

---

# Detect Missing Values

```python id="q8b9ri"
print(df.isnull())
```

---

# Count Missing Values

```python id="8x71it"
print(df.isnull().sum())
```

---

# Removing Missing Values

```python id="9iwl1w"
df.dropna()
```

---

# Filling Missing Values

```python id="d2obzi"
df.fillna(0)
```

---

# Saving DataFrame

---

## Save as CSV

```python id="vx6hvk"
df.to_csv("students.csv", index=False)
```

---

## Save as Excel

```python id="7cckgt"
df.to_excel("students.xlsx", index=False)
```

---

# Reading Files

---

## CSV File

```python id="r3o6ph"
df = pd.read_csv("students.csv")
```

---

## Excel File

```python id="tuw7ra"
df = pd.read_excel("students.xlsx")
```

---

# Real Life Example Workflow

Suppose school gives you:
`students.csv`

You can:

1. Load file
2. Clean data
3. Find toppers
4. Calculate average
5. Save report

All using Pandas.

---

# Difference Between Series & DataFrame

| Series          | DataFrame        |
| --------------- | ---------------- |
| One-dimensional | Two-dimensional  |
| Single column   | Multiple columns |
| Simpler         | More powerful    |

---

# Common Beginner Mistakes

---

## 1. Forgetting `axis=1`

Wrong:

```python id="77wd4w"
df.drop("Marks")
```

Correct:

```python id="i8k6m0"
df.drop("Marks", axis=1)
```

---

## 2. Confusing `loc[]` and `iloc[]`

| loc[]       | iloc[]         |
| ----------- | -------------- |
| Label based | Position based |

---

## 3. Forgetting `inplace=True`

Without it, changes may not save.

---

# Mini Project Idea

Create:

## Student Management System

Features:

* Add students
* Filter toppers
* Calculate average
* Save reports

---

# Summary

You learned:
✅ What is DataFrame
✅ Creating DataFrame
✅ Rows & Columns
✅ Selecting data
✅ Filtering
✅ Sorting
✅ Missing values
✅ Reading/Saving files
✅ loc[] and iloc[]