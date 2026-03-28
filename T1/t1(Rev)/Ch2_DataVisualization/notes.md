# Chapter 2: Data Visualization & Graph Theory

## 1. Overview
Data visualization is the graphical representation of information and data. In Python, we primarily use **Matplotlib** for basic plotting and **Seaborn** for high-level statistical graphics. For interactive plots, we use **Plotly**, and for graph/network analysis, we use **NetworkX**.

---

## 2. Matplotlib & Seaborn Basics

### Core Functions Table
| Module | Function | Description | Key Parameters |
|:-------|:---------|:------------|:---------------|
| `plt` | `plot(x, y)` | Line plot | `color`, `marker`, `linestyle`, `linewidth` |
| `plt` | `scatter(x, y)` | Scatter plot | `c` (color), `s` (size), `alpha` |
| `plt` | `bar(x, height)` | Vertical bar chart | `width`, `color`, `edgecolor` |
| `plt` | `hist(x)` | Histogram | `bins`, `range`, `density` |
| `plt` | `pie(x)` | Pie chart | `labels`, `autopct`, `explode` |
| `sns` | `scatterplot()` | Relationship plot | `hue`, `style`, `size`, `data` |
| `sns` | `lineplot()` | Line plot with error bands | `hue`, `style`, `markers`, `data` |
| `sns` | `boxplot()` | Box and whisker plot | `x`, `y`, `hue`, `data`, `orient` |
| `sns` | `countplot()` | Show counts of observations | `x`, `hue`, `palette`, `data` |

### Chart Customization Reference
- `plt.title("Title")`: Adds a title.
- `plt.xlabel("X Label")` / `plt.ylabel("Y Label")`: Adds axis labels.
- `plt.legend()`: Shows legend (requires `label` parameter in plot functions).
- `plt.grid(True)`: Adds grid lines.
- `plt.figure(figsize=(width, height))`: Sets dimensions of the plot.
- `plt.xticks(rotation=45)`: Rotates x-axis labels.

---

## 3. Seaborn Heatmaps (Master Reference)
`sns.heatmap(data, ...)` is used to visualize matrices (like correlation matrices).

### Parameter Table
| Parameter | Type | Description | Use Case |
|:----------|:-----|:------------|:---------|
| `data` | Matrix | 2D dataset or correlation matrix (`df.corr()`) | Data source |
| `vmin`, `vmax` | Float | Anchors for the colormap | Set color range boundaries |
| `cmap` | String | Color palette (e.g., 'viridis', 'magma', 'coolwarm') | Visual aesthetic |
| `annot` | Bool | If `True`, writes values in each cell | Show exact correlation values |
| `fmt` | String | String formatting code (e.g., `.2f`) | Control decimal places |
| `linewidths` | Float | Width of the lines that divide cells | Aesthetic spacing |
| `linecolor` | Color | Color of the lines dividing cells | Contrast |
| `cbar` | Bool | Whether to show the color bar | Remove distraction |
| `mask` | Matrix | Data to hide (usually the upper triangle) | Clean up diagonal duplicates |

**Example Snippet:**
```python
corr = df.corr()
sns.heatmap(corr, annot=True, cmap='coolwarm', fmt='.2f', vmin=-1, vmax=1)
plt.show()
```

---

## 4. NetworkX (Graph Theory)
Used for creating, manipulating, and studying the structure of complex networks.

### Graph Types
- `nx.Graph()`: Undirected graph (connections flow both ways).
- `nx.DiGraph()`: Directed graph (arrows indicating direction).

### NetworkX
- **Methods**:
    - `G.add_edge('A', 'B')`: Add single edge.
    - `G.add_edges_from([('A', 'B'), ('B', 'C')])`: Add multiple edges from list.
    - `nx.draw(G, with_labels=True, node_color='red', arrows=True, arrowsize=20)`: Visualize graph. Use `arrows=True` for directed graphs.
- `nx.draw_networkx(G)`: Advanced visualization with arrow styles.

**Arrow Style Tip:** Use `arrowstyle='->'` or `'-|>'` in `nx.draw` for directed graphs.

---

## 5. Plotly (Interactive Charts)
Plotly allows for zooming, hovering, and interactive exploration.

### Plotly Express (`px`)
- **Key Plots**:
    - `px.scatter(df, x, y, color, facet_col='category')`: Interactive scatter. `facet_col` creates sub-plots side-by-side.
    - `px.bar(df, x, y, barmode='group')`: Interactive bar charts.
    - `px.scatter_matrix(df, dimensions=['A', 'B', 'C'])`: Pair plot equivalent.
    - `px.histogram(...)`

---

## 6. Example Practice Questions

### Q1: Compare Variables
**Question:** Given a dataset `cars.csv`, create a scatter plot of `Horsepower` (X) vs `MPG` (Y), differentiated by `Origin` (Color/Hue).
**Solution:**
```python
import seaborn as sns
import matplotlib.pyplot as plt
sns.scatterplot(x='Horsepower', y='MPG', hue='Origin', data=df)
plt.title('Horsepower vs MPG')
plt.show()
```

### Q2: Correlation Analysis
**Question:** Visualize the correlation between all numeric columns using a heatmap. Annotate values and use a 'magma' color scheme.
- `sns.barplot(x, y, data)`: Aggregate data and show as bars.
- `sns.countplot(x, data, hue)`: Count occurrences of a category. `hue` adds a sub-category.
- `sns.boxplot(data=df[['Col1', 'Col2']])`: Distribution/Outliers for multiple columns.
- `sns.heatmap(df.corr(), annot=True, cmap='coolwarm')`: Correlation matrix visualization.
**Solution:**
```python
sns.heatmap(df.corr(), annot=True, cmap='magma')
```

### Q3: Network Representation
**Question:** Create a directed graph with nodes A, B, and C where A points to B, and B points to C. Visualize with labels.
**Solution:**
```python
import networkx as nx
G = nx.DiGraph()
G.add_edges_from([('A', 'B'), ('B', 'C')])
nx.draw(G, with_labels=True, arrowstyle='->', arrowsize=20)
```

---

## 7. Use Cases
- **Box Plot:** Finding outliers in price or salary data.
- **Histogram:** Understanding the distribution (frequency) of age or grades.
- **Heatmap:** Feature selection in ML by finding highly correlated variables.
- **Network Graph:** Representing social media followers or flight routes.
- **Pie Chart:** Visualizing market share of different brands.
