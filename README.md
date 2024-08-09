# 🛒 Analyzing Real Transaction Data 🛒

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-1.2.4+-red.svg)
![Mlxtend](https://img.shields.io/badge/Mlxtend-0.19.0+-green.svg)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.4.2+-orange.svg)
![Seaborn](https://img.shields.io/badge/Seaborn-0.11.1+-purple.svg)

## 📋 Overview

This project analyzes real transaction data to identify frequent itemsets and generate association rules using market basket analysis techniques. The results are visualized to help interpret the strength of these associations, providing actionable insights for optimizing product placement and promotions.

## 🎯 Objectives

- 🛍️ Load and clean transaction data for analysis.
- 🧩 Identify frequent itemsets using the Apriori algorithm.
- 🔗 Generate association rules to discover item relationships.
- 📊 Visualize the association rules using heatmaps for better interpretation.

## 🧩 Code Snippets

### 1. Data Loading and Initial Inspection

```python
import pandas as pd

# Load the dataset from an Excel file
df_retail = pd.read_excel(r"C:\path\to\Online Retail.xlsx", index_col=0, engine='openpyxl')

# Display the number of instances and first few rows
print('The number of instances: ', len(df_retail))
print(df_retail.head())
```
**Explanation:** The code loads the transaction data from an Excel file into a Pandas DataFrame. It also prints out the number of instances and the first few rows to verify successful loading.

## 2. Data Cleanup and Transformation

```python
# Drop rows with missing values in the 'Description' column
df_retail = df_retail.dropna(subset=['Description'])

# Ensure that the 'Description' column is of type string
df_retail = df_retail.astype({"Description": 'str'})

# Group data into transactions using the 'InvoiceNo' column
trans = df_retail.groupby(['InvoiceNo'])['Description'].apply(list).to_list()

# Print the number of transactions
print('Number of transactions: ', len(trans))
```
from mlxtend.preprocessing import TransactionEncoder

# One-hot encode the transaction data
```python
encoder = TransactionEncoder()
encoded_array = encoder.fit(trans).transform(trans)
```
# Convert the encoded array into a DataFrame
```python
df_itemsets = pd.DataFrame(encoded_array, columns=encoder.columns_)
from mlxtend.frequent_patterns import apriori
```
# Identify frequent itemsets using the Apriori algorithm
```python
frequent_itemsets = apriori(df_itemsets, min_support=0.025, use_colnames=True)
```
# Print the frequent itemsets
```python
print(frequent_itemsets)
from mlxtend.frequent_patterns import apriori
```
# Identify frequent itemsets using the Apriori algorithm
```python
frequent_itemsets = apriori(df_itemsets, min_support=0.025, use_colnames=True)
```
# Print the frequent itemsets
```python
print(frequent_itemsets)
import matplotlib.pyplot as plt
import seaborn as sns
```
# Prepare the rules for plotting
```python
rules_plot = pd.DataFrame()
rules_plot['antecedents'] = rules['antecedents'].apply(lambda x: ','.join(list(x)))
rules_plot['consequents'] = rules['consequents'].apply(lambda x: ','.join(list(x)))
rules_plot['lift'] = rules['lift'].apply(lambda x: round(x, 2))
```
# Create a pivot table for the heatmap
```python
pivot = rules_plot.pivot(index='antecedents', columns='consequents', values='lift')
```
# Create a heatmap using Seaborn
```python
plt.figure(figsize=(12, 8))
sns.set(font_scale=1.1)
ax = sns.heatmap(pivot, annot=True, fmt='.2f', cmap='coolwarm', linewidths=.5, linecolor='black')
```
# Rotate the x-axis labels for better readability
```python
plt.xticks(rotation=45, ha='right')
plt.yticks(rotation=0)
```
# Set the title of the heatmap
```python
plt.title("Lift Metric for Frequent Itemsets", fontsize=16)
```
# Display the heatmap
```python
plt.tight_layout()
plt.show()
```
