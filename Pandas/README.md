

# Pandas (Python) – Learning Notes + Practice

    This folder contains my hands-on learning notes and practice scripts for **pandas**, the main Python library for working with **tables of data** (like Excel and CSV). I used pandas to load datasets, inspect columns, filter rows, clean messy values, handle missing data, work with dates/time series, summarize results with `groupby`, and export cleaned data.


    Core Objects: Series and DataFrame
    - **Series**: a single column of data
    - **DataFrame**: a full table (rows + columns)

    Loading and Saving Data (CSV/Excel)
    - df = pd.read_csv("students.csv")
    - df = pd.read_excel("Book1.xlsx")
    - df.to_csv("students_cleaned.csv", index=False, encoding="utf-8-sig")

    Inspecting Data (first steps for every dataset)
    - df.head(), df.tail(), df.shape, df.columns, df.dtypes, df.info(), df.describe(), df.isna().sum()

    Selecting Rows and Columns:
    - df["score"]
    - df[["name", "score"]]
    - df.loc[0, "score"]     # by label
    - df.iloc[0, 1]          # by position

    Filtering Rows (most used feature)
    - df[df["score"] >= 50]
    - df[(df["class"] == "SS1") & (df["score"] >= 50)]

    Creating and Updating Columns:
    - df["passed"] = df["score"] >= 50
    - df["score_plus_10"] = df["score"] + 10

    Convert text to numbers, then sort correctly:
    - clean = df["YearsCode"].replace({"Less than 1 year": "0", "More than 50 years": "51"})
    - df["YearsCode_num"] = pd.to_numeric(clean, errors="coerce")
    - df.sort_values(by=["Country", "YearsCode_num"], ascending=[True, False], inplace=True)

    Missing Values (NaN)    
    - df.isna().sum()
    - df = df.dropna()
    - df = df.fillna(0)
    - df["score"] = df["score"].fillna(df["score"].mean())



Mini Examples

## Data Cleaning Steps (Pandas)

    This section documents the exact cleaning operations applied to the dataset. The goal is to standardize messy text fields, convert mixed-type columns to proper numeric types, fix inconsistent date formats, handle outliers, and fill missing values in a consistent way.

---

# 1) Clean and Convert `YearsCode` to Numeric

    `YearsCode` contains a mix of numbers stored as strings and text values such as 'Less than 1 year' or 'More than 50 years'.  
    To make it usable for sorting, filtering, and analysis, we first map text values to numeric strings, then convert the column to numeric.

# 2) ClassLevel contains inconsistent casing and spacing (e.g., 'Jss2 ', 'ss1', 'SS-3').
    I strip spaces, convert to uppercase, and fix known inconsistencies


# 3) Parse Mixed Date Formats in Date

    The Date column contains multiple formats, so we use a two-pass conversion strategy:
    First pass: let pandas try to parse automatically
    Second pass: explicitly parse the format DD/MM/YYYY HH:MM AM/PM
    Then fill missing parsed values from the second pass


# 4) Clean MathScore and EnglishScore

    Scores can contain missing values and outliers (negative values or values above 100).
    We convert them to numeric, clamp them into a valid range of 0–100, then fill missing values with the column mean.

# 5) Standardize Country

    We remove extra spaces and normalize formatting (title case) so values like 'nigeria ' become 'Nigeria'.


# 6) Standardize Gender

    The Gender column includes messy values such as 'female ', ' MALE', "M", "F", and blanks.
    We strip spaces, uppercase everything, map full words to single-letter values, and convert blanks to missing (pd.NA).


# 7) Clean AttendancePct

    Attendance percentage should fall between 0 and 100.
    We convert to numeric, clip to the valid range, then fill missing values with the column mean.


# 8) Clean and Fix Age

    Age values may include outliers or missing values.
    We convert to numeric, set out-of-range values to NaN, then fill missing values with the median age.







## Weekly Resample Summary (Time-Series Aggregation)

    After cleaning the dataset (dates, scores, attendance, age, and YearsCode), I created a weekly summary table to understand performance trends over time.

    This step converts the raw row-level dataset (many records per day/hour) into a weekly report that contains:
    - Weekly average MathScore
    - Weekly average EnglishScore
    - Weekly average AttendancePct
    - Weekly average Age
    - Weekly average YearsCode
    - Number of records captured per week (`RowsInWeek`)

---

### Step 1: Keep Only Valid Dates
    Some rows contain invalid or missing date values (converted to `NaT` during parsing).  
    To avoid resampling errors and incorrect grouping, I drop rows where `Date` is missing.

    ```python
    dp_date = df.dropna(subset=['Date'])


