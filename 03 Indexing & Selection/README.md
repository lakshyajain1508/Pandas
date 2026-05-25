# Topic 3: Indexing & Selection Mastery in pandas

This is one of the MOST important topics in Pandas.

Why?

Because in real-world data analysis:

* 70% work = selecting correct data
* Analysts constantly filter rows & columns
* Machine learning preprocessing depends on selection

If you master indexing, Pandas becomes much easier.

---

# What is Indexing?

Indexing means:

## Accessing specific data from a DataFrame or Series.

Example:

* Select rows
* Select columns
* Select ranges
* Filter conditions

---

# Types of Indexing in Pandas

There are mainly 4 methods:

| Method          | Purpose                  |
| --------------- | ------------------------ |
| `[]`            | Basic selection          |
| `loc[]`         | Label-based selection    |
| `iloc[]`        | Position-based selection |
| Boolean Masking | Conditional filtering    |

---

# Sample DataFrame

We use this throughout:

```python id="oz0zjk"
import pandas as pd

df = pd.DataFrame({
    "Name": ["Laksh", "Aryan", "Parth", "Riya"],
    "Age": [20, 21, 22, 19],
    "Marks": [90, 85, 95, 88],
    "City": ["Mumbai", "Pune", "Delhi", "Mumbai"]
})

print(df)
```

Output:

```python id="s7bjlwm"
     Name   Age   Marks    City
0   Laksh   20      90   Mumbai
1   Aryan   21      85   Pune
2   Parth   22      95   Delhi
3    Riya   19      88   Mumbai
```

---

# 1. Basic Selection Using `[]`

---

# Select Single Column

```python id="jlwm3h"
df["Name"]
```

Output:

```python id="2u8i6p"
0    Laksh
1    Aryan
2    Parth
3     Riya
```

Type returned:

## Series

---

# Select Multiple Columns

```python id="jlwm8u"
df[["Name", "Marks"]]
```

Type returned:

## DataFrame

---

# Important Difference

| Syntax         | Result    |
| -------------- | --------- |
| `df["Name"]`   | Series    |
| `df[["Name"]]` | DataFrame |

---

# Column Selection Internally

```text id="d6zkwn"
df["Name"]
   ↓
Search column label
   ↓
Return Series
```

---

# 2. loc[] (Label-Based Selection)

One of the MOST used functions.

---

# Syntax

```python id="jlwm0v"
df.loc[row_labels, column_labels]
```

---

# Select Single Row

```python id="jlwmf1"
df.loc[0]
```

Output:

```python id="jlwm4t"
Name       Laksh
Age           20
Marks         90
City      Mumbai
```

---

# Select Multiple Rows

```python id="9m12ht"
df.loc[[0, 2]]
```

---

# Select Specific Rows & Columns

```python id="jlwm3x"
df.loc[[0, 2], ["Name", "Marks"]]
```

Output:

```python id="jlwmc9"
    Name   Marks
0  Laksh     90
2  Parth     95
```

---

# Select Range Using loc[]

```python id="jlwm6b"
df.loc[0:2]
```

IMPORTANT:

## loc includes ending index.

Result:
Rows 0,1,2 included.

---

# Conditional Selection with loc[]

```python id="jlwm9a"
df.loc[df["Marks"] > 90]
```

---

# Modify Values Using loc[]

```python id="4yjlwm"
df.loc[0, "Marks"] = 99
```

---

# Multiple Updates

```python id="jlwm4o"
df.loc[df["City"] == "Mumbai", "Marks"] = 100
```

---

# Custom Index with loc[]

```python id="jlwm2k"
df.index = ["a", "b", "c", "d"]

print(df)
```

Now:

```python id="3jlwmf"
df.loc["a"]
```

---

# 3. iloc[] (Position-Based Selection)

iloc uses:

## Integer positions

---

# Syntax

```python id="jlwm4n"
df.iloc[row_positions, column_positions]
```

---

# Select First Row

```python id="3zjlwm"
df.iloc[0]
```

---

# Select Multiple Rows

```python id="jlwm7s"
df.iloc[[0, 2]]
```

---

# Select Specific Rows & Columns

```python id="4jlwmz"
df.iloc[[0, 2], [0, 2]]
```

Output:

```python id="jlwm5j"
    Name   Marks
0  Laksh     90
2  Parth     95
```

---

# Range Selection

```python id="6jlwmk"
df.iloc[0:2]
```

IMPORTANT:

## iloc excludes ending index.

Returns:
Rows 0 and 1 only.

---

# loc vs iloc (VERY IMPORTANT)

| loc[]               | iloc[]                |
| ------------------- | --------------------- |
| Label-based         | Position-based        |
| Includes stop index | Excludes stop index   |
| Uses column names   | Uses column positions |

---

# Example Comparison

---

# loc

```python id="7jlwmn"
df.loc[0:2]
```

Returns:
0,1,2

---

# iloc

```python id="jlwm1f"
df.iloc[0:2]
```

Returns:
0,1

---

# 4. Boolean Masking (SUPER IMPORTANT)

Used heavily in:

* Data analysis
* Machine learning
* Dashboards

---

# Basic Condition

```python id="jlwm8n"
df["Marks"] > 90
```

Output:

```python id="zjlwmq"
0    False
1    False
2     True
3    False
```

This is called:

## Boolean Mask

---

# Using Boolean Mask

```python id="jlwm2n"
df[df["Marks"] > 90]
```

---

# Multiple Conditions

Use:

* `&` → AND
* `|` → OR
* `~` → NOT

---

# AND Condition

```python id="jlwm9o"
df[
    (df["Marks"] > 85) &
    (df["Age"] > 20)
]
```

---

# OR Condition

```python id="jlwm6s"
df[
    (df["City"] == "Mumbai") |
    (df["Marks"] > 90)
]
```

---

# NOT Condition

```python id="jlwm7v"
df[
    ~(df["City"] == "Mumbai")
]
```

---

# IMPORTANT RULE

Always wrap conditions in brackets.

Correct:

```python id="8jlwmx"
(df["Marks"] > 90)
```

Wrong:

```python id="9jlwmw"
df["Marks"] > 90
```

inside combined conditions.

---

# isin() Function

Used to check multiple values.

---

# Example

```python id="5jlwmc"
df[df["City"].isin(["Mumbai", "Delhi"])]
```

---

# between() Function

```python id="4jlwmr"
df[df["Marks"].between(85, 95)]
```

---

# String Filtering

---

# contains()

```python id="2jlwmm"
df[df["Name"].str.contains("a")]
```

---

# startswith()

```python id="1jlwmz"
df[df["Name"].str.startswith("L")]
```

---

# endswith()

```python id="0jlwmv"
df[df["Name"].str.endswith("h")]
```

---

# query() Method

Cleaner filtering syntax.

---

# Example

```python id="jlwm5l"
df.query("Marks > 90")
```

---

# Multiple Conditions

```python id="3jlwmu"
df.query("Marks > 85 and Age > 20")
```

---

# Why query() is Useful

Cleaner for:

* Large conditions
* Readability
* Analytics scripts

---

# Selecting Random Rows

```python id="7jlwml"
df.sample(2)
```

---

# Selecting Top Rows

```python id="9jlwmp"
df.head(2)
```

---

# Selecting Last Rows

```python id="8jlwmt"
df.tail(2)
```

---

# Index Manipulation

---

# Set Custom Index

```python id="6jlwmu"
df.set_index("Name", inplace=True)
```

---

# Access with New Index

```python id="5jlwmx"
df.loc["Laksh"]
```

---

# Reset Index

```python id="4jlwmq"
df.reset_index(inplace=True)
```

---

# MultiIndex Introduction

Advanced indexing system.

---

# Example

```python id="2jlwmw"
df.set_index(["City", "Name"], inplace=True)
```

Output:

```text id="1jlwmh"
                 Age   Marks
City    Name
Mumbai Laksh   20      90
Pune    Aryan  21      85
```

---

# Access MultiIndex

```python id="0jlwmk"
df.loc["Mumbai"]
```

---

# Copy vs View Problem

Very important issue.

---

# Problem Example

```python id="zjlwmv"
filtered = df[df["Marks"] > 90]
```

Sometimes this creates:

* Copy
  OR
* View

This can cause warnings.

---

# Safe Way

```python id="yjlwmm"
filtered = df[df["Marks"] > 90].copy()
```

---

# Chained Indexing Problem

BAD:

```python id="xjlwmj"
df[df["Marks"] > 90]["Age"]
```

Better:

```python id="wjlwmn"
df.loc[df["Marks"] > 90, "Age"]
```

---

# Performance Tips

---

# Fastest Selection

```python id="vjlwms"
df.loc[]
```

preferred over loops.

---

# Avoid iterrows()

Slow:

```python id="ujlwmx"
for index, row in df.iterrows():
    pass
```

---

# Use Vectorization

Fast:

```python id="tjlwmv"
df["Marks"] + 5
```

---

# Real World Use Cases

Indexing is used for:

* Finding top students
* Filtering customers
* Fraud detection
* Sales analysis
* Stock market analysis

---

# Most Important Concepts to Master

✅ loc[]
✅ iloc[]
✅ Boolean masking
✅ query()
✅ Multi-condition filtering
✅ Index manipulation
✅ isin()
✅ String filtering
✅ Copy vs View

---

# Practice Exercises

---

# Exercise 1

Find students with marks > 90.

---

# Exercise 2

Find Mumbai students.

---

# Exercise 3

Find students with:

* Marks > 85
* Age < 22

---

# Exercise 4

Set Name as index.

---

# Exercise 5

Use query() to filter data.

---

# Mini Challenge

Create a DataFrame for:

* IPL players
* Runs
* Teams

Then:

* Filter top scorers
* Find specific teams
* Sort by runs
* Use loc and iloc

---

# Summary

You now deeply understand:

✅ loc[]
✅ iloc[]
✅ Boolean masking
✅ query()
✅ String filtering
✅ MultiIndex basics
✅ Advanced selection
✅ Performance concepts
