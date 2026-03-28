# Chapter 3: Machine Learning

## 1. Introduction to Machine Learning
Machine Learning (ML) is a subset of AI that allows systems to learn from data.

### Types of Learning
- **Supervised Learning:** Learning with labeled data (Inputs and Targets provided).
  - **Regression:** Predicting a continuous numeric value (e.g., Price, Salary).
  - **Classification:** Predicting a discrete category/class (e.g., Yes/No, Cat/Dog).
- **Unsupervised Learning:** Learning from unlabeled data (Finding patterns/clusters).

---

## 2. Feature Engineering & Preprocessing
Before training a model, data must be cleaned and transformed.

### A. Handling Categorical Data (Encoding)
1.  **Label Encoding:** Replacing categories with numbers (0, 1, 2...). Suitable for ordinal data.
2.  **One-Hot Encoding (Dummies):**
    - `pd.get_dummies(df, columns=[...], drop_first=True, dtype=int)`: Creating binary columns. `dtype=int` ensures 0 or 1 values.

### B. Feature Creation & Logic
- `df['New_Col'] = df['ColA'] + df['ColB']`: Simple arithmetic.
- `np.where(condition, if_true, if_false)`: Like Excel's IF.
    - Example: `df['Class'] = np.where(df['Price'] > 10, 'High', 'Low')`.

### C. Feature Selection
Removing columns using `df.drop(columns=[...])` before splitting.

---

## 3. Supervised Learning: Regression
Predicting quantitative values.

### Linear Regression
- **Concept:** Fits a straight line ($y = mx + c$) to the data.
- **Library:** `from sklearn.linear_model import LinearRegression`

### Steps to Train a Model
1.  **Define X and y:**
    ```python
    X = df[['Feature1', 'Feature2']] # Independent variables
    y = df['Target']                 # Dependent variable
    ```
2.  **Split Data:**
    ```python
    from sklearn.model_selection import train_test_split
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
    ```
3.  **Train:**
    ```python
    model = LinearRegression()
    model.fit(X_train, y_train)
    ```
4.  **Predict:**
    ```python
    predictions = model.predict(X_test)
    ```

---

## 4. Supervised Learning: Classification
Predicting categories.

### Logistic Regression
Despite the name, it is a **classification** algorithm. It uses the Sigmoid function to map predictions to probabilities between 0 and 1.

---

## 5. Evaluation Metrics (Full Table)

| Metric | Type | Formula/Description | Ideal Value |
|:-------|:-----|:--------------------|:------------|
| **MAE** | Regression | Mean Absolute Error (Average of absolute differences) | 0 |
| **MSE** | Regression | Mean Squared Error (Average of squared differences) | 0 |
| **RMSE** | Regression | Square root of MSE (Same unit as target) | 0 |
| **R² Score** | Regression | Coefficient of Determination (Variance explained) | 1 (or 100%) |
| **Accuracy** | Class. | Ratio of correct predictions to total predictions | 1 (or 100%) |
| **Conf. Matrix** | Class. | Table showing True Positives, True Negatives, etc. | High Diagonal |

**Evaluation Imports:**
- `from sklearn.metrics import mean_squared_error, r2_score` (Regression)
- `from sklearn.metrics import accuracy_score, confusion_matrix, classification_report` (Classification)

**Prediction Methods:**
- `model.predict(X_test)`: Returns class (e.g., 0 or 1).
- `model.predict_proba(X_test)`: Returns probabilities (e.g., [0.1, 0.9]) – useful for setting custom thresholds.
- `print(classification_report(y_test, predictions))`: Returns precision, recall, and f1-score for all classes.

---

## 6. Example Practice Questions

### Q1: Encoding
**Question:** You have a column 'Fuel_Type' with values ['Petrol', 'Diesel', 'CNG']. How do you encode this for a Linear Regression model in one line?
**Solution:**
```python
df_encoded = pd.get_dummies(df, columns=['Fuel_Type'], drop_first=True)
```

### Q2: Evaluation
**Question:** After training a Linear Regression model, how do you check how much variance is explained by the model?
**Solution:** Check the **R-Squared (R2) Score**.
```python
print(r2_score(y_test, predictions))
```

### Q3: Probability vs Class
**Question:** In Logistic Regression, what is the difference between `predict()` and `predict_proba()`?
**Solution:**
- `predict()` returns the class (e.g., 0 or 1).
- `predict_proba()` returns the probability of each class (e.g., [0.2, 0.8]).

---

## 7. Use Cases
- **Linear Regression:** Predicting house prices based on square footage.
- **Logistic Regression:** Predicting if an email is Spam or Not Spam.
- **MAE/RMSE:** Judging the accuracy of a weather forecasting model.
- **Confusion Matrix:** Analyzing types of errors in a medical diagnosis model (False positives vs False negatives).
