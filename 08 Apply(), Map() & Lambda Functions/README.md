# Topic 8: Apply(), Map() & Lambda Functions in pandas

## Easy Explanation + Practical Coding

---

# Why This Topic is Important

These functions are used for:

* Custom calculations
* Data transformation
* Cleaning columns
* Automation
* Feature engineering

Very heavily used in:

* Data Science
* Machine Learning
* Analytics

---

# Three Important Functions

| Function  | Use                       |
| --------- | ------------------------- |
| `map()`   | Works on Series           |
| `apply()` | Works on Series/DataFrame |
| `lambda`  | Short custom function     |

---

# Create Dataset

```python id="apply1"
import pandas as pd

data = {
    "Name": ["Laksh", "Aryan", "Parth"],
    "Marks": [90, 85, 95]
}

df = pd.DataFrame(data)

print(df)
```

Output:

```python id="apply2"
    Name  Marks
0  Laksh     90
1  Aryan     85
2  Parth     95
```

---

# 1. map()

Used mainly:

## On single column (Series)

---

# Example 1: Add Bonus Marks

```python id="map1"
df["Marks"] = df["Marks"].map(lambda x: x + 5)

print(df)
```

Output:

```python id="map2"
    Name  Marks
0  Laksh     95
1  Aryan     90
2  Parth    100
```

Explanation:

* Each mark increased by 5.

---

# Understanding Lambda

---

# Normal Function

```python id="lambda1"
def add_five(x):
    return x + 5
```

---

# Lambda Version

```python id="lambda2"
lambda x: x + 5
```

Meaning:

* Take `x`
* Add 5
* Return result

---

# Example 2: Convert to Grades

```python id="map3"
grades = {
    95: "A",
    90: "B",
    100: "A+"
}

df["Grade"] = df["Marks"].map(grades)

print(df)
```

Output:

```python id="map4"
    Name  Marks Grade
0  Laksh     95     A
1  Aryan     90     B
2  Parth    100    A+
```

---

# Example 3: Lowercase Names

```python id="map5"
df["Name"] = df["Name"].map(str.lower)

print(df)
```

Output:

```python id="map6"
    Name  Marks Grade
0  laksh     95     A
1  aryan     90     B
2  parth    100    A+
```

---

# Important Point

`map()` works:

## Column-wise only

Not whole DataFrame.

---

# 2. apply()

More powerful than map().

Can work:

* On columns
* On rows
* On entire DataFrame

---

# Example 1: Add 10 Marks

```python id="apply3"
df["Marks"] = df["Marks"].apply(lambda x: x + 10)

print(df)
```

---

# Example 2: Pass/Fail Column

```python id="apply4"
df["Result"] = df["Marks"].apply(
    lambda x: "Pass" if x >= 90 else "Fail"
)

print(df)
```

Output:

```python id="apply5"
    Name  Marks Grade Result
0  laksh    105     A   Pass
1  aryan    100     B   Pass
2  parth    110    A+   Pass
```

---

# Example 3: String Length

```python id="apply6"
df["Name Length"] = df["Name"].apply(len)

print(df)
```

Output:

```python id="apply7"
    Name  Name Length
0  laksh            5
1  aryan            5
2  parth            5
```

---

# apply() on Multiple Columns

---

# Example

```python id="apply8"
def total_info(row):
    return row["Name"] + " scored " + str(row["Marks"])

df["Info"] = df.apply(total_info, axis=1)

print(df)
```

Output:

```python id="apply9"
laksh scored 105
```

---

# Understanding axis

| axis   | Meaning     |
| ------ | ----------- |
| axis=0 | Column-wise |
| axis=1 | Row-wise    |

---

# Row-wise Example

```python id="apply10"
df.apply(lambda row: row["Marks"] + 5, axis=1)
```

---

# Column-wise Example

```python id="apply11"
df[["Marks"]].apply(sum, axis=0)
```

---

# 3. Lambda Functions

Lambda = short anonymous function.

---

# Syntax

```python id="lambda3"
lambda parameters: expression
```

---

# Example

```python id="lambda4"
lambda x: x * 2
```

Meaning:

* Input `x`
* Multiply by 2

---

# Normal Function vs Lambda

---

# Normal Function

```python id="lambda5"
def square(x):
    return x * x
```

---

# Lambda Function

```python id="lambda6"
lambda x: x * x
```

---

# Real Examples

---

# Square Marks

```python id="lambda7"
df["Square"] = df["Marks"].apply(
    lambda x: x * x
)

print(df)
```

---

# Even/Odd

```python id="lambda8"
df["Even"] = df["Marks"].apply(
    lambda x: "Yes" if x % 2 == 0 else "No"
)

print(df)
```

---

# Multiple Conditions

```python id="lambda9"
df["Category"] = df["Marks"].apply(
    lambda x:
        "Excellent" if x >= 100
        else "Good"
)

print(df)
```

---

# applymap()

Used:

## On entire DataFrame

---

# Example

```python id="applymap1"
numbers = pd.DataFrame({
    "A": [1, 2],
    "B": [3, 4]
})

print(
    numbers.applymap(lambda x: x * 10)
)
```

Output:

```python id="applymap2"
    A   B
0  10  30
1  20  40
```

---

# Difference Between map, apply, applymap

| Function     | Works On         |
| ------------ | ---------------- |
| `map()`      | Series only      |
| `apply()`    | Series/DataFrame |
| `applymap()` | Entire DataFrame |

---

# Real World Examples

---

# Example 1: Salary Bonus

```python id="real1"
employees["Salary"] = employees["Salary"].apply(
    lambda x: x + 5000
)
```

---

# Example 2: Product Category

```python id="real2"
products["Category"] = products["Price"].apply(
    lambda x:
        "Expensive" if x > 50000
        else "Affordable"
)
```

---

# Example 3: Clean Text

```python id="real3"
df["Name"] = df["Name"].apply(str.title)
```

---

# Performance Tip

Vectorized operations are faster.

---

# Slower

```python id="perf1"
df["Marks"].apply(lambda x: x + 5)
```

---

# Faster

```python id="perf2"
df["Marks"] + 5
```

---

# Use apply() When

Use when:

* Custom logic needed
* Multiple conditions
* Complex transformations

---

# Common Mistakes

---

# Mistake 1

Forgetting axis=1

Wrong:

```python id="mist1"
df.apply(function)
```

when row-wise needed.

Correct:

```python id="mist2"
df.apply(function, axis=1)
```

---

# Mistake 2

Using map() on DataFrame.

`map()` works only on Series.

---

# Mistake 3

Overusing apply() when vectorized operations exist.

---

# Summary

You learned:

✅ map()
✅ apply()
✅ applymap()
✅ lambda functions
✅ Row-wise operations
✅ Column-wise operations
✅ Custom transformations
✅ Real-world examples