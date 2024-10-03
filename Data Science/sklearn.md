Here's a detailed cheat sheet for **Scikit-learn** and **SciPy**. This includes a wide range of algorithms for prediction, evaluation metrics, and feature engineering, along with notes on when and where to use each approach.

```
## 1. Machine Learning with Scikit-learn & SciPy Cheat Sheet

### a. Importing Libraries
```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, MinMaxScaler, LabelEncoder
from sklearn.metrics import accuracy_score, mean_squared_error, classification_report
import scipy.stats as stats
```

---

### 2. Feature Engineering

#### a. Encoding Categorical Variables
- **Label Encoding**: Convert categorical labels into integers. Best for ordinal data.
    ```python
    le = LabelEncoder()
    df['encoded_column'] = le.fit_transform(df['category_column'])
    ```

- **One-Hot Encoding**: Convert categorical data into dummy/indicator variables. Best for nominal data.
    ```python
    df_encoded = pd.get_dummies(df, columns=['category_column'])
    ```

#### b. Feature Scaling
- **Standardization**: Scales data to have a mean of 0 and standard deviation of 1. Use for most algorithms like logistic regression, SVM, etc.
    ```python
    scaler = StandardScaler()
    df_scaled = scaler.fit_transform(df)
    ```

- **Normalization**: Scales data to a range of 0 to 1. Use when you need to bound the feature values (e.g., neural networks).
    ```python
    scaler = MinMaxScaler()
    df_normalized = scaler.fit_transform(df)
    ```

#### c. Feature Selection
- **Variance Threshold**: Removes features with low variance.
    ```python
    from sklearn.feature_selection import VarianceThreshold
    selector = VarianceThreshold(threshold=0.1)
    df_selected = selector.fit_transform(df)
    ```

- **SelectKBest**: Select the top K features based on statistical tests.
    ```python
    from sklearn.feature_selection import SelectKBest, f_classif
    selector = SelectKBest(score_func=f_classif, k=10)
    df_selected = selector.fit_transform(X, y)
    ```

#### d. Polynomial Features
- **Use**: For models that benefit from non-linear relationships.
    ```python
    from sklearn.preprocessing import PolynomialFeatures
    poly = PolynomialFeatures(degree=2)
    df_poly = poly.fit_transform(df)
    ```

---

### 3. Model Selection

#### a. Supervised Learning

##### Classification Algorithms:
- **Logistic Regression**: Used when the target variable is binary (0 or 1).
    ```python
    from sklearn.linear_model import LogisticRegression
    model = LogisticRegression()
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    ```

- **Decision Tree Classifier**: Works well for both categorical and continuous data. It’s easy to interpret but can easily overfit.
    ```python
    from sklearn.tree import DecisionTreeClassifier
    model = DecisionTreeClassifier()
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    ```

- **Random Forest Classifier**: An ensemble of decision trees. Use when you want to improve accuracy and reduce overfitting.
    ```python
    from sklearn.ensemble import RandomForestClassifier
    model = RandomForestClassifier()
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    ```

- **Support Vector Machine (SVM)**: Effective for high-dimensional spaces and non-linear data.
    ```python
    from sklearn.svm import SVC
    model = SVC(kernel='rbf')
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    ```

- **K-Nearest Neighbors (KNN)**: Simple algorithm. Use when you want a non-parametric model and for small datasets.
    ```python
    from sklearn.neighbors import KNeighborsClassifier
    model = KNeighborsClassifier(n_neighbors=5)
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    ```

- **Naive Bayes**: Best used when the features are independent of each other.
    ```python
    from sklearn.naive_bayes import GaussianNB
    model = GaussianNB()
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    ```

##### Regression Algorithms:
- **Linear Regression**: For continuous target variables. Simple, interpretable model.
    ```python
    from sklearn.linear_model import LinearRegression
    model = LinearRegression()
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    ```

- **Ridge and Lasso Regression**: Linear regression with L2 (Ridge) and L1 (Lasso) regularization to avoid overfitting.
    ```python
    from sklearn.linear_model import Ridge, Lasso
    ridge = Ridge(alpha=1.0)
    lasso = Lasso(alpha=0.1)
    ridge.fit(X_train, y_train)
    lasso.fit(X_train, y_train)
    ```

- **Decision Tree Regressor**: Non-linear, interpretable model. Can overfit on small datasets.
    ```python
    from sklearn.tree import DecisionTreeRegressor
    model = DecisionTreeRegressor()
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    ```

- **Random Forest Regressor**: Reduces overfitting compared to decision trees.
    ```python
    from sklearn.ensemble import RandomForestRegressor
    model = RandomForestRegressor()
    model.fit(X_train, y_train)
    predictions = model.predict(X_test)
    ```

---

### 4. Model Evaluation

#### a. Classification Metrics
- **Accuracy**: Overall correctness of the model.
    ```python
    accuracy = accuracy_score(y_test, predictions)
    ```

- **Confusion Matrix**: Gives detailed information on true/false positives and negatives.
    ```python
    from sklearn.metrics import confusion_matrix
    cm = confusion_matrix(y_test, predictions)
    ```

- **Precision, Recall, F1-Score**: Useful when classes are imbalanced.
    ```python
    from sklearn.metrics import classification_report
    print(classification_report(y_test, predictions))
    ```

#### b. Regression Metrics
- **Mean Squared Error (MSE)**: Measures average squared difference between actual and predicted values.
    ```python
    mse = mean_squared_error(y_test, predictions)
    ```

- **R-Squared**: Proportion of variance explained by the model.
    ```python
    from sklearn.metrics import r2_score
    r_squared = r2_score(y_test, predictions)
    ```

---

### 5. Cross-Validation & Hyperparameter Tuning

#### a. Cross-Validation
- **K-Fold Cross-Validation**: Use when you want to validate the model on different data splits.
    ```python
    from sklearn.model_selection import cross_val_score
    scores = cross_val_score(model, X, y, cv=5)  # 5-fold cross-validation
    ```

#### b. Grid Search for Hyperparameter Tuning
- **Use**: Automatically tune hyperparameters to find the best model.
    ```python
    from sklearn.model_selection import GridSearchCV
    param_grid = {'C': [0.1, 1, 10], 'kernel': ['linear', 'rbf']}
    grid_search = GridSearchCV(SVC(), param_grid, cv=5)
    grid_search.fit(X_train, y_train)
    print(grid_search.best_params_)
    ```

---

### 6. Unsupervised Learning

#### a. Clustering Algorithms
- **K-Means Clustering**: Use for partitioning the dataset into K distinct clusters.
    ```python
    from sklearn.cluster import KMeans
    kmeans = KMeans(n_clusters=3)
    kmeans.fit(X)
    ```

- **Hierarchical Clustering**: Builds a hierarchy of clusters.
    ```python
    from scipy.cluster.hierarchy import dendrogram, linkage
    Z = linkage(X, 'ward')
    dendrogram(Z)
    plt.show()
    ```

- **DBSCAN**: Clustering based on density (good for non-spherical data).
    ```python
    from sklearn.cluster import DBSCAN
    dbscan = DBSCAN(eps=0.5, min_samples=5)
    dbscan.fit(X)
    ```

#### b. Dimensionality Reduction
- **Principal Component Analysis (PCA)**: Use to reduce dimensionality while preserving variance.
    ```python
    from sklearn.decomposition import PCA
    pca = PCA(n_components=2)
    X_reduced = pca.fit_transform(X)
    ```

- **t-SNE**: Best for visualizing high-dimensional data.
    ```python
    from sklearn.manifold import TSNE
    tsne = TSNE(n_components=2)
    X_embedded = tsne.fit_transform(X)
    ```

---

### 7. Statistical Functions with SciPy

#### a. Statistical Tests
- **t-test**: Test whether two sample means are different.
    ```python
    t_stat, p_value = stats.ttest_ind(group1, group2)
    ```

- **Chi-Square Test**: Test for independence between categorical variables.
    ```python
    chi2_stat, p_value = stats.chi2_contingency(pd.crosstab(df['A'], df['B']))
    ```

- **ANOVA (Analysis of Variance)**: Test whether the means of multiple groups are equal.
    ```python
    f_stat, p_value = stats.f_oneway(group1, group2, group3)
    ```

#### b. Probability Distributions
- **Normal Distribution**:
    ```python
    normal_dist = stats.norm(loc=0, scale=1)
    data = normal_dist.rvs(1000)  # Generate random numbers
    ```

- **Binomial Distribution**:
    ```python
    binom_dist = stats.binom(n=10, p=0.5)
    data = binom_dist.rvs(1000)
    ```

---

### 8. Model Deployment & Saving

- **Saving the Model**:
    ```python
    import pickle
    with open('model.pkl', 'wb') as f:
        pickle.dump(model, f)
    ```

- **Loading the Model**:
    ```python
    with open('model.pkl', 'rb') as f:
        loaded_model = pickle.load(f)
    ```

---

This cheat sheet covers **Scikit-learn** and **SciPy** for both supervised and unsupervised learning, along with feature engineering, statistical testing, and model evaluation. Let me know if you need further enhancements!
```