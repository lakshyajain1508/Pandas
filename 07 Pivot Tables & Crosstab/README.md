# Topic 7: Pivot Tables & Crosstab in pandas

## Easy Explanation + Practical Coding

---

# What is a Pivot Table?

A Pivot Table is used to:

## Summarize data quickly.

It helps:

* Calculate totals
* Find averages
* Compare categories
* Create reports

Think of it like:

## Excel Pivot Table in Python

---

# Real Life Example

Suppose sales data:

| Product | City   | Sales |
| ------- | ------ | ----- |
| Laptop  | Mumbai | 50000 |
| Mobile  | Pune   | 30000 |
| Laptop  | Pune   | 45000 |

Now you want:

* Total sales city-wise
* Average sales product-wise

Pivot tables make this easy.

---

# Create Dataset

```python
import pandas as pd

data = {
    "Product": ["Laptop", "Mobile", "Laptop", "Tablet", "Mobile"],
    "City": ["Mumbai", "Pune", "Pune", "Mumbai", "Mumbai"],
    "Sales": [50000, 30000, 45000, 20000, 35000],
    "Quantity": [5, 10, 4, 3, 8]
}

df = pd.DataFrame(data)

print(df)
```

Output:

```python
   Product     City  Sales  Quantity
0   Laptop  Mumbai  50000         5
1   Mobile    Pune  30000        10
2   Laptop    Pune  45000         4
3   Tablet  Mumbai  20000         3
4   Mobile  Mumbai  35000         8
```

---

# Basic Pivot Table

---

# Average Sales by Product

```python
pivot = pd.pivot_table(
    df,
    values="Sales",
    index="Product"
)

print(pivot)
```

Output:

```python
          Sales
Product
Laptop   47500
Mobile   32500
Tablet   20000
```

Explanation:

* Laptop average sales:
  (50000 + 45000) / 2

---

# Understanding Parameters

| Parameter | Meaning              |
| --------- | -------------------- |
| `values`  | Column to calculate  |
| `index`   | Group rows           |
| `columns` | Create columns       |
| `aggfunc` | Aggregation function |

---

# Change Aggregation Function

Default:

```text
mean()
```

---

# Total Sales by Product

```python
pivot = pd.pivot_table(
    df,
    values="Sales",
    index="Product",
    aggfunc="sum"
)

print(pivot)
```

Output:

```python
          Sales
Product
Laptop    95000
Mobile    65000
Tablet    20000
```

---

# Multiple Aggregations

```python
pivot = pd.pivot_table(
    df,
    values="Sales",
    index="Product",
    aggfunc=["sum", "mean", "max"]
)

print(pivot)
```

Output:

```python
            sum   mean    max
          Sales  Sales  Sales
Product
Laptop    95000  47500  50000
Mobile    65000  32500  35000
Tablet    20000  20000  20000
```

---

# Using Columns Parameter

Creates Excel-like table.

---

# Sales by Product and City

```python
pivot = pd.pivot_table(
    df,
    values="Sales",
    index="Product",
    columns="City",
    aggfunc="sum"
)

print(pivot)
```

Output:

```python
City      Mumbai     Pune
Product
Laptop    50000   45000
Mobile    35000   30000
Tablet    20000      NaN
```

---

# Fill Missing Values

Replace NaN with 0.

```python
pivot = pd.pivot_table(
    df,
    values="Sales",
    index="Product",
    columns="City",
    aggfunc="sum",
    fill_value=0
)

print(pivot)
```

---

# Multiple Value Columns

```python
pivot = pd.pivot_table(
    df,
    values=["Sales", "Quantity"],
    index="Product",
    aggfunc="sum"
)

print(pivot)
```

Output:

```python
          Quantity   Sales
Product
Laptop          9   95000
Mobile         18   65000
Tablet          3   20000
```

---

# Multiple Indexes

```python
pivot = pd.pivot_table(
    df,
    values="Sales",
    index=["City", "Product"],
    aggfunc="sum"
)

print(pivot)
```

---

# Margins (Grand Total)

Adds totals automatically.

```python
pivot = pd.pivot_table(
    df,
    values="Sales",
    index="Product",
    aggfunc="sum",
    margins=True
)

print(pivot)
```

Output:

```python
           Sales
Product
Laptop     95000
Mobile     65000
Tablet     20000
All       180000
```

---

# Real Life Use Cases

Pivot tables are used for:

* Sales reports
* Business dashboards
* Student analytics
* Employee analysis
* Financial reports

---

# Example

---

# Total Salary by Department

```python
pd.pivot_table(
    employees,
    values="Salary",
    index="Department",
    aggfunc="sum"
)
```

---

# Average Marks by Class

```python
pd.pivot_table(
    students,
    values="Marks",
    index="Class",
    aggfunc="mean"
)
```

---

# Crosstab

Used for:

## Frequency tables

Shows:

* Counts
* Relationships between categories

---

# Example Dataset

```python
data = {
    "Gender": ["Male", "Female", "Male", "Female", "Male"],
    "Result": ["Pass", "Pass", "Fail", "Pass", "Fail"]
}

df = pd.DataFrame(data)

print(df)
```

Output:

```python
   Gender Result
0    Male   Pass
1  Female   Pass
2    Male   Fail
3  Female   Pass
4    Male   Fail
```

---

# Basic Crosstab

```python
print(
    pd.crosstab(
        df["Gender"],
        df["Result"]
    )
)
```

Output:

```python
Result  Fail  Pass
Gender
Female     0     2
Male       2     1
```

Explanation:

* Male Fail = 2
* Female Pass = 2

---

# Add Totals

```python
print(
    pd.crosstab(
        df["Gender"],
        df["Result"],
        margins=True
    )
)
```

Output:

```python
Result  Fail  Pass  All
Gender
Female     0     2    2
Male       2     1    3
All        2     3    5
```

---

# Normalize Crosstab

Shows percentages.

```python
print(
    pd.crosstab(
        df["Gender"],
        df["Result"],
        normalize=True
    )
)
```

---

# normalize Options

| Option      | Meaning            |
| ----------- | ------------------ |
| `True`      | Overall percentage |
| `"index"`   | Row percentage     |
| `"columns"` | Column percentage  |

---

# Row Percentage

```python
print(
    pd.crosstab(
        df["Gender"],
        df["Result"],
        normalize="index"
    )
)
```

---

# Difference Between GroupBy & Pivot Table

| GroupBy             | Pivot Table          |
| ------------------- | -------------------- |
| More flexible       | More summary-focused |
| Better for analysis | Better for reports   |
| Code-heavy          | Cleaner tables       |

---

# Difference Between Pivot Table & Crosstab

| Pivot Table         | Crosstab         |
| ------------------- | ---------------- |
| Numeric aggregation | Frequency counts |
| Uses values         | Uses categories  |
| More advanced       | Simpler          |

---

# Common Mistakes

---

# Mistake 1

Wrong aggregation:

```python
aggfunc="means"
```

Correct:

```python
aggfunc="mean"
```

---

# Mistake 2

Forgetting fill_value

Results in:

```text
NaN
```

---

# Mistake 3

Using pivot table without numeric values.

---


# Summary

You learned:

✅ pivot_table()

✅ values

✅ index

✅ columns

✅ aggfunc

✅ Multiple aggregations

✅ Crosstab

✅ Frequency tables

✅ Percentages

✅ Report generation

---
