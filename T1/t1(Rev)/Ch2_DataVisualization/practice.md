# Practice Workbook: Chapter 2 (Data Visualization)

## Section A: Matplotlib Basics
**Q1: Multi-line Plot**
Plot two lists `y1 = [1, 2, 3]` and `y2 = [3, 2, 1]` against `x = [1, 2, 3]`. Use markers and different colors. Add a legend.
```python
import matplotlib.pyplot as plt
plt.plot(x, y1, marker='o', color='r', label='Line 1')
plt.plot(x, y2, marker='x', color='b', label='Line 2')
plt.legend()
plt.show()
```

**Q2: Histogram**
Generate a histogram for a column `df['age']` with 20 bins.
```python
plt.hist(df['age'], bins=20)
plt.title('Age Distribution')
plt.show()
```

---

## Section B: Seaborn Highlights
**Q3: Boxplot**
Create a boxplot to see how 'Total_Bill' varies across different 'Day's in the `tips` dataset.
```python
import seaborn as sns
sns.boxplot(x='day', y='total_bill', data=df)
```

**Q4: Count Plot**
Show the count of gender in each 'class' of passengers from a `titanic` dataset.
```python
sns.countplot(x='class', hue='sex', data=df)
```

---

## Section C: Heatmaps (Advanced)
**Q5: Correlation Matrix**
Calculate the correlation for a DataFrame `df` and visualize it using a heatmap with annotations and a 'YlGnBu' colormap.
```python
corr = df.corr()
sns.heatmap(corr, annot=True, cmap='YlGnBu')
```

---

## Section D: NetworkX (Graphs)
**Q6: Creating a Star Graph**
Create a graph where one center node (0) is connected to 4 other nodes (1, 2, 3, 4).
```python
import networkx as nx
G = nx.Graph()
G.add_edges_from([(0, 1), (0, 2), (0, 3), (0, 4)])
nx.draw(G, with_labels=True)
```

**Q7: Directed Connection**
In a directed graph, add an edge from 'User1' to 'User2'.
```python
DG = nx.DiGraph()
DG.add_edge('User1', 'User2')
```

### 7. Directed Graphs
**Task**: Create a directed graph with 3 nodes (X, Y, Z). Add edges X -> Y and Y -> Z. Draw the graph with large red nodes and visible arrows.

### 8. Interactive Pair Plots
**Task**: Use Plotly Express to create a `scatter_matrix` for 'Selling_Price', 'Present_Price', and 'Kms_Driven', colored by 'Fuel_Type'.

---

## Section E: Plotly
**Q8: Interactive Scatter**
Create an interactive scatter plot of 'Body_Mass' vs 'Flipper_Length' where hovering on a point shows the 'Species'.
```python
import plotly.express as px
fig = px.scatter(df, x='Flipper_Size', y='Body_Mass', hover_name='Species')
fig.show()
```
