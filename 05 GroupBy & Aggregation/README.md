# Topic 5: GroupBy & Aggregation in pandas

## Easy Explanation + Practical Coding

---

# What is GroupBy?

`groupby()` is used to:

## Group similar data together.

Then we can:

- Calculate average
- Find total
- Count values
- Find highest values
- Find lowest values

---

# Real-Life Example

Imagine school data:

| Name | City | Marks |
|------|------|------|
| Laksh | Mumbai | 90 |
| Aryan | Pune | 85 |
| Riya | Mumbai | 88 |

Now you want:

## Average marks city-wise

Like:

- Mumbai → Average marks
- Pune → Average marks

This is where `groupby()` is used.

---

# Create Dataset

```python
import pandas as pd

data = {
    "Name": ["Laksh", "Aryan", "Parth", "Riya", "Karan"],
    "City": ["Mumbai", "Pune", "Mumbai", "Delhi", "Pune"],
    "Marks": [90, 85, 95, 88, 92],
    "Age": [20, 21, 22, 19, 23]
}

df = pd.DataFrame(data)

print(df)
```

### Output

```text
    Name    City  Marks  Age
0  Laksh  Mumbai     90   20
1  Aryan    Pune     85   21
2  Parth  Mumbai     95   22
3   Riya   Delhi     88   19
4  Karan    Pune     92   23
```

---

# Basic GroupBy

## Group by City

```python
grouped = df.groupby("City")

print(grouped)
```

### Output

```text
<pandas.core.groupby.generic.DataFrameGroupBy object>
```

### Explanation

- Data is grouped internally.
- No calculation has been performed yet.

---

# View Groups

```python
print(grouped.groups)
```

### Output

```python
{
    'Delhi': [3],
    'Mumbai': [0, 2],
    'Pune': [1, 4]
}
```

### Explanation

- Mumbai group contains rows 0 and 2
- Pune group contains rows 1 and 4
- Delhi group contains row 3

---

# Aggregation Functions

Aggregation means:

## Performing calculations on groups.

---

# 1. mean() → Average

## Average Marks by City

```python
print(df.groupby("City")["Marks"].mean())
```

### Output

```text
City
Delhi     88.0
Mumbai    92.5
Pune      88.5
```

### Explanation

Mumbai Average:

```text
(90 + 95) / 2 = 92.5
```

---

# 2. sum()

## Total Marks by City

```python
print(df.groupby("City")["Marks"].sum())
```

### Output

```text
City
Delhi      88
Mumbai    185
Pune      177
```

---

# 3. count()

## Count Students in Each City

```python
print(df.groupby("City")["Name"].count())
```

### Output

```text
City
Delhi     1
Mumbai    2
Pune      2
```

---

# 4. max()

## Highest Marks by City

```python
print(df.groupby("City")["Marks"].max())
```

---

# 5. min()

## Lowest Marks by City

```python
print(df.groupby("City")["Marks"].min())
```

---

# 6. median()

```python
print(df.groupby("City")["Marks"].median())
```

---

# Multiple Aggregations

Instead of one calculation:

## Perform many calculations together.

### Example

```python
print(
    df.groupby("City")["Marks"]
      .agg(["mean", "sum", "max", "min"])
)
```

### Output

```text
         mean  sum  max  min
City
Delhi    88.0   88   88   88
Mumbai   92.5  185   95   90
Pune     88.5  177   92   85
```

---

# Group By Multiple Columns

## Example

```python
print(
    df.groupby(["City", "Age"])["Marks"].mean()
)
```

### Explanation

Groups data using both:

- City
- Age

---

# Select Multiple Columns

```python
print(
    df.groupby("City")[["Marks", "Age"]].mean()
)
```

### Output

```text
         Marks   Age
City
Delhi     88.0  19.0
Mumbai    92.5  21.0
Pune      88.5  22.0
```

---

# as_index=False

Normally grouped columns become indexes.

## Default Behavior

```python
print(df.groupby("City")["Marks"].mean())
```

---

## Keep Group Column as Normal Column

```python
print(
    df.groupby("City", as_index=False)["Marks"].mean()
)
```

### Output

```text
      City  Marks
0   Delhi   88.0
1  Mumbai   92.5
2    Pune   88.5
```

---

# sort=False

By default, groups are sorted alphabetically.

### Example

```python
print(
    df.groupby("City", sort=False)["Marks"].mean()
)
```

---

# size() vs count()

## size()

Counts all rows.

```python
print(df.groupby("City").size())
```

---

## count()

Counts only non-missing values.

```python
print(df.groupby("City")["Marks"].count())
```

---

# GroupBy with Conditions

## Students with Marks > 88

```python
filtered = df[df["Marks"] > 88]

print(
    filtered.groupby("City")["Marks"].mean()
)
```

---

# Iterating Through Groups

```python
grouped = df.groupby("City")

for city, data in grouped:
    print(city)
    print(data)
```

### Explanation

- `city` → Group name
- `data` → DataFrame of that group

---

# transform()

A very important advanced feature.

Used when:

## You want grouped calculations but keep the original DataFrame shape.

### Example

Add city-wise average marks.

```python
df["City Average"] = (
    df.groupby("City")["Marks"]
      .transform("mean")
)

print(df)
```

### Output

```text
    Name    City  Marks  Age  City Average
0  Laksh  Mumbai     90   20          92.5
1  Aryan    Pune     85   21          88.5
2  Parth  Mumbai     95   22          92.5
3   Riya   Delhi     88   19          88.0
4  Karan    Pune     92   23          88.5
```

---

# apply()

Allows custom functions.

### Example

```python
def bonus_marks(x):
    return x + 5

print(
    df.groupby("City")["Marks"]
      .apply(bonus_marks)
)
```

---

# Named Aggregation

Provides cleaner output.

### Example

```python
print(
    df.groupby("City").agg(
        Average_Marks=("Marks", "mean"),
        Total_Marks=("Marks", "sum"),
        Max_Marks=("Marks", "max")
    )
)
```

### Output

```text
         Average_Marks  Total_Marks  Max_Marks
City
Delhi             88           88         88
Mumbai          92.5          185         95
Pune            88.5          177         92
```

---

# Real-Life Use Cases

GroupBy is commonly used in:

- Sales reports
- Employee analytics
- IPL statistics
- E-commerce dashboards
- Financial analysis
- Student performance reports

---

# Example Real Analysis

## Total Sales by Product

```python
sales.groupby("Product")["Amount"].sum()
```

---

## Average Salary by Department

```python
employees.groupby("Department")["Salary"].mean()
```

---

# Common Mistakes

## Mistake 1

### Wrong

```python
df.groupby("City")["Marks", "Age"]
```

### Correct

```python
df.groupby("City")[["Marks", "Age"]]
```

---

## Mistake 2

Forgetting aggregation.

### Wrong

```python
df.groupby("City")
```

This only creates groups.

### Correct

```python
df.groupby("City").mean()
```

---

# Summary

You learned:

✅ `groupby()`

✅ `mean()`

✅ `sum()`

✅ `count()`

✅ `max()`

✅ `min()`

✅ Multiple aggregations

✅ `transform()`

✅ `apply()`

✅ Named aggregation

✅ Real-world usage

---

# Key Takeaway

**GroupBy is one of the most powerful features in Pandas.**

It allows you to summarize, analyze, and extract insights from large datasets efficiently and is widely used in Data Analytics, Business Intelligence, Data Science, and Machine Learning workflows.