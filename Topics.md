# Complete pandas Roadmap

## Beginner → Advanced Topics

---

# 1. Beginner Level

Learn the foundation first.

## Introduction

* What is Pandas?
* Why use Pandas?
* Installing Pandas
* Importing Pandas

```python
import pandas as pd
```

---

## Series

* Creating Series
* Indexing
* Accessing values
* Operations on Series

```python
s = pd.Series([1, 2, 3])
```

---

## DataFrame Basics

* Creating DataFrame
* Rows and Columns
* Selecting columns
* Adding columns
* Deleting columns

```python
df = pd.DataFrame(data)
```

---

## Reading Files

* `read_csv()`
* `read_excel()`
* `read_json()`

---

## Writing Files

* `to_csv()`
* `to_excel()`
* `to_json()`

---

## Viewing Data

* `head()`
* `tail()`
* `sample()`
* `shape`
* `columns`
* `dtypes`
* `info()`
* `describe()`

---

## Selecting Data

* Single column
* Multiple columns
* Rows using `loc[]`
* Rows using `iloc[]`

---

## Filtering Data

* Conditions
* Multiple conditions
* Boolean indexing

```python
df[df["Age"] > 18]
```

---

## Sorting

* `sort_values()`
* `sort_index()`

---

## Renaming

* Columns rename
* Index rename

---

# 2. Intermediate Level

Now start real data analysis.

---

## Missing Data Handling

* `isnull()`
* `notnull()`
* `dropna()`
* `fillna()`

---

## Duplicate Data

* `duplicated()`
* `drop_duplicates()`

---

## String Operations

* `str.lower()`
* `str.upper()`
* `str.contains()`
* `str.replace()`

---

## Data Cleaning

* Removing spaces
* Fixing formats
* Changing data types

```python
df["Age"] = df["Age"].astype(int)
```

---

## Apply Functions

* `apply()`
* Lambda functions

```python
df["Age"].apply(lambda x: x + 1)
```

---

## GroupBy Operations

* `groupby()`
* Aggregation
* Mean
* Sum
* Count

---

## Aggregation Functions

* `mean()`
* `median()`
* `mode()`
* `sum()`
* `count()`
* `min()`
* `max()`

---

## Merging Data

* `merge()`
* `concat()`
* `join()`

---

## Indexing

* Setting index
* Resetting index
* Multi-index

---

## Date & Time Handling

* `to_datetime()`
* Extract year/month/day
* Time filtering

---

## Value Counts

* `value_counts()`
* Unique values

---

## Pivot Tables

* `pivot_table()`

---

## Crosstab

* `pd.crosstab()`

---

# 3. Advanced Level

Now you work like a real data analyst/data scientist.

---

## Advanced Indexing

* Multi-level indexing
* Hierarchical indexing

---

## Window Functions

* Rolling averages
* Expanding windows

```python
df["Sales"].rolling(3).mean()
```

---

## Time Series Analysis

* Resampling
* Shifting
* Lag features
* Moving averages

---

## Advanced Grouping

* Multiple aggregations
* Custom aggregations

---

## Performance Optimization

* Vectorization
* Efficient memory usage
* Category dtype

---

## Large Dataset Handling

* Chunking large CSVs
* Memory optimization

```python
pd.read_csv("file.csv", chunksize=1000)
```

---

## Advanced Apply

* Custom functions
* Complex transformations

---

## Reshaping Data

* `melt()`
* `stack()`
* `unstack()`
* `explode()`

---

## MultiIndex Operations

* Slice MultiIndex
* Swap levels

---

## Statistical Analysis

* Correlation
* Covariance
* Standard deviation

---

## Integration with Other Libraries

* NumPy
* Matplotlib
* Seaborn
* Scikit-learn

---

## Data Visualization

Using:

* Matplotlib
* Seaborn

---

## Real-world Projects

* Sales dashboard
* IPL analysis
* Netflix data analysis
* Expense tracker
* COVID data analysis
* Stock market analysis

---

# 4. Expert Level (Optional)

---

## Method Chaining

```python
(
    df.dropna()
      .groupby("City")
      .mean()
)
```

---

## Custom Pipelines

* Reusable cleaning systems
* ETL workflows

---

## SQL + Pandas

* SQL integration
* Query optimization

---

## Machine Learning Preprocessing

* Feature engineering
* Encoding
* Scaling
* Train/test preparation

---

# Best Learning Order

## Phase 1

* Series
* DataFrame
* CSV handling
* Filtering

## Phase 2

* Cleaning
* GroupBy
* Missing values
* Merging

## Phase 3

* Time series
* Pivot tables
* Advanced indexing

## Phase 4

* Real projects
* Visualization
* ML preprocessing

---

# Best Datasets for Practice

* Titanic Dataset
* Netflix Dataset
* IPL Dataset
* COVID Dataset
* Sales Dataset
* Student Dataset

---

# Recommended Mini Projects

## Beginner

* Student marks analyzer
* Expense tracker

## Intermediate

* Sales dashboard
* IPL stats analyzer

## Advanced

* Stock market analysis
* Real-time analytics dashboard

---

# Final Goal

After mastering Pandas, you can move to:

* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* AI & Machine Learning
* Data Science
* Analytics Engineering
