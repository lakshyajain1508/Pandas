# Topic 4: Data Cleaning & Missing Values in pandas

## Easy Explanation + Practical Coding

---

# Why Data Cleaning is Important

Real-world datasets are NEVER perfect.

They usually contain:

* Missing values
* Wrong spellings
* Duplicate rows
* Empty cells
* Incorrect formats

Before analysis or AI/ML:

## Data MUST be cleaned.

---

# Real Life Example

Imagine student data:

| Name  | Age        | Marks |
| ----- | ---------- | ----- |
| Laksh | 20         | 90    |
| Aryan | NaN        | 85    |
| Laksh | 20         | 90    |
| Parth | twenty two | NaN   |

Problems:

* Missing values
* Duplicate row
* Wrong datatype

This is very common.

---

# Create Sample Dataset

```python id="nltjlwm"
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

Output:

```python id="jlwmr1"
     Name          Age  Marks    City
0   Laksh           20   90.0  Mumbai
1   Aryan          NaN   85.0    Pune
2   Laksh           20   90.0  Mumbai
3   Parth  twenty two    NaN    None
```

---

# 1. Missing Values

Missing values are shown as:

```text id="jlwmr2"
NaN
```

Meaning:

## Not a Number

or empty value.

---

# Detect Missing Values

```python id="jlwmr3"
print(df.isnull())
```

Output:

```python id="jlwmr4"
    Name    Age  Marks   City
0  False  False  False  False
1  False   True  False  False
2  False  False  False  False
3  False  False   True   True
```

Explanation:

* `True` means missing value exists.

---

# Count Missing Values

```python id="jlwmr5"
print(df.isnull().sum())
```

Output:

```python id="jlwmr6"
Name     0
Age      1
Marks    1
City     1
```

Explanation:

* Age has 1 missing value
* Marks has 1 missing value
* City has 1 missing value

---

# 2. Remove Missing Values

---

# Drop Rows with Missing Values

```python id="jlwmr7"
print(df.dropna())
```

Output:

```python id="jlwmr8"
    Name Age  Marks    City
0  Laksh  20   90.0  Mumbai
2  Laksh  20   90.0  Mumbai
```

Explanation:

* Rows with missing values removed.

---

# IMPORTANT

`dropna()` does NOT change original DataFrame unless:

```python id="jlwmr9"
df.dropna(inplace=True)
```

---

# Drop Columns with Missing Values

```python id="jlwmra"
print(df.dropna(axis=1))
```

Explanation:

* `axis=1` means columns.

---

# 3. Fill Missing Values

Sometimes deleting data is bad.

Instead:

## Fill missing values.

---

# Fill with Zero

```python id="jlwmrb"
print(df.fillna(0))
```

Output:

```python id="jlwmrc"
     Name          Age  Marks    City
0   Laksh           20   90.0  Mumbai
1   Aryan            0   85.0    Pune
2   Laksh           20   90.0  Mumbai
3   Parth  twenty two    0.0       0
```

---

# Fill Specific Column

```python id="jlwmrd"
df["Marks"] = df["Marks"].fillna(50)

print(df)
```

---

# Fill with Mean

Very common in data science.

---

# Example

```python id="jlwmre"
df["Marks"] = df["Marks"].fillna(df["Marks"].mean())

print(df)
```

Explanation:

* Missing marks replaced by average marks.

---

# Fill with Median

```python id="jlwmrf"
df["Marks"] = df["Marks"].fillna(df["Marks"].median())
```

---

# Fill with Mode

```python id="jlwmrg"
df["City"] = df["City"].fillna(df["City"].mode()[0])
```

---

# Forward Fill

Uses previous value.

```python id="jlwmrh"
print(df.fillna(method="ffill"))
```

---

# Backward Fill

Uses next value.

```python id="jlwmri"
print(df.fillna(method="bfill"))
```

---

# 4. Duplicate Data

Duplicate rows are very common.

---

# Detect Duplicates

```python id="jlwmrj"
print(df.duplicated())
```

Output:

```python id="jlwmrk"
0    False
1    False
2     True
3    False
```

Explanation:

* Row 2 is duplicate.

---

# Remove Duplicates

```python id="jlwmrl"
print(df.drop_duplicates())
```

---

# Remove Duplicates Permanently

```python id="jlwmrm"
df.drop_duplicates(inplace=True)
```

---

# Remove Duplicate Based on One Column

```python id="jlwmrn"
print(df.drop_duplicates(subset=["Name"]))
```

---

# 5. Changing Data Types

Very important in cleaning.

---

# Check Data Types

```python id="jlwmro"
print(df.dtypes)
```

---

# Convert Column Type

---

# Convert to Integer

```python id="分快三1"
df["Marks"] = df["Marks"].astype(int)
```

---

# Convert to Float

```python id="分快三2"
df["Marks"] = df["Marks"].astype(float)
```

---

# Convert to String

```python id="分快三3"
df["Age"] = df["Age"].astype(str)
```

---

# Problem Example

This will fail:

```python id="分快三4"
df["Age"] = df["Age"].astype(int)
```

Because:

```text id="分快三5"
twenty two
```

is not numeric.

---

# Fix Wrong Data

---

# Replace Wrong Values

```python id="分快三6"
df["Age"] = df["Age"].replace("twenty two", 22)

print(df)
```

Now conversion works.

---

# 6. String Cleaning

Real datasets contain messy text.

---

# Example Dataset

```python id="分快三7"
df = pd.DataFrame({
    "Name": [" Laksh ", "ARYAN", "parth"]
})

print(df)
```

---

# Remove Spaces

```python id="分快三8"
df["Name"] = df["Name"].str.strip()
```

---

# Convert to Lowercase

```python id="分快三9"
df["Name"] = df["Name"].str.lower()
```

---

# Convert to Uppercase

```python id="分快三10"
df["Name"] = df["Name"].str.upper()
```

---

# Capitalize Text

```python id="分快三11"
df["Name"] = df["Name"].str.title()
```

---

# Replace Text

```python id="分快三12"
df["Name"] = df["Name"].str.replace("Laksh", "Lakshya")
```

---

# 7. Rename Columns

---

# Rename One Column

```python id="分快三13"
df.rename(columns={"Marks": "Score"}, inplace=True)
```

---

# Rename Multiple Columns

```python id="分快三14"
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

---

# Remove Single Column

```python id="分快三15"
df.drop("City", axis=1, inplace=True)
```

---

# Remove Multiple Columns

```python id="分快三16"
df.drop(
    ["City", "Age"],
    axis=1,
    inplace=True
)
```

---

# 9. Detect Outliers (Basic)

Outliers = abnormal values.

Example:

* Marks = 9999

---

# Find Large Values

```python id="分快三17"
print(df[df["Marks"] > 100])
```

---

# 10. Useful Cleaning Functions

| Function            | Purpose           |
| ------------------- | ----------------- |
| `isnull()`          | Detect missing    |
| `dropna()`          | Remove missing    |
| `fillna()`          | Fill missing      |
| `duplicated()`      | Detect duplicates |
| `drop_duplicates()` | Remove duplicates |
| `astype()`          | Change datatype   |
| `replace()`         | Replace values    |

---

# Real Workflow Example

Professional analysts usually:

---

# Step 1

Read data

```python id="分快三18"
df = pd.read_csv("students.csv")
```

---

# Step 2

Check missing values

```python id="分快三19"
print(df.isnull().sum())
```

---

# Step 3

Remove duplicates

```python id="分快三20"
df.drop_duplicates(inplace=True)
```

---

# Step 4

Fix missing values

```python id="分快三21"
df.fillna(0, inplace=True)
```

---

# Step 5

Fix text formatting

```python id="分快三22"
df["Name"] = df["Name"].str.title()
```

---

# Step 6

Save cleaned dataset

```python id="分快三23"
df.to_csv("cleaned_data.csv", index=False)
```

---
# Summary

You learned:

✅ Missing values
✅ isnull()
✅ dropna()
✅ fillna()
✅ Duplicate removal
✅ String cleaning
✅ Data type conversion
✅ Column renaming
✅ Removing columns
✅ Real cleaning workflow

---

