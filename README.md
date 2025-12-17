# Dirty Cafe Sales — Data Cleaning Pipeline

## Project Summary
This project focuses on cleaning a deliberately corrupted cafe sales dataset and producing a **logically consistent, model-ready CSV**.  
The emphasis is on **decision-driven data cleaning**, not blind imputation.

---

## Issues Identified & Solutions Applied

### 1. Duplicate Transactions
**Issue**
- Duplicate rows present despite unique transaction identifiers.

**Solution**
- Removed duplicates using `Transaction ID` as the primary key.

---

### 2. Missing Critical Fields
**Issue**
- Missing values in `Transaction ID`, `Item`, and `Transaction Date`.

**Solution**
- Dropped rows missing critical identifiers or dates.
- These fields are not imputable without introducing noise.

---

### 3. Inconsistent Categorical Values
**Issue**
- Categorical columns contained:
  - `None`, `UNKNOWN`, empty strings
  - Inconsistent casing and formatting

**Solution**
- Standardized text (trimmed whitespace, normalized casing).
- Replaced invalid or null-like values with `"Unknown"`.

---

### 4. Invalid Numerical Entries
**Issue**
- Non-numeric, zero, or negative values in:
  - `Quantity`
  - `Price Per Unit`

**Solution**
- Enforced numeric types.
- Removed invalid values.
- Filled missing quantities using **median**.
- Filled missing prices using **median per item** to preserve pricing logic.

---

### 5. Incorrect Derived Values
**Issue**
- `Total Spent` values did not always equal  
  `Quantity × Price Per Unit`.

**Solution**
- Ignored original `Total Spent`.
- Recomputed deterministically from cleaned numerical columns.

---

### 6. Invalid or Missing Dates
**Issue**
- Malformed or missing `Transaction Date` values.

**Solution**
- Parsed dates using strict datetime conversion.
- Dropped rows with invalid or missing dates.

---

### 7. Extreme Outliers
**Issue**
- Nonsensical extreme values affecting distributions.

**Solution**
- Applied conservative IQR-based outlier removal.
- Preserved legitimate bulk transactions.

---

### 8. Feature Engineering
**Enhancement**
- Extracted time-based features:
  - Day
  - Month
  - Weekday

---

## Output
- **Cleaned dataset:** `clean_cafe_sales.csv`
- Suitable for:
  - Machine learning
  - EDA
  - Business analytics

---

## Original Dataset
- **Source:** Kaggle  
- **Link:** https://www.kaggle.com/datasets/ahmedmohamed2003/cafe-sales-dirty-data-for-cleaning-training?resource=download
---

## Tech Stack
- Python
- Pandas
- NumPy
- Google Colab
- Git & GitHub
