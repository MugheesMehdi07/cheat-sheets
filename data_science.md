
# Comprehensive Data Science Cheat Sheet

## 1. NumPy Cheat Sheet

### a. Importing NumPy
```python
import numpy as np
```

### b. Arrays
- **Creating Arrays**:
    - 1D Array:
    ```python
    arr = np.array([1, 2, 3])
    ```
    - 2D Array:
    ```python
    two_dim_arr = np.array([[1, 2], [3, 4]])
    ```
    - 3D Array:
    ```python
    three_dim_arr = np.array([[[1], [2]], [[3], [4]]])
    ```

### c. Array Attributes
- **Shape**: Returns the dimensions of the array.
    ```python
    arr.shape  # (3,)
    two_dim_arr.shape  # (2, 2)
    ```
- **Number of Dimensions**:
    ```python
    arr.ndim  # 1
    two_dim_arr.ndim  # 2
    ```
- **Data Type**:
    ```python
    arr.dtype  # dtype('int64')
    ```

### d. Array Operations
- **Basic Operations**:
    ```python
    arr_sum = arr + arr          # Element-wise addition
    arr_diff = arr - arr         # Element-wise subtraction
    arr_product = arr * arr      # Element-wise multiplication
    arr_division = arr / arr     # Element-wise division
    ```
- **Statistical Functions**:
    ```python
    arr_mean = np.mean(arr)      # Mean
    arr_std = np.std(arr)        # Standard Deviation
    arr_var = np.var(arr)        # Variance
    ```
- **Reshaping Arrays**:
    ```python
    arr_reshape = arr.reshape((1, 3))  # Reshape to 1 row, 3 columns
    ```

### e. Slicing and Indexing
- **Accessing Elements**:
    ```python
    element = arr[0]           # First element
    sub_array = arr[0:2]       # Slicing from index 0 to 1
    ```
- **Multi-dimensional indexing**:
    ```python
    two_dim_arr[1, 0]          # Accessing element at 2nd row, 1st column
    ```

### f. Additional Functions
- **Concatenation**:
    ```python
    concatenated = np.concatenate((arr, arr))  # Concatenating along the first axis
    ```
- **Unique Values**:
    ```python
    unique_values = np.unique(arr)
    ```
- **Logical Operations**:
    ```python
    bool_array = arr > 1        # Boolean array where condition is met
    filtered_array = arr[bool_array]  # Array with values greater than 1
    ```

### g. Broadcasting
- **Understanding Broadcasting**:
    ```python
    arr1 = np.array([[1], [2], [3]])
    arr2 = np.array([4, 5, 6])
    result = arr1 + arr2  # Broadcasting arr2 across arr1
    ```

---

## 2. Pandas Transformation Techniques

### a. DataFrame Creation and Basic Operations
- **Creating DataFrame from CSV**:
    ```python
    df = pd.read_csv('data.csv')
    ```
- **Basic Operations**:
    ```python
    df.head()                      # Displays first 5 rows
    df.tail()                      # Displays last 5 rows
    df.info()                      # Displays summary of the DataFrame
    df.describe()                  # Statistical summary of numerical columns
    ```

### b. Data Selection and Filtering
- **Column Selection**:
    ```python
    df['column_name']              # Selects a column
    df[['col1', 'col2']]          # Selects multiple columns
    ```
- **Row Selection**:
    ```python
    df.iloc[0]                    # Selects the first row by index
    df.loc[df['col'] > value]     # Selects rows based on a condition
    ```

### c. Data Transformation Techniques
- **Adding New Columns**:
    ```python
    df['new_col'] = df['A'] + df['B']  # Creating a new column
    ```
- **Dropping Columns**:
    ```python
    df.drop(columns=['B'], inplace=True)  # Drop column B
    ```
- **Renaming Columns**:
    ```python
    df.rename(columns={'old_name': 'new_name'}, inplace=True)  # Renaming a column
    ```
- **Changing Data Types**:
    ```python
    df['col'] = df['col'].astype(float)  # Convert column to float
    ```
- **Handling Missing Data**:
    ```python
    df.fillna(value=0, inplace=True)      # Fill missing values with 0
    df.dropna(inplace=True)                # Drop rows with any missing values
    ```

### d. Data Aggregation and Grouping
- **GroupBy**:
    ```python
    grouped = df.groupby('column_name').mean()  # Grouping by a column and calculating mean
    ```
- **Aggregation Functions**:
    ```python
    df.agg({'A': 'sum', 'B': 'mean'})  # Aggregating multiple functions on columns
    ```

### e. Merging and Joining DataFrames
- **Merging DataFrames**:
    ```python
    merged_df = pd.merge(df1, df2, on='key_column')  # Merging on a key column
    ```
- **Concatenating DataFrames**:
    ```python
    concat_df = pd.concat([df1, df2])  # Concatenating DataFrames
    ```

### f. Applying Functions
- **Using apply()**:
    ```python
    df['new_col'] = df['A'].apply(lambda x: x + 1)  # Applying a function to a column
    ```
- **Using map()**:
    ```python
    df['new_col'] = df['A'].map({'A': 1, 'B': 2})  # Mapping values based on a dictionary
    ```

### g. Pivot Tables
- **Creating Pivot Tables**:
    ```python
    pivot_table = df.pivot_table(values='values_col', index='index_col', columns='columns_col', aggfunc='mean')
    ```

---

## 3. Visualization Techniques

### a. Matplotlib
#### i. Basic Plots
- **Line Plot**:
    ```python
    plt.plot(x, y)
    plt.title('Line Plot')
    plt.xlabel('X-axis')
    plt.ylabel('Y-axis')
    plt.show()
    ```

#### ii. Bar Plot
    ```python
    plt.bar(x, height)
    plt.title('Bar Plot')
    plt.xlabel('Categories')
    plt.ylabel('Values')
    plt.show()
    ```

#### iii. Histogram
    ```python
    plt.hist(data, bins=10)
    plt.title('Histogram')
    plt.xlabel('Value')
    plt.ylabel('Frequency')
    plt.show()
    ```

#### iv. Scatter Plot
    ```python
    plt.scatter(x, y)
    plt.title('Scatter Plot')
    plt.xlabel('X-axis')
    plt.ylabel('Y-axis')
    plt.show()
    ```

#### v. Box Plot
    ```python
    plt.boxplot(data)
    plt.title('Box Plot')
    plt.ylabel('Values')
    plt.show()
    ```

#### vi. Pie Chart
    ```python
    plt.pie(sizes, labels=labels, autopct='%1.1f%%')
    plt.title('Pie Chart')
    plt.show()
    ```

### b. Seaborn
#### i. Line Plot
    ```python
    sns.lineplot(data=df, x='A', y='B')
    plt.title('Line Plot')
    plt.show()
    ```

#### ii. Scatter Plot
    ```python
    sns.scatterplot(data=df, x='A', y='B')
    plt.title('Scatter Plot')
    plt.show()
    ```

#### iii. Box Plot
    ```python
    sns.boxplot(data=df, x='category', y='value')
    plt.title('Box Plot')
    plt.show()
    ```

#### iv. Violin Plot
    ```python
    sns.violinplot(data=df, x='category', y='value')
    plt.title('Violin Plot')
    plt.show()
    ```

#### v. Pair Plot
    ```python
    sns.pairplot(df)
    plt.title('Pair Plot')
    plt.show()
    ```

#### vi. Heatmap
    ```python
    sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
    plt.title('Heatmap of Correlations')
    plt.show()
    ```

---

## 4. Scikit-learn Algorithms and Metrics

### a. Algorithms
#### i. Linear Regression
- **Usage**: Predicting a continuous target variable based on one or more predictors.
- **Benefits**: Simple to implement, interpretable coefficients, performs well with linearly separable data.
    ```python
    from sklearn.linear_model import LinearRegression
    model = LinearRegression().fit(X_train, y_train)
    predictions = model.predict(X_test)
    ```

#### ii. Logistic Regression
- **Usage**: Binary classification problems.
- **Benefits**: Interpretable model

, good for small datasets.
    ```python
    from sklearn.linear_model import LogisticRegression
    model = LogisticRegression().fit(X_train, y_train)
    ```

#### iii. Decision Trees
- **Usage**: Classification and regression tasks.
- **Benefits**: Easy to interpret, handles both numerical and categorical data.
    ```python
    from sklearn.tree import DecisionTreeClassifier
    model = DecisionTreeClassifier().fit(X_train, y_train)
    ```

#### iv. Random Forest
- **Usage**: Ensemble method for classification and regression.
- **Benefits**: Reduces overfitting, robust to noise, provides feature importance.
    ```python
    from sklearn.ensemble import RandomForestClassifier
    model = RandomForestClassifier().fit(X_train, y_train)
    ```

#### v. Support Vector Machines (SVM)
- **Usage**: Classification tasks with high-dimensional data.
- **Benefits**: Effective in high dimensional spaces, robust against overfitting.
    ```python
    from sklearn.svm import SVC
    model = SVC().fit(X_train, y_train)
    ```

#### vi. k-Nearest Neighbors (k-NN)
- **Usage**: Classification and regression tasks.
- **Benefits**: Simple to implement, no training phase.
    ```python
    from sklearn.neighbors import KNeighborsClassifier
    model = KNeighborsClassifier(n_neighbors=3).fit(X_train, y_train)
    ```

#### vii. Gradient Boosting
- **Usage**: Ensemble technique for classification and regression.
- **Benefits**: High performance in competitions, can handle mixed data types.
    ```python
    from sklearn.ensemble import GradientBoostingClassifier
    model = GradientBoostingClassifier().fit(X_train, y_train)
    ```

#### viii. Neural Networks
- **Usage**: Deep learning tasks for complex datasets.
- **Benefits**: Can model complex relationships.
    ```python
    from sklearn.neural_network import MLPClassifier
    model = MLPClassifier().fit(X_train, y_train)
    ```

### b. Evaluation Metrics
#### i. Classification Metrics
- **Accuracy**: 
    - **Usage**: Proportion of correct predictions.
    ```python
    from sklearn.metrics import accuracy_score
    accuracy = accuracy_score(y_test, predictions)
    ```

- **Precision**: 
    - **Usage**: Proportion of true positives out of predicted positives.
    ```python
    from sklearn.metrics import precision_score
    precision = precision_score(y_test, predictions)
    ```

- **Recall**: 
    - **Usage**: Proportion of true positives out of actual positives.
    ```python
    from sklearn.metrics import recall_score
    recall = recall_score(y_test, predictions)
    ```

- **F1 Score**: 
    - **Usage**: Harmonic mean of precision and recall.
    ```python
    from sklearn.metrics import f1_score
    f1 = f1_score(y_test, predictions)
    ```

- **ROC-AUC**: 
    - **Usage**: Measures the trade-off between true positive rate and false positive rate.
    ```python
    from sklearn.metrics import roc_auc_score
    auc = roc_auc_score(y_test, model.predict_proba(X_test)[:, 1])
    ```

#### ii. Regression Metrics
- **Mean Absolute Error (MAE)**: 
    - **Usage**: Average of absolute differences between predicted and actual values.
    ```python
    from sklearn.metrics import mean_absolute_error
    mae = mean_absolute_error(y_test, predictions)
    ```

- **Mean Squared Error (MSE)**: 
    - **Usage**: Average of squared differences between predicted and actual values.
    ```python
    from sklearn.metrics import mean_squared_error
    mse = mean_squared_error(y_test, predictions)
    ```

- **R² Score**: 
    - **Usage**: Proportion of variance explained by the model.
    ```python
    from sklearn.metrics import r2_score
    r2 = r2_score(y_test, predictions)
    ```
