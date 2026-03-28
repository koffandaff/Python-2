# Practice Workbook: Chapter 1 (Pandas)

## Section A: Data Exploration
**Q1: Loading Data**
Load a CSV file named `sales.csv` and display the last 10 rows.
```python
import pandas as pd
df = pd.read_csv('sales.csv')
print(df.tail(10))
```

**Q2: Summary Statistics**
How do you get the count, mean, std, min, and max for all numeric columns in a single command?
```python
df.describe()
```

---

## Section B: Filtering & Selection
**Q3: Specific Columns**
Given a DataFrame `df`, select only the columns 'Name' and 'Salary' where 'Salary' is greater than 50000.
```python
result = df[df['Salary'] > 50000][['Name', 'Salary']]
```

**Q4: Indexing**
Select the first 5 rows and the first 3 columns using an index-based method.
```python
df.iloc[:5, :3]
```

---

## Section C: Data Cleaning
**Q5: Null Values**
1. Count the number of null values in each column.
2. Fill all null values in the 'Age' column with the average age.
```python
# 1
print(df.isnull().sum())

# 2
df['Age'] = df['Age'].fillna(df['Age'].mean())
```

**Q6: Removing Data**
Drop the column named 'Address' permanently from the DataFrame.
```python
df.drop('Address', axis=1, inplace=True)
```

---

## Section D: Transformations
**Q7: Custom Functions**
Create a new column 'Tax' which is 10% of 'Salary'. Use the `.apply()` method.
```python
df['Tax'] = df['Salary'].apply(lambda x: x * 0.10)
```

**Q8: Aggregation**
Find the total 'Revenue' grouped by 'Category'.
```python
df.groupby('Category')['Revenue'].sum()
```

---

## Section E: Merging
**Q9: Concatenation**
Combine two DataFrames `df1` and `df2` vertically (stacking them).
```python
combined = pd.concat([df1, df2], axis=0)
```
