# Data Formatting in Pandas

## What is Data Formatting?

Data formatting is the process of converting data into a **consistent format** so it can be analyzed correctly.

### Why is it important?

* Ensures consistency across the dataset.
* Makes statistical analysis reliable.
* Prevents errors during model training.
* Makes data easier to compare and understand.

---

# Common Data Formatting Problems

## 1. Inconsistent Text

The same value may be written in different ways.

Example:

```text
New York
NY
N.Y.
Ny
```

These all represent the same city but are treated as different values by a computer.

---

## 2. Different Units

The same measurement may use different units.

Example:

* Miles per gallon (MPG)
* Liters per 100 kilometers (L/100 km)

Before analysis, convert everything to a single unit.

Example:

```python
df["city-L/100km"] = 235 / df["city-mpg"]
```

---

## 3. Incorrect Data Types

Sometimes numbers are imported as text.

Example:

```text
Price

"15000"
"22000"
"18000"
```

Pandas may store these as **object** instead of **int** or **float**.

This can cause incorrect calculations and model errors.

---

# Check Data Types

Use:

```python
df.dtypes
```

Example Output:

```text
price      object
horsepower int64
city-mpg   float64
```

---

# Convert Data Types

Use `astype()`.

### Convert to Integer

```python
df["price"] = df["price"].astype("int")
```

### Convert to Float

```python
df["price"] = df["price"].astype("float")
```

### Convert to String

```python
df["price"] = df["price"].astype("str")
```

---

# Rename Columns

Use `rename()` to give columns meaningful names.

```python
df.rename(
    columns={
        "city-mpg": "city-L/100km"
    },
    inplace=True
)
```

---

# Common Pandas Methods

| Method      | Purpose               |
| ----------- | --------------------- |
| `df.dtypes` | Check data types      |
| `astype()`  | Convert data type     |
| `rename()`  | Rename columns        |
| `replace()` | Replace values        |
| `fillna()`  | Fill missing values   |
| `dropna()`  | Remove missing values |

---

# Data Types in Pandas

| Data Type    | Description      |
| ------------ | ---------------- |
| `object`     | Text/String      |
| `int64`      | Integer          |
| `float64`    | Decimal number   |
| `bool`       | True/False       |
| `datetime64` | Date & Time      |
| `category`   | Categorical data |

---

# Best Practices

* Check data types after loading a dataset.
* Keep text values consistent.
* Convert units to one standard.
* Rename confusing column names.
* Convert columns to the correct data type before analysis.
* Clean data before building ML models.

---

# Workflow

```text
Load Data
      ↓
Check Data Types
      ↓
Fix Missing Values
      ↓
Standardize Text
      ↓
Convert Units
      ↓
Convert Data Types
      ↓
Rename Columns
      ↓
Ready for EDA & Machine Learning
```

---

# Key Takeaways

* Data formatting makes datasets consistent and reliable.
* Standardize text values (e.g., "NY", "N.Y.", "New York").
* Convert measurements to a common unit.
* Use `df.dtypes` to inspect column types.
* Use `astype()` to convert data types.
* Use `rename()` to improve column names.
* Proper formatting is an essential step in data cleaning before EDA and machine learning.
