# Introduction to pandas

---

# What is Pandas?

Pandas is a powerful Python library used for:

* Data Analysis
* Data Manipulation
* Data Cleaning
* Handling CSV/Excel files
* Working with tables and datasets

Think of Pandas like **Excel inside Python** but much more powerful.

With Pandas, you can:

* Read huge datasets
* Filter information
* Clean messy data
* Analyze trends
* Prepare data for AI/ML

---

# Why Was Pandas Created?

Before Pandas, working with structured data in Python was difficult.

For example:

* Reading CSV files took more code
* Filtering rows was complex
* Handling missing data was hard

Pandas simplified all of this.

It was created by:
Wes McKinney

---

# Real Life Example

Imagine you own a coaching institute.

You have student data:

| Name  | Marks | City   |
| ----- | ----- | ------ |
| Laksh | 90    | Mumbai |
| Aryan | 85    | Pune   |
| Parth | 95    | Delhi  |

Now you want to:

* Find students with marks > 90
* Calculate average marks
* Sort students
* Save report to Excel

Pandas makes all this extremely easy.

---

# Why Companies Use Pandas

Companies use Pandas because data exists everywhere.

Examples:

* Netflix analyzes viewing data
* Amazon analyzes customer purchases
* Banks analyze transactions
* Hospitals analyze patient records

Pandas helps process this data quickly.

---

# Where Pandas is Used

## Data Science

Analyzing datasets

## Machine Learning

Preparing data before training AI models

## Web Analytics

User activity analysis

## Finance

Stock market analysis

## Research

Scientific datasets

## Business Intelligence

Reports and dashboards

---

# Installing Pandas

First install Python.

Then install Pandas:

```bash id="4x9zrd"
pip install pandas
```

Check version:

```python id="1y7h1o"
import pandas as pd

print(pd.__version__)
```

---

# Importing Pandas

```python id="3ocb4n"
import pandas as pd
```

Here:

* `pandas` = library name
* `pd` = short nickname

Almost every developer uses `pd`.

---

# Core Data Structures in Pandas

Pandas mainly has 2 important structures:

| Structure | Meaning       |
| --------- | ------------- |
| Series    | Single column |
| DataFrame | Full table    |

---
