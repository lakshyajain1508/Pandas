# Introduction to Pandas

---

# What is Pandas?

**Pandas** is a powerful Python library used for:

- Data Analysis
- Data Manipulation
- Data Cleaning
- Handling CSV and Excel files
- Working with tables and datasets

Think of Pandas as **Excel inside Python**, but much more powerful.

With Pandas, you can:

- Read huge datasets
- Filter information
- Clean messy data
- Analyze trends
- Prepare data for AI and Machine Learning

---

# Why Was Pandas Created?

Before Pandas, working with structured data in Python was difficult.

For example:

- Reading CSV files required more code
- Filtering rows was complex
- Handling missing data was difficult

Pandas simplified all of these tasks and made data analysis much easier.

### Creator

Pandas was created by **Wes McKinney**.

---

# Real-Life Example

Imagine you own a coaching institute.

You have student data:

| Name | Marks | City |
|------|------|------|
| Laksh | 90 | Mumbai |
| Aryan | 85 | Pune |
| Parth | 95 | Delhi |

Now you want to:

- Find students with marks greater than 90
- Calculate average marks
- Sort students by marks
- Save reports to Excel

Pandas makes all of these tasks extremely easy.

---

# Why Companies Use Pandas

Companies use Pandas because data exists everywhere.

### Examples

- Netflix analyzes viewing data
- Amazon analyzes customer purchases
- Banks analyze financial transactions
- Hospitals analyze patient records

Pandas helps process and analyze this data quickly and efficiently.

---

# Where Pandas is Used

## Data Science

Analyzing datasets and discovering insights.

---

## Machine Learning

Preparing and cleaning data before training AI models.

---

## Web Analytics

Analyzing user activity and website performance.

---

## Finance

Stock market analysis and financial reporting.

---

## Research

Working with scientific and experimental datasets.

---

## Business Intelligence

Creating reports, dashboards, and performance metrics.

---

# Installing Pandas

First, install Python.

Then install Pandas using:

```bash
pip install pandas
```

---

## Check Installed Version

```python
import pandas as pd

print(pd.__version__)
```

This displays the currently installed Pandas version.

---

# Importing Pandas

```python
import pandas as pd
```

### Explanation

- `pandas` = Library name
- `pd` = Short alias (nickname)

Almost every Python developer uses `pd` as the standard alias.

---

# Core Data Structures in Pandas

Pandas mainly provides two important data structures:

| Structure | Meaning |
|-----------|---------|
| Series | Single column of data |
| DataFrame | Complete table of data |

---

## Series

A **Series** is a one-dimensional labeled array.

Example:

```python
import pandas as pd

marks = pd.Series([90, 85, 95])

print(marks)
```

Output:

```text
0    90
1    85
2    95
dtype: int64
```

---

## DataFrame

A **DataFrame** is a two-dimensional table consisting of rows and columns.

Example:

```python
import pandas as pd

data = {
    "Name": ["Laksh", "Aryan", "Parth"],
    "Marks": [90, 85, 95]
}

df = pd.DataFrame(data)

print(df)
```

Output:

```text
    Name  Marks
0  Laksh     90
1  Aryan     85
2  Parth     95
```

---

# Why Learn Pandas?

Pandas is one of the most important libraries in the Python ecosystem because it helps you:

- Work with real-world datasets
- Clean messy data
- Perform statistical analysis
- Build Machine Learning projects
- Generate reports and dashboards
- Process millions of records efficiently

---

# Prerequisites

Before learning Pandas, it is helpful to know:

- Basic Python
- Lists
- Dictionaries
- Functions
- Loops and Conditions

---

# Summary

You learned:

✅ What Pandas is

✅ Why Pandas was created

✅ Real-world applications of Pandas

✅ Where Pandas is used

✅ How to install Pandas

✅ How to import Pandas

✅ Core data structures:
- Series
- DataFrame

✅ Why Pandas is important for Data Science and Machine Learning

---

# Key Takeaway

**Pandas is the foundation of data analysis in Python.**

Almost every Data Science, Data Analytics, and Machine Learning project starts with loading, cleaning, and analyzing data using Pandas.