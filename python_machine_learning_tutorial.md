# Python Machine Learning Tutorial for Absolute Beginners

## Table of Contents

1. **Introduction to Numpy, Pandas, and Matplotlib**

   - Numpy Basics
   - Pandas Basics
   - Matplotlib Basics

2. **Introduction to Machine Learning**

   - What is Machine Learning?
   - Types of Machine Learning Algorithms
   - Supervised Learning, Unsupervised Learning, and More

3. **Linear Regression**

   - What is Linear Regression?
   - Implementation using Scikit-Learn
   - Plotting the Regression Line

4. **Logistic Regression**

   - What is Logistic Regression?
   - Binary and Multiclass Classification
   - Implementing Logistic Regression

5. **Decision Trees**

   - Introduction to Decision Trees
   - Decision Tree Construction
   - Visualizing Decision Trees

6. **Random Forest**

   - What is Random Forest?
   - Ensemble Learning
   - Building and Visualizing Random Forest

7. **K-Nearest Neighbors (KNN)**
   - Introduction to KNN
   - Working Mechanism
   - Implementing KNN with Scikit-Learn

---

## 1. Introduction to Numpy, Pandas, and Matplotlib

### Numpy Basics

Numpy is a library for numerical computations in Python.

```python
import numpy as np

# Create a Numpy array
arr = np.array([1, 2, 3, 4, 5])

# Calculate mean
mean = np.mean(arr)

# Calculate standard deviation
std = np.std(arr)
```

### Pandas Basics

Pandas is used for data manipulation and analysis.

```python
import pandas as pd

# Create a DataFrame
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 22]}
df = pd.DataFrame(data)

# Filter data
filtered_data = df[df['Age'] > 25]

# Group data
grouped_data = df.groupby('Age').count()
```

### Matplotlib Basics

Matplotlib is a data visualization library.

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [10, 14, 8, 12, 6]

# Create a line plot
plt.plot(x, y)
plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.title('Line Plot')
plt.show()
```

---

## 2. Introduction to Machine Learning

### What is Machine Learning?

Machine Learning is a subset of artificial intelligence that enables systems to learn from data and make predictions or decisions.

### Types of Machine Learning Algorithms

- **Supervised Learning**: Learn from labeled data (input, output pairs).
- **Unsupervised Learning**: Find patterns in unlabeled data.
- **Reinforcement Learning**: Learn from actions and rewards.
- **Semi-Supervised Learning**: Mix of labeled and unlabeled data.
- **Deep Learning**: Neural networks with many layers.

### Supervised Learning, Unsupervised Learning, and More

Supervised Learning example:

```python
# Given dataset
X = np.array([[1, 2], [2, 3], [3, 4]])
y = np.array([5, 8, 11])

# Linear regression model
from sklearn.linear_model import LinearRegression
model = LinearRegression()
model.fit(X, y)

# Make predictions
predictions = model.predict([[4, 5]])
```

---

## 3. Linear Regression

### What is Linear Regression?

Linear Regression is a supervised learning algorithm used for predicting continuous output based on input features.

### Implementation using Scikit-Learn

```python
# Given dataset
X = np.array([1, 2, 3, 4, 5]).reshape(-1, 1)
y = np.array([2, 4, 5, 4, 5])

# Linear regression model
from sklearn.linear_model import LinearRegression
model = LinearRegression()
model.fit(X, y)

# Make predictions
predictions = model.predict([[6]])
```

### Plotting the Regression Line

```python
plt.scatter(X, y)
plt.plot(X, model.predict(X), color='red')
plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.title('Linear Regression')
plt.show()
```

In this example, we have data points and a linear regression line fitted to the data.

---

## 4. Logistic Regression

### What is Logistic Regression?

Logistic Regression is used for binary or multiclass classification problems.

### Binary and Multiclass Classification

```python
# Given dataset
X = np.array([[1, 2], [2, 3], [3, 4]])
y = np.array([0, 1, 1])  # Binary labels

# Logistic regression model
from sklearn.linear_model import LogisticRegression
model = LogisticRegression()
model.fit(X, y)

# Make predictions
predictions = model.predict([[4, 5]])
```

### Implementing Logistic Regression

```python
from sklearn.datasets import load_iris

# Load Iris dataset
iris = load_iris()
X = iris.data
y = iris.target

# Logistic regression model
model = LogisticRegression(multi_class='ovr')
model.fit(X, y)

# Make predictions
predictions = model.predict(X)
```

---

## 5. Decision Trees

### Introduction to Decision Trees

Decision Trees are used for both classification and regression tasks.

### Decision Tree Construction

```python
from sklearn.tree import DecisionTreeClassifier

# Given dataset
X = np.array([[1, 2], [2, 3], [3, 4]])
y = np.array([0, 1, 1])  # Binary labels

# Decision Tree model
model = DecisionTreeClassifier()
model.fit(X, y)

# Make predictions
predictions = model.predict([[4, 5]])
```

### Visualizing Decision Trees

```python
from sklearn.tree import plot_tree

plt.figure(figsize=(10, 6))
plot_tree(model, filled=True)
plt.show()
```

The plot displays the decision tree's structure and decisions made at each node.

---

## 6. Random Forest

### What is Random Forest?

Random Forest is an ensemble learning algorithm combining multiple decision trees.

### Ensemble Learning

```python
from sklearn.ensemble import RandomForestClassifier

# Given dataset
X = np.array([[1, 2], [2, 3], [3, 4]])
y = np.array([0, 1, 1])  # Binary labels

# Random Forest model
model = RandomForestClassifier(n_estimators=100)
model.fit(X, y)

# Make predictions
predictions = model.predict([[4, 5]])
```

### Building and Visualizing Random Forest

```python
from sklearn.datasets import load_iris

# Load Iris dataset
iris = load_iris()
X = iris.data
y = iris.target

# Random Forest model
model = RandomForestClassifier(n_estimators=100)
model.fit(X, y)

# Visualizing a single decision tree within the forest
plt.figure(figsize=(10, 6))
plot_tree(model.estimators_[0], filled=True)
plt.show()
```

---

## 7. K-Nearest Neighbors (KNN)

### Introduction to KNN

K-Nearest Neighbors is a classification algorithm that classifies

a data point based on the majority class of its k nearest neighbors.

### Working Mechanism

```python
from sklearn.neighbors import KNeighborsClassifier

# Given dataset
X = np.array([[1, 2], [2, 3], [3, 4]])
y = np.array([0, 1, 1])  # Binary labels

# KNN model
model = KNeighborsClassifier(n_neighbors=2)
model.fit(X, y)

# Make predictions
predictions = model.predict([[4, 5]])
```

### Implementing KNN with Scikit-Learn

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Load Iris dataset
iris = load_iris()
X = iris.data
y = iris.target

# Split dataset into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# KNN model
model = KNeighborsClassifier(n_neighbors=3)
model.fit(X_train, y_train)

# Make predictions
predictions = model.predict(X_test)

# Evaluate accuracy
accuracy = accuracy_score(y_test, predictions)
```

---

Congratulations! You've completed the Python Machine Learning Tutorial for Absolute Beginners. This tutorial covered essential concepts, algorithms, and their implementation using Scikit-Learn. You've learned about Numpy, Pandas, Matplotlib, Linear Regression, Logistic Regression, Decision Trees, Random Forest, and K-Nearest Neighbors. Continue practicing and experimenting to build a strong foundation in machine learning.
