# Pandas

Pandas is one of the most popular Python libraries used for:

* Data Analysis
* Data Cleaning
* Working with CSV/Excel files
* Data Visualization preparation
* Machine Learning preprocessing

It helps you work with data in a simple table format like Excel sheets.

---

# Why Learn Pandas?

With Pandas you can:

- ✅ Read CSV and Excel files
- ✅ Filter and clean data
- ✅ Analyze large datasets
- ✅ Handle missing values
- ✅ Sort and group data
- ✅ Prepare datasets for AI/ML projects

Companies use it heavily in:

* Data Science
* AI/ML
* Backend Analytics
* Finance
* Research

---

# Main Concepts in Pandas

## 1. Series

A Series is like a single column in Excel.

```python
import pandas as pd

data = pd.Series([10, 20, 30, 40])

print(data)
```

---

## 2. DataFrame

A DataFrame is a full table (rows + columns).

```python
import pandas as pd

data = {
    "Name": ["Laksh", "Aryan", "Parth"],
    "Age": [20, 21, 22]
}

df = pd.DataFrame(data)

print(df)
```

---

# Installing Pandas

```bash
pip install pandas
```

---

# Reading CSV Files

```python
import pandas as pd

df = pd.read_csv("students.csv")

print(df)
```

---

# Useful Functions

| Function     | Purpose             |
| ------------ | ------------------- |
| `head()`     | First 5 rows        |
| `tail()`     | Last 5 rows         |
| `info()`     | Dataset information |
| `describe()` | Statistics summary  |
| `shape`      | Rows and columns    |
| `columns`    | Column names        |

Example:

```python
print(df.head())
print(df.info())
```

---

# Selecting Data

## Select Column

```python
print(df["Name"])
```

## Select Multiple Columns

```python
print(df[["Name", "Age"]])
```

---

# Filtering Data

```python
print(df[df["Age"] > 20])
```

---

# Adding New Column

```python
df["Marks"] = [90, 85, 88]
```

---

# Saving Data

```python
df.to_csv("output.csv", index=False)
```

---

# Beginner Roadmap for Pandas

## Beginner

* Series
* DataFrame
* Reading CSV
* head(), tail()
* Filtering

## Intermediate

* Missing values
* GroupBy
* Sorting
* Merging datasets

## Advanced

* Pivot Tables
* Time Series
* Data Visualization with Matplotlib
* Data Cleaning Pipelines

---
