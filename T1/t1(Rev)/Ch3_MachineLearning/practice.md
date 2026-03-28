# Practice Workbook: Chapter 3 (Machine Learning)

## Section A: Data Preprocessing
**Q1: One-Hot Encoding**
Your DataFrame `df` has categorical columns 'City' and 'Gender'. Convert them into dummy variables while avoiding the dummy trap.
```python
df = pd.get_dummies(df, columns=['City', 'Gender'], drop_first=True)
```

**Q2: Train-Test Split**
Split your input features `X` and target `y` into 70% training and 30% testing sets. Use `random_state=1` for reproducibility.
```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=1)
```

---

## Section B: Linear Regression (Regression)
**Q3: Model Training**
Initialize and train a Linear Regression model on `X_train` and `y_train`.
```python
from sklearn.linear_model import LinearRegression
model = LinearRegression()
model.fit(X_train, y_train)
```

**Q4: Performance Metrics**
Calculate the MSE and R2 score for the model predictions.
```python
from sklearn.metrics import mean_squared_error, r2_score
y_pred = model.predict(X_test)
print("MSE:", mean_squared_error(y_test, y_pred))
print("R2 Score:", r2_score(y_test, y_pred))
```

### 6. Conditional Logic
**Task**: Use `np.where` to create a new column 'Budget' where cars with 'Selling_Price' < 5 are labeled 'Low' and others 'High'.

### 7. Evaluation Mastery
**Task**: After training your classifier, print the `classification_report`. Which class has the lowest Recall? What does that mean for your model?

---

## Section C: Logistic Regression (Classification)
**Q5: Confusion Matrix**
Generate and print a confusion matrix for a trained Logistic Regression model.
```python
from sklearn.metrics import confusion_matrix
cm = confusion_matrix(y_test, y_pred)
print(cm)
```

**Q6: Classification Report**
Why is a `classification_report` useful?
**Answer:** It provides a detailed breakdown of Precision, Recall, and F1-Score for each class, which is vital when classes are imbalanced.

---

## Section D: Concepts & Logic
**Q7: Overfitting**
What does it mean if your R2 score is 0.99 on the training set but 0.45 on the test set?
**Answer:** The model is **overfitting**. It has learned the training data (including noise) so well that it fails to generalize to new, unseen data.

**Q8: Feature Selection**
How does a correlation heatmap help in the ML pipeline?
**Answer:** It identifies features that are highly correlated with the target (important predictors) and features that are highly correlated with each other (redundancy/multicollinearity).
