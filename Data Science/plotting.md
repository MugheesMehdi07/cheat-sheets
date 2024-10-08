Here’s a **Plotting Cheat Sheet** for both **Matplotlib** and **Seaborn**. This will cover a wide range of plotting functionalities commonly used for data visualization.

```
## 1. Plotting Cheat Sheet

### a. Importing Libraries
```python
import matplotlib.pyplot as plt
import seaborn as sns
```

---

### 2. Matplotlib Cheat Sheet

### a. Basic Plotting

- **Line Plot**:
    ```python
    x = [1, 2, 3, 4]
    y = [10, 20, 25, 30]
    plt.plot(x, y)
    plt.xlabel('X-axis label')
    plt.ylabel('Y-axis label')
    plt.title('Line Plot Title')
    plt.show()
    ```

- **Scatter Plot**:
    ```python
    plt.scatter(x, y)
    plt.xlabel('X-axis label')
    plt.ylabel('Y-axis label')
    plt.title('Scatter Plot Title')
    plt.show()
    ```

- **Bar Plot**:
    ```python
    categories = ['A', 'B', 'C']
    values = [3, 7, 2]
    plt.bar(categories, values)
    plt.xlabel('Categories')
    plt.ylabel('Values')
    plt.title('Bar Plot Title')
    plt.show()
    ```

- **Histogram**:
    ```python
    data = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
    plt.hist(data, bins=4)
    plt.xlabel('Value')
    plt.ylabel('Frequency')
    plt.title('Histogram Title')
    plt.show()
    ```

- **Pie Chart**:
    ```python
    labels = ['A', 'B', 'C']
    sizes = [20, 30, 50]
    plt.pie(sizes, labels=labels, autopct='%1.1f%%')
    plt.title('Pie Chart Title')
    plt.show()
    ```

---

### b. Customizing Plots

- **Adding Grid**:
    ```python
    plt.plot(x, y)
    plt.grid(True)
    plt.show()
    ```

- **Changing Line Styles**:
    ```python
    plt.plot(x, y, linestyle='--', color='r', marker='o')
    plt.show()
    ```

- **Subplots**:
    ```python
    plt.subplot(2, 1, 1)  # 2 rows, 1 column, plot 1
    plt.plot(x, y)
    
    plt.subplot(2, 1, 2)  # 2 rows, 1 column, plot 2
    plt.bar(categories, values)
    
    plt.show()
    ```

- **Setting Axis Limits**:
    ```python
    plt.plot(x, y)
    plt.xlim(0, 5)  # X-axis range
    plt.ylim(0, 35)  # Y-axis range
    plt.show()
    ```

---

### c. Advanced Matplotlib

- **Logarithmic Scale**:
    ```python
    plt.plot(x, y)
    plt.yscale('log')  # Set Y-axis to logarithmic scale
    plt.show()
    ```

- **Dual Axes**:
    ```python
    fig, ax1 = plt.subplots()

    ax2 = ax1.twinx()  # Create a second y-axis
    ax1.plot(x, y, 'g-')
    ax2.plot(x, y, 'b-')

    ax1.set_xlabel('X data')
    ax1.set_ylabel('Y1 data', color='g')
    ax2.set_ylabel('Y2 data', color='b')
    plt.show()
    ```

- **Annotations**:
    ```python
    plt.plot(x, y)
    plt.annotate('Important Point', xy=(2, 25), xytext=(3, 30),
                 arrowprops=dict(facecolor='black', arrowstyle='->'))
    plt.show()
    ```

---

### d. Saving Plots
- **Save Figure**:
    ```python
    plt.plot(x, y)
    plt.savefig('plot.png', dpi=300)  # Save plot as PNG with 300 dpi
    ```

---

### e. Styling in Matplotlib

- **Available Styles**:
    ```python
    plt.style.use('ggplot')  # Example of using 'ggplot' style
    plt.plot(x, y)
    plt.show()
    ```

- **Available Style List**:
    ```python
    plt.style.available  # Returns list of available styles
    ```

---

### 3. Seaborn Cheat Sheet

### a. Basic Plots in Seaborn

- **Line Plot**:
    ```python
    sns.lineplot(x=x, y=y)
    plt.title('Seaborn Line Plot')
    plt.show()
    ```

- **Scatter Plot**:
    ```python
    sns.scatterplot(x=x, y=y)
    plt.title('Seaborn Scatter Plot')
    plt.show()
    ```

- **Bar Plot**:
    ```python
    sns.barplot(x=categories, y=values)
    plt.title('Seaborn Bar Plot')
    plt.show()
    ```

- **Histogram**:
    ```python
    sns.histplot(data, bins=4)
    plt.title('Seaborn Histogram')
    plt.show()
    ```

- **Box Plot**:
    ```python
    sns.boxplot(x=categories, y=values)
    plt.title('Seaborn Box Plot')
    plt.show()
    ```

- **Violin Plot**:
    ```python
    sns.violinplot(x=categories, y=values)
    plt.title('Seaborn Violin Plot')
    plt.show()
    ```

- **Pie Chart**: (Seaborn does not natively support pie charts, but you can use Matplotlib)
    ```python
    labels = ['A', 'B', 'C']
    sizes = [20, 30, 50]
    plt.pie(sizes, labels=labels, autopct='%1.1f%%')
    plt.title('Pie Chart with Matplotlib')
    plt.show()
    ```

---

### b. Advanced Seaborn

- **Pairplot**:
    ```python
    sns.pairplot(df)
    plt.title('Seaborn Pairplot')
    plt.show()
    ```

- **Heatmap**:
    ```python
    sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
    plt.title('Seaborn Heatmap')
    plt.show()
    ```

- **FacetGrid**:
    ```python
    g = sns.FacetGrid(df, col="category")
    g.map(plt.hist, "value")
    plt.show()
    ```

---

### c. Customizing Seaborn Plots

- **Setting Themes**:
    ```python
    sns.set_theme(style="darkgrid")  # Change theme (e.g., 'white', 'dark', 'whitegrid', 'darkgrid')
    sns.lineplot(x=x, y=y)
    plt.show()
    ```

- **Customizing Palettes**:
    ```python
    sns.set_palette("Blues")  # Set color palette
    sns.barplot(x=categories, y=values)
    plt.show()
    ```

- **Modifying Axis Labels**:
    ```python
    sns.lineplot(x=x, y=y)
    plt.xlabel("Custom X Label")
    plt.ylabel("Custom Y Label")
    plt.title("Custom Title")
    plt.show()
    ```

---

### d. Joint Plots and Pair Grids

- **Joint Plot (scatter + hist)**:
    ```python
    sns.jointplot(x='col1', y='col2', data=df, kind='scatter')
    plt.show()
    ```

- **PairGrid**:
    ```python
    g = sns.PairGrid(df)
    g.map(plt.scatter)
    plt.show()
    ```

---

### e. Regression Plots

- **Linear Regression**:
    ```python
    sns.regplot(x='col1', y='col2', data=df)
    plt.title('Linear Regression Plot')
    plt.show()
    ```

- **Logistic Regression**:
    ```python
    sns.lmplot(x='col1', y='col2', data=df, logistic=True)
    plt.title('Logistic Regression Plot')
    plt.show()
    ```

---

### f. Saving Seaborn Plots

- **Saving the Plot**:
    ```python
    sns.lineplot(x=x, y=y)
    plt.savefig('seaborn_plot.png', dpi=300)
    ```

---
