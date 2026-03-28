# Chapter 1: Data Analysis with Pandas

Pandas is the core library for data manipulation and analysis in Python. It provides high-performance, easy-to-use data structures.

## 1. Core Data Structures

### 1.1 Pandas Series
A 1D labeled array capable of holding any data type.
- **Creation**: `pd.Series(data, index=index, name="ColumnName")`
- **Attributes**:
    - `.index`: Labels of the series.
    - `.values`: Underlying data (numpy array).
    - `.dtype`: Data type of elements.
    - `.size`: Number of elements.

### 1.2 Pandas DataFrame
A 2D labeled data structure (tabular data).
- **Creation**: `pd.DataFrame(data, columns=column_names)`
- **Attributes**:
    - `.shape`: (rows, columns).
    - `.columns`: Column labels.
    - `.index`: Row labels.
    - `.dtypes`: Data types of each column.
    - `.T`: Transpose (swap rows and columns).

---

## 2. Data Exploration & Scanning

| Function | Parameters | Use Case | Example Question |
| :--- | :--- | :--- | :--- |
| `pd.read_csv()` | `filepath`, `index_col`, `usecols` | Load data from CSV file. | "How do you load only specific columns from a CSV?" |
| `.head(n)` | `n` (default 5) | View first $n$ rows. | "Check the top 10 entries of the dataset." |
| `.tail(n)` | `n` (default 5) | View last $n$ rows. | "Verify if the last row was loaded correctly." |
| `.info()` | None | Summary of types, non-null counts, and memory. | "How to check for data types and null counts in one go?" |
| `.describe()` | `include`, `exclude` | Statistical summary (mean, std, min, max, etc.). | "Get the mean, median, and 75th percentile of numerical data." |
| `.sample(n)` | `n` | Get $n$ random rows. | "Select 5 random samples from the dataframe." |
| `.nunique()` | `axis` | Count unique values in columns. | "Find out how many unique car names are in the dataset." |
| `.value_counts()` | `sort`, `ascending` | Count occurrences of unique values. | "Get the frequency of each fuel type." |
| `.duplicated().sum()` | None | Count total duplicated rows. | "Check if there are any repetitive records." |
| `.drop_duplicates()` | `inplace`, `keep` | Remove identical rows. | "Clean the dataset by removing duplicate entries." |
| `df.corr(numeric_only=True)` | `numeric_only` | Compute pairwise correlation of columns. | "Analyze the dependency between numeric features." |

---

## 3. Indexing & Slicing

### 3.1 Selection Types
1. **`.loc[]`**: Label-based selection. `.loc[row_label, col_label]`
2. **`.iloc[]`**: Integer-based (index) selection. `.iloc[row_idx, col_idx]`
3. **Boolean Indexing**: `df[df['col'] > value]`

**Example Use Cases:**
- `df.loc[0:10, 'Name']`: Rows 0 to 10 (inclusive) and column 'Name'.
- `df.iloc[0:10, 0:2]`: First 10 rows and first 2 columns (exclusive of upper bound).
- `df[df['Age'] > 25]`: Rows where Age is greater than 25.

---

## 4. Data Cleaning & Missing Values

| Function | Parameters | Description | Example Question |
| :--- | :--- | :--- | :--- |
| `.isna()` | None | Returns True for null values. | "Identify rows with missing information." |
| `.isnull().sum()` | None | Count of nulls per column. | "Find the total number of missing values in each column." |
| `.dropna()` | `axis`, `how`, `thresh`, `subset`, `inplace` | Remove missing values. | "Remove rows where 'Price' is null." |
| `.fillna()` | `value`, `method`, `axis`, `inplace` | Replace nulls with specific values (mean, median). | "Replace missing age values with the median age." |
| `.replace()` | `to_replace`, `value` | Replace specific values with others. | "Change 'Unknown' strings to 'NaN'." |
| `.drop()` | `labels`, `axis`, `inplace` | Remove columns or rows. | "Drop the 'Car_Name' column from the dataframe." |
| `.rename()` | `columns={'old': 'new'}` | Change column or index names. | "Rename 'Present_Price' to 'ExShowroomPrice'." |

---

## 5. Advanced Operations

### 5.1 Sorting
- `df.sort_values(by='col', ascending=True)`: Sort by specific column.
- `df.sort_index()`: Sort by index labels.
- `df.reset_index(drop=True)`: Reset row index (common after sorting).

### 5.2 Function Mapping & Aggregation
- `.apply(func)`: Apply a function (often `lambda`) to columns.
- `.groupby('col')['val'].agg(['mean', 'count', 'max'])`: Multi-function aggregation in one step.

### 5.3 Categorical to Numerical
- `pd.get_dummies(df, columns=['Col'], drop_first=True, dtype=int)`: One-Hot Encoding. `dtype=int` forces 0/1 instead of Bool.

---

## 6. Combining Datasets

| Method | Parameters | Description | Use Case |
| :--- | :--- | :--- | :--- |
| `pd.concat()` | `objs`, `axis`, `join`, `ignore_index` | Stacks dataframes vertically (axis=0) or horizontally (axis=1). | Combining data from different months. |
| `pd.merge()` | `on`, `how` (left, right, inner, outer) | SQL-like join on common keys. | Linking User details with their Orders. |

---

## 7. Outlier Detection (Concept)

### The IQR Method (Interquartile Range)
1. **Calculate Q1 (25th)** and **Q3 (75th)** percentiles: `df['col'].quantile(0.25)`
2. **IQR** = Q3 - Q1
3. **Lower Bound** = Q1 - 1.5 * IQR
4. **Upper Bound** = Q3 + 1.5 * IQR
5. **Filter**: `df[(df['col'] < Lower) | (df['col'] > Upper)]` identifies outliers.
