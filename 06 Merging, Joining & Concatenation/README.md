# Topic 6: Merging, Joining & Concatenation in pandas

## Easy Explanation + Practical Coding

---

# Why This Topic is Important

In real-world projects:

- Data is usually stored in multiple files or tables.
- We often need to combine datasets.

### Examples

- Student details + Marks
- Customer information + Orders
- Employee data + Salary records

Pandas provides:

- `merge()`
- `join()`
- `concat()`

to combine data efficiently.

---

# Types of Combining Data

| Method | Purpose |
|----------|----------|
| `merge()` | Combine using common columns |
| `join()` | Combine using indexes |
| `concat()` | Stack DataFrames |

---

# 1. MERGE()

The most important method.

Think of it as:

## SQL JOIN in Pandas

---

# Example Datasets

## Student Information

```python
import pandas as pd

students = pd.DataFrame({
    "ID": [1, 2, 3],
    "Name": ["Laksh", "Aryan", "Parth"]
})

print(students)
```

### Output

```text
   ID   Name
0   1  Laksh
1   2  Aryan
2   3  Parth
```

---

## Student Marks

```python
marks = pd.DataFrame({
    "ID": [1, 2, 3],
    "Marks": [90, 85, 95]
})

print(marks)
```

### Output

```text
   ID  Marks
0   1     90
1   2     85
2   3     95
```

---

# Merge DataFrames

```python
result = pd.merge(students, marks, on="ID")

print(result)
```

### Output

```text
   ID   Name  Marks
0   1  Laksh     90
1   2  Aryan     85
2   3  Parth     95
```

---

# Understanding `on="ID"`

Pandas combines rows where:

## IDs match

---

# INNER JOIN (Default)

Only matching data is kept.

### Example

```python
students = pd.DataFrame({
    "ID": [1, 2, 3],
    "Name": ["Laksh", "Aryan", "Parth"]
})

marks = pd.DataFrame({
    "ID": [1, 2],
    "Marks": [90, 85]
})

print(pd.merge(students, marks, on="ID"))
```

### Output

```text
   ID   Name  Marks
0   1  Laksh     90
1   2  Aryan     85
```

### Explanation

- ID 3 is removed because it has no matching row.

---

# LEFT JOIN

Keep all rows from the left DataFrame.

### Example

```python
print(
    pd.merge(
        students,
        marks,
        on="ID",
        how="left"
    )
)
```

### Output

```text
   ID   Name  Marks
0   1  Laksh   90.0
1   2  Aryan   85.0
2   3  Parth    NaN
```

### Explanation

- All students are kept.
- Missing marks become `NaN`.

---

# RIGHT JOIN

Keep all rows from the right DataFrame.

### Example

```python
print(
    pd.merge(
        students,
        marks,
        on="ID",
        how="right"
    )
)
```

---

# OUTER JOIN

Keep all rows from both DataFrames.

### Example

```python
students = pd.DataFrame({
    "ID": [1, 2, 3],
    "Name": ["Laksh", "Aryan", "Parth"]
})

marks = pd.DataFrame({
    "ID": [2, 3, 4],
    "Marks": [85, 95, 88]
})

print(
    pd.merge(
        students,
        marks,
        on="ID",
        how="outer"
    )
)
```

### Output

```text
   ID   Name  Marks
0   1  Laksh    NaN
1   2  Aryan   85.0
2   3  Parth   95.0
3   4    NaN   88.0
```

---

# Visual Understanding

## Inner Join

```text
Common rows only
```

---

## Left Join

```text
All left rows + matching right rows
```

---

## Right Join

```text
All right rows + matching left rows
```

---

## Outer Join

```text
Everything from both tables
```

---

# Merge on Different Column Names

### Example

```python
students = pd.DataFrame({
    "Student_ID": [1, 2],
    "Name": ["Laksh", "Aryan"]
})

marks = pd.DataFrame({
    "ID": [1, 2],
    "Marks": [90, 85]
})

print(
    pd.merge(
        students,
        marks,
        left_on="Student_ID",
        right_on="ID"
    )
)
```

---

# Multiple Key Merge

### Example

```python
df1 = pd.DataFrame({
    "ID": [1, 1],
    "Subject": ["Math", "Science"]
})

df2 = pd.DataFrame({
    "ID": [1, 1],
    "Subject": ["Math", "Science"],
    "Marks": [90, 85]
})

print(
    pd.merge(
        df1,
        df2,
        on=["ID", "Subject"]
    )
)
```

---

# 2. JOIN()

Used mainly with indexes.

### Example

```python
df1 = pd.DataFrame({
    "Name": ["Laksh", "Aryan"]
}, index=[1, 2])

df2 = pd.DataFrame({
    "Marks": [90, 85]
}, index=[1, 2])

print(df1.join(df2))
```

### Output

```text
     Name  Marks
1  Laksh     90
2  Aryan     85
```

---

# Difference Between merge() and join()

| merge() | join() |
|----------|----------|
| Uses columns | Uses indexes |
| More flexible | Simpler |
| SQL-style joins | Index-based joins |

---

# 3. CONCAT()

Used to:

## Stack DataFrames

---

# Vertical Concatenation

### Example

```python
df1 = pd.DataFrame({
    "Name": ["Laksh", "Aryan"]
})

df2 = pd.DataFrame({
    "Name": ["Parth", "Riya"]
})

print(pd.concat([df1, df2]))
```

### Output

```text
    Name
0  Laksh
1  Aryan
0  Parth
1   Riya
```

---

# Reset Index

```python
print(
    pd.concat(
        [df1, df2],
        ignore_index=True
    )
)
```

### Output

```text
    Name
0  Laksh
1  Aryan
2  Parth
3   Riya
```

---

# Horizontal Concatenation

### Example

```python
df1 = pd.DataFrame({
    "Name": ["Laksh", "Aryan"]
})

df2 = pd.DataFrame({
    "Marks": [90, 85]
})

print(
    pd.concat(
        [df1, df2],
        axis=1
    )
)
```

### Output

```text
    Name  Marks
0  Laksh     90
1  Aryan     85
```

---

# Understanding axis

| axis | Meaning |
|------|----------|
| `axis=0` | Vertical |
| `axis=1` | Horizontal |

---

# Real-Life Examples

## Example 1

Combine:

- January Sales
- February Sales
- March Sales

using `concat()`.

---

## Example 2

Combine:

- Student Details
- Student Marks

using `merge()`.

---

## Example 3

Combine:

- Employee Data
- Salary Data

using `join()`.

---

# Common Mistakes

## Mistake 1: Wrong Column Name

### Wrong

```python
pd.merge(df1, df2, on="id")
```

### Actual Column

```text
ID
```

Column names are case-sensitive.

---

## Mistake 2: Forgetting `ignore_index=True`

Can result in duplicate indexes after concatenation.

---

## Mistake 3: Using `join()` Without Proper Indexes

`join()` works primarily on indexes. Incorrect indexes may produce unexpected results.

---

# Quick Comparison

| Feature | merge() | join() | concat() |
|----------|----------|----------|----------|
| Uses Common Columns | ✅ | ❌ | ❌ |
| Uses Index | Optional | ✅ | Optional |
| SQL-style Join | ✅ | Limited | ❌ |
| Stack DataFrames | ❌ | ❌ | ✅ |
| Most Common | ✅ | ⚪ | ✅ |

---

# Real-World Applications

These operations are heavily used in:

- Data Analytics
- Business Intelligence
- Machine Learning
- Financial Reporting
- E-commerce Dashboards
- HR Analytics
- Student Management Systems

---

# Summary

You learned:

✅ `merge()`

✅ Inner Join

✅ Left Join

✅ Right Join

✅ Outer Join

✅ `join()`

✅ `concat()`

✅ Vertical Concatenation

✅ Horizontal Concatenation

✅ Multiple Key Merge

✅ Real-world Data Combining

---

# Key Takeaway

**Most real-world datasets are split across multiple tables and files.**

To become proficient in Pandas, you must be comfortable with:

- `merge()` for combining related datasets
- `join()` for index-based combinations
- `concat()` for stacking DataFrames

These three functions are among the most frequently used tools in professional data analysis workflows.