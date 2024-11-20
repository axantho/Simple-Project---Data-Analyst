



# Libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

# Load Dataset
data = pd.read_csv('/kaggle/input/titanic/train.csv')
data.head()

# Dataset Overview
print("Dataset Information:")
print(data.info())
print("\nMissing Values:")
print(data.isnull().sum())

# Descriptive Statistics
data.describe()

# Univariate Analysis: Age Distribution
plt.figure(figsize=(8, 5))
sns.histplot(data['Age'].dropna(), kde=True, bins=30, color='skyblue')
plt.title('Age Distribution')
plt.xlabel('Age')
plt.show()

# Multivariate Analysis: Survival Rate by Class
plt.figure(figsize=(8, 5))
sns.barplot(x='Pclass', y='Survived', palette='viridis', data=data)
plt.title('Survival Rate by Passenger Class')
plt.ylabel('Survival Rate')
plt.show()

# Handling Missing Data
data['Age'].fillna(data['Age'].median(), inplace=True)
data['Embarked'].fillna(data['Embarked'].mode()[0], inplace=True)

# Creating New Features
data['FamilySize'] = data['SibSp'] + data['Parch'] + 1
data['IsAlone'] = (data['FamilySize'] == 1).astype(int)

# Encoding Categorical Data
data['Sex'] = data['Sex'].map({'male': 0, 'female': 1})
data = pd.get_dummies(data, columns=['Embarked'], drop_first=True)

# Insight 1: Gender Impact on Survival
plt.figure(figsize=(8, 5))
sns.barplot(x='Sex', y='Survived', palette='pastel', data=data)
plt.title('Survival Rate by Gender')
plt.xlabel('Gender (0 = Male, 1 = Female)')
plt.ylabel('Survival Rate')
plt.show()

# Insight 2: Ticket Class and Gender
plt.figure(figsize=(10, 6))
sns.barplot(x='Pclass', y='Survived', hue='Sex', data=data, palette='coolwarm')
plt.title('Survival Rate by Ticket Class and Gender')
plt.xlabel('Ticket Class')
plt.ylabel('Survival Rate')
plt.legend(title='Gender (0 = Male, 1 = Female)')
plt.show()

# Feature Selection
features = ['Pclass', 'Sex', 'Age', 'Fare', 'FamilySize', 'IsAlone', 
            'Embarked_Q', 'Embarked_S']
target = 'Survived'

X = data[features]
y = data[target]

# Split Data into Training and Testing Sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train Random Forest Classifier
model = RandomForestClassifier(random_state=42, n_estimators=100, max_depth=5)
model.fit(X_train, y_train)

# Predict on Test Data
y_pred = model.predict(X_test)

# Model Evaluation
accuracy = accuracy_score(y_test, y_pred)
print(f"Model Accuracy: {accuracy:.2f}")

# Confusion Matrix and Classification Report
print("\nClassification Report:")
print(classification_report(y_test, y_pred))

print("\nConfusion Matrix:")
sns.heatmap(confusion_matrix(y_test, y_pred), annot=True, fmt='d', cmap='Blues')
plt.title('Confusion Matrix')
plt.show()

