# 📚 Student Data Analysis — 3-Part Project

A three-part data analysis project on a mystery student dataset. Covers **data cleaning**, **feature engineering**, **hypothesis testing**, and **gender-based visualization** to extract meaningful insights from student performance data.

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset](#-dataset)
- [Part A — Data Cleaning & Renaming](#-part-a--data-cleaning--renaming)
- [Part B — Feature Engineering](#-part-b--feature-engineering)
- [Part C — Hypothesis Testing & Visualization](#-part-c--hypothesis-testing--visualization)
- [Libraries Used](#️-libraries-used)
- [How to Run](#-how-to-run)
- [Project Structure](#-project-structure)

---

## 📌 Project Overview

This project analyzes student academic data in **3 structured parts**:

| Part | Task |
|---|---|
| **Part A** | Load dataset, rename columns, clean structure |
| **Part B** | Handle missing values, create TotalScore feature, find top 5 students |
| **Part C** | Hypothesis testing (t-test) + Gender-based score visualization |

---

## 📂 Dataset

- **File:** `mystery_data(in).csv`
- **Rows:** 99 students (IDs 101–200)
- **Columns (after renaming):**

| Column | Type | Description |
|---|---|---|
| `ID` | Numeric | Student ID (101–200) |
| `Maths` | Numeric | Math score |
| `Gender` | Categorical | M / F |
| `StudyHours` | Numeric | Weekly study hours |
| `Science` | Numeric | Science score |

---

## 🔵 Part A — Data Cleaning & Renaming

The raw CSV had no proper column headers. First row values were used as column names by default.

**Renamed columns:**

| Old Name | New Name |
|---|---|
| `101` | `ID` |
| `40` | `Maths` |
| `M` | `Gender` |
| `5.6` | `StudyHours` |
| `45` | `Science` |

```python
df_renamed = df.rename(columns={
    '101': 'ID', '40': 'Maths', 'M': 'Gender',
    '5.6': 'StudyHours', '45': 'Science'
})
```

✅ After renaming: 99 rows × 5 columns

---

## 🟡 Part B — Feature Engineering

### Step 1 — Handle Missing/Invalid StudyHours
- Converted `StudyHours` to numeric using `pd.to_numeric(errors='coerce')`
- Dropped rows where `StudyHours` was NaN
- Result: **98 valid rows** retained

### Step 2 — Create TotalScore Column
```python
df_renamed['TotalScore'] = df_renamed['Maths'] + df_renamed['Science']
```

### Step 3 — Top 5 Students by TotalScore

| ID | Maths | Gender | StudyHours | Science | TotalScore |
|---|---|---|---|---|---|
| 118 | 93 | M | 9.1 | 97 | **190** |
| 102 | 90 | M | 10.3 | 97 | **187** |
| 103 | 84 | F | 7.7 | 98 | **182** |
| 158 | 81 | M | 3.3 | 98 | **179** |
| 178 | 87 | F | 4.8 | 92 | **179** |

---

## 🔴 Part C — Hypothesis Testing & Visualization

### Hypothesis Test — One Sample T-Test

**Claim:** University claims average math score = **70**

**Question:** Do students who study **more than 10 hours/week** score significantly higher than 70?

**Hypotheses:**
- H₀ (Null): Mean math score of 10+ hour students = 70
- H₁ (Alternative): Mean math score of 10+ hour students > 70

**Method:** One-sample t-test (one-tailed)

**Results:**

| Metric | Value |
|---|---|
| T-Statistic | -1.099 |
| One-tailed P-value | 0.139 |
| Alpha (significance level) | 0.05 |

**Conclusion:**
> ❌ **No significant evidence** that students who study more than 10 hours/week score higher than 70 in Maths. P-value (0.139) > alpha (0.05), so we **fail to reject** the null hypothesis.

---

### Gender-Based Visualization — Box Plot

- **Chart Type:** Box Plot (Seaborn)
- **X-axis:** Gender (M / F)
- **Y-axis:** TotalScore

**Insights:**
1. Both male and female students show a similar median TotalScore, suggesting gender alone does not strongly influence overall academic performance.
2. Female students show a slightly wider spread in TotalScore, indicating more variability in performance compared to males.

---

## 🛠️ Libraries Used

```
pandas
numpy
matplotlib
seaborn
scipy (ttest_1samp)
```

---

## 🚀 How to Run

1. Clone the repository:
```bash
git clone https://github.com/hamza93-ai/Student-Data-Analysis.git
```

2. Open the notebook:
```bash
jupyter notebook student_data_analysis.ipynb
```

3. Place `mystery_data(in).csv` in the same folder and run all cells.

---

## 📁 Project Structure

```
Student-Data-Analysis/
│
├── student_data_analysis.ipynb   # Main notebook (Part A, B, C)
├── mystery_data(in).csv          # Raw dataset
└── README.md                     # Project documentation
```

---

## 👤 Author

**Hamza Asif**
