# Missing Values

## What are Missing Values?

A missing value occurs when no data is stored for a feature in an observation.

Common representations:
- NaN
- ?
- N/A
- 0 (sometimes)
- Blank cell

---

# Ways to Handle Missing Values

## 1. Retrieve the Actual Value
- Contact the data source if possible.
- Best option when feasible.

---

## 2. Drop Missing Data

### Drop Rows
Use when:
- Only a few rows have missing values.
- Removing them won't significantly affect the dataset.

```python
df.dropna(axis=0, inplace=True)
```

### Drop Columns
Use when:
- A column contains too many missing values.
- The feature is not important.

```python
df.dropna(axis=1, inplace=True)
```

---

## 3. Replace Missing Values

Preferred when you don't want to lose data.

### Numerical Columns

Replace with:
- Mean (most common)
- Median (for skewed data)

```python
mean = df["column"].mean()
df["column"].replace(np.nan, mean, inplace=True)
```

---

### Categorical Columns

Replace with the most frequent value (Mode).

Example:

```
Gasoline
Gasoline
Diesel
Gasoline
NaN
```

↓

```
Gasoline
Gasoline
Diesel
Gasoline
Gasoline
```

---

## 4. Use Domain Knowledge

Estimate missing values using additional information.

Example:
- Older cars usually have higher losses.
- Replace based on similar old cars instead of the overall mean.

---

## 5. Leave Missing Values

Sometimes keeping NaN is acceptable if:
- The model can handle missing values.
- Missingness itself carries useful information.

---

# Pandas Functions

## Drop Missing Values

```python
df.dropna(axis=0, inplace=True)   # Drop rows
df.dropna(axis=1, inplace=True)   # Drop columns
```

---

## Replace Missing Values

```python
mean = df["normalized-losses"].mean()

df["normalized-losses"].replace(np.nan, mean, inplace=True)
```

---

# inplace=True

```python
df.dropna(inplace=True)
```

Changes the original DataFrame directly.

Without `inplace=True`:

```python
new_df = df.dropna()
```

The original DataFrame remains unchanged.

---

# Choosing a Strategy

| Situation | Recommended Action |
|-----------|--------------------|
| Few missing rows | Drop rows |
| Many missing rows | Replace values |
| Important numeric feature | Replace with Mean/Median |
| Categorical feature | Replace with Mode |
| Too many missing values in a column | Drop column |
| Better data available | Recollect data |
| Missingness is meaningful | Keep NaN |

---

# Key Takeaways

- Missing values reduce data quality.
- Dropping rows is best when only a few values are missing.
- Replacing values preserves more data.
- Use **Mean/Median** for numerical features.
- Use **Mode** for categorical features.
- Always choose the method based on the data and business problem.