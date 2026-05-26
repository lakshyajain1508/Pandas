# Topic 4: Data Cleaning & Missing Values in pandas

## Why Data Cleaning is Important

Real-world datasets are **never perfect**.

They usually contain:

- Missing values
- Wrong spellings
- Duplicate rows
- Empty cells
- Incorrect formats

Before analysis or AI/ML:

> **Data must be cleaned.**

---

## Real Life Example

Imagine student data:

| Name  | Age        | Marks |
| ------ | ---------- | ------ |
| Laksh | 20 | 90 |
| Aryan | NaN | 85 |
| Laksh | 20 | 90 |
| Parth | twenty two | NaN |

### Problems

- Missing values
- Duplicate row
- Wrong datatype

This is very common in real-world datasets.

---

## Create Sample Dataset

```python
import pandas as pd
import numpy as np

data = {
    "Name": ["Laksh", "Aryan", "Laksh", "Parth"],
    "Age": [20, np.nan, 20, "twenty two"],
    "Marks": [90, 85, 90, np.nan],
    "City": ["Mumbai", "Pune", "Mumbai", None]
}

df = pd.DataFrame(data)

print(df)
```

### Output

```text
     Name          Age  Marks    City
0   Laksh           20   90.0  Mumbai
1   Aryan          NaN   85.0    Pune
2   Laksh           20   90.0  Mumbai
3   Parth  twenty two    NaN    None
```

---

# 1. Missing Values

Missing values are shown as:

```text
NaN
```

### Meaning

- Not a Number
- Empty value

---

## Detect Missing Values

```python
print(df.isnull())
```

### Output

```text
    Name    Age  Marks   City
0  False  False  False  False
1  False   True  False  False
2  False  False  False  False
3  False  False   True   True
```

### Explanation

- `True` means a missing value exists.

---

## Count Missing Values

```python
print(df.isnull().sum())
```

### Output

```text
Name     0
Age      1
Marks    1
City     1
```

### Explanation

- Age has 1 missing value
- Marks has 1 missing value
- City has 1 missing value

---

# 2. Remove Missing Values

## Drop Rows with Missing Values

```python
print(df.dropna())
```

### Output

```text
    Name Age  Marks    City
0  Laksh  20   90.0  Mumbai
2  Laksh  20   90.0  Mumbai
```

### Explanation

Rows containing missing values are removed.

---

## Important

`dropna()` does **not** change the original DataFrame unless:

```python
df.dropna(inplace=True)
```

---

## Drop Columns with Missing Values

```python
print(df.dropna(axis=1))
```

### Explanation

- `axis=1` means columns.

---

# 3. Fill Missing Values

Sometimes deleting data is not a good idea.

Instead, fill missing values.

---

## Fill with Zero

```python
print(df.fillna(0))
```

### Output

```text
     Name          Age  Marks    City
0   Laksh           20   90.0  Mumbai
1   Aryan            0   85.0    Pune
2   Laksh           20   90.0  Mumbai
3   Parth  twenty two    0.0       0
```

---

## Fill Specific Column

```python
df["Marks"] = df["Marks"].fillna(50)

print(df)
```

---

## Fill with Mean

Very common in Data Science.

```python
df["Marks"] = df["Marks"].fillna(df["Marks"].mean())

print(df)
```

### Explanation

Missing marks are replaced by the average marks.

---

## Fill with Median

```python
df["Marks"] = df["Marks"].fillna(df["Marks"].median())
```

---

## Fill with Mode

```python
df["City"] = df["City"].fillna(df["City"].mode()[0])
```

---

## Forward Fill

Uses the previous value.

```python
print(df.fillna(method="ffill"))
```

---

## Backward Fill

Uses the next value.

```python
print(df.fillna(method="bfill"))
```

---

# 4. Duplicate Data

Duplicate rows are very common.

---

## Detect Duplicates

```python
print(df.duplicated())
```

### Output

```text
0    False
1    False
2     True
3    False
```

### Explanation

Row 2 is a duplicate.

---

## Remove Duplicates

```python
print(df.drop_duplicates())
```

---

## Remove Duplicates Permanently

```python
df.drop_duplicates(inplace=True)
```

---

## Remove Duplicates Based on One Column

```python
print(df.drop_duplicates(subset=["Name"]))
```

---

# 5. Changing Data Types

Very important in cleaning.

---

## Check Data Types

```python
print(df.dtypes)
```

---

## Convert to Integer

```python
df["Marks"] = df["Marks"].astype(int)
```

---

## Convert to Float

```python
df["Marks"] = df["Marks"].astype(float)
```

---

## Convert to String

```python
df["Age"] = df["Age"].astype(str)
```

---

## Problem Example

This will fail:

```python
df["Age"] = df["Age"].astype(int)
```

### Because

```text
twenty two
```

is not numeric.

---

## Fix Wrong Data

### Replace Wrong Values

```python
df["Age"] = df["Age"].replace("twenty two", 22)

print(df)
```

Now conversion works correctly.

---

# 6. String Cleaning

Real datasets often contain messy text.

---

## Example Dataset

```python
df = pd.DataFrame({
    "Name": [" Laksh ", "ARYAN", "parth"]
})

print(df)
```

---

## Remove Spaces

```python
df["Name"] = df["Name"].str.strip()
```

---

## Convert to Lowercase

```python
df["Name"] = df["Name"].str.lower()
```

---

## Convert to Uppercase

```python
df["Name"] = df["Name"].str.upper()
```

---

## Capitalize Text

```python
df["Name"] = df["Name"].str.title()
```

---

## Replace Text

```python
df["Name"] = df["Name"].str.replace("Laksh", "Lakshya")
```

---

# 7. Rename Columns

## Rename One Column

```python
df.rename(columns={"Marks": "Score"}, inplace=True)
```

---

## Rename Multiple Columns

```python
df.rename(
    columns={
        "Marks": "Score",
        "City": "Location"
    },
    inplace=True
)
```

---

# 8. Remove Columns

## Remove Single Column

```python
df.drop("City", axis=1, inplace=True)
```

---

## Remove Multiple Columns

```python
df.drop(
    ["City", "Age"],
    axis=1,
    inplace=True
)
```

---

# 9. Detect Outliers (Basic)

Outliers are abnormal values.

### Example

- Marks = 9999

---

## Find Large Values

```python
print(df[df["Marks"] > 100])
```

---

# 10. Useful Cleaning Functions

| Function | Purpose |
|-----------|---------|
| `isnull()` | Detect missing values |
| `dropna()` | Remove missing values |
| `fillna()` | Fill missing values |
| `duplicated()` | Detect duplicates |
| `drop_duplicates()` | Remove duplicates |
| `astype()` | Change datatype |
| `replace()` | Replace values |

---

# Real Workflow Example

Professional analysts usually follow these steps.

---

## Step 1: Read Data

```python
df = pd.read_csv("students.csv")
```

---

## Step 2: Check Missing Values

```python
print(df.isnull().sum())
```

---

## Step 3: Remove Duplicates

```python
df.drop_duplicates(inplace=True)
```

---

## Step 4: Fix Missing Values

```python
df.fillna(0, inplace=True)
```

---

## Step 5: Fix Text Formatting

```python
df["Name"] = df["Name"].str.title()
```

---

## Step 6: Save Cleaned Dataset

```python
df.to_csv("cleaned_data.csv", index=False)
```

---

# Summary

You learned:

✅ Missing values

✅ `isnull()`

✅ `dropna()`

✅ `fillna()`

✅ Duplicate removal

✅ String cleaning

✅ Data type conversion

✅ Column renaming

✅ Removing columns

✅ Real data cleaning workflow

---