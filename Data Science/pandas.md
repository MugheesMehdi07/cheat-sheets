Here’s a detailed **Pandas Cheat Sheet**, structured similarly to the one for NumPy. It covers key features and operations commonly used in data analysis.

```
## 1. Pandas Cheat Sheet

### a. Importing Pandas
```python
import pandas as pd
```

### b. Data Structures
- **Series**: One-dimensional labeled array.
    ```python
    s = pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])
    ```
- **DataFrame**: Two-dimensional labeled data structure.
    ```python
    data = {'col1': [1, 2], 'col2': [3, 4]}
    df = pd.DataFrame(data)
    ```

### c. Reading and Writing Data
- **Reading from CSV**:
    ```python
    df = pd.read_csv('file.csv')
    ```
- **Writing to CSV**:
    ```python
    df.to_csv('file.csv', index=False)
    ```

- **Reading from Excel**:
    ```python
    df = pd.read_excel('file.xlsx', sheet_name='Sheet1')
    ```
- **Writing to Excel**:
    ```python
    df.to_excel('output.xlsx', sheet_name='Sheet1', index=False)
    ```

- **Reading from SQL**:
    ```python
    df = pd.read_sql('SELECT * FROM table', connection)
    ```

### d. DataFrame Attributes
- **Shape**:
    ```python
    df.shape  # Returns (rows, columns)
    ```
- **Columns**:
    ```python
    df.columns  # Returns the column labels
    ```
- **Index**:
    ```python
    df.index  # Returns the row labels
    ```
- **Data Types**:
    ```python
    df.dtypes  # Returns data types of each column
    ```

### e. Data Selection and Filtering
- **Selecting Columns**:
    ```python
    df['col1']  # Returns a Series for a single column
    df[['col1', 'col2']]  # Returns a DataFrame for multiple columns
    ```

- **Selecting Rows by Index**:
    ```python
    df.iloc[0]  # Select the first row
    df.iloc[0:2]  # Select the first two rows
    df.loc['row_label']  # Select rows by index label
    ```

- **Conditional Filtering**:
    ```python
    df[df['col1'] > 1]  # Rows where 'col1' is greater than 1
    ```

### f. Data Cleaning
- **Handling Missing Data**:
    ```python
    df.isnull()  # Detect missing values
    df.dropna()  # Drop rows with missing values
    df.fillna(0)  # Fill missing values with a specified value
    ```

- **Renaming Columns**:
    ```python
    df.rename(columns={'old_name': 'new_name'}, inplace=True)
    ```

- **Replacing Values**:
    ```python
    df.replace({'old_value': 'new_value'}, inplace=True)
    ```

### g. DataFrame Operations
- **Basic Operations**:
    ```python
    df['col1'] + df['col2']  # Element-wise addition of two columns
    df['col1'] * 2           # Multiply a column by a scalar
    ```

- **Sorting**:
    ```python
    df_sorted = df.sort_values('col1')  # Sort DataFrame by 'col1'
    df_sorted_by_index = df.sort_index()  # Sort by index
    ```

- **Statistical Functions**:
    ```python
    df_mean = df.mean()       # Mean of each column
    df_median = df.median()   # Median of each column
    df_std = df.std()         # Standard deviation
    df_sum = df.sum()         # Sum of each column
    ```

- **Unique Values**:
    ```python
    df['col1'].unique()  # Unique values in a column
    df['col1'].nunique()  # Number of unique values
    ```

- **Value Counts**:
    ```python
    df['col1'].value_counts()  # Count occurrences of each value
    ```

### h. Grouping and Aggregation
- **Grouping Data**:
    ```python
    grouped = df.groupby('col1')
    ```

- **Aggregation Functions**:
    ```python
    grouped['col2'].mean()  # Mean for each group
    grouped['col2'].agg(['mean', 'sum'])  # Multiple aggregate functions
    grouped.agg({'col2': 'mean', 'col3': 'sum'})  # Different functions for different columns
    ```

- **Pivot Table**:
    ```python
    pivot_table = df.pivot_table(values='col1', index='col2', columns='col3', aggfunc='mean')
    ```

### i. Merging and Joining
- **Concatenation**:
    ```python
    pd.concat([df1, df2], axis=0)  # Concatenate DataFrames vertically (row-wise)
    pd.concat([df1, df2], axis=1)  # Concatenate DataFrames horizontally (column-wise)
    ```

- **Merging**:
    ```python
    merged = pd.merge(df1, df2, on='key')  # Merge DataFrames on a common column
    ```

- **Joining**:
    ```python
    joined = df1.join(df2.set_index('key'), on='key')  # Join on index or key
    ```

### j. Reshaping Data
- **Stacking and Unstacking**:
    ```python
    stacked = df.stack()    # Pivot columns into rows
    unstacked = df.unstack()  # Pivot rows into columns
    ```

- **Melt**:
    ```python
    melted = pd.melt(df, id_vars=['col1'], value_vars=['col2', 'col3'])  # Unpivot DataFrame from wide to long format
    ```

### k. Working with Dates
- **Converting to Datetime**:
    ```python
    df['date'] = pd.to_datetime(df['date'])
    ```

- **Date Components**:
    ```python
    df['year'] = df['date'].dt.year
    df['month'] = df['date'].dt.month
    df['day'] = df['date'].dt.day
    ```

- **Date Range**:
    ```python
    date_range = pd.date_range(start='2024-01-01', end='2024-12-31', freq='D')
    ```

### l. Visualization
- **Basic Plotting**:
    ```python
    df.plot(kind='line')  # Line plot
    df.plot(kind='bar')   # Bar plot
    df.plot(kind='hist')  # Histogram
    df.plot(kind='box')   # Box plot
    df.plot(kind='scatter', x='col1', y='col2')  # Scatter plot
    ```

- **Correlation Plot**:
    ```python
    df.corr().plot(kind='heatmap')  # Heatmap of correlations
    ```

### m. Advanced Operations
- **Applying Functions**:
    ```python
    df['col1'].apply(lambda x: x * 2)  # Apply a function to a column
    ```

- **Rolling Statistics**:
    ```python
    df['rolling_mean'] = df['col1'].rolling(window=3).mean()  # Rolling mean with window size 3
    ```

- **Cumulative Functions**:
    ```python
    df['cum_sum'] = df['col1'].cumsum()  # Cumulative sum
    df['cum_prod'] = df['col1'].cumprod()  # Cumulative product
    ```

--- 
This cheat sheet covers the core functionalities of **Pandas**, from reading data to advanced operations like reshaping, merging, and visualization. Let me know if you’d like any modifications or additions!