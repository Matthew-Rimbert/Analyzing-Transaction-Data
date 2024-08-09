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
- 
## 📂 Dataset

The dataset used for this analysis is included in the repository and can be accessed here:
[Online Retail.xlsx](https://github.com/user-attachments/files/16566967/Online.Retail.xlsx)

- **File Name:** `Online.Retail.xlsx`
- **Format:** Excel
- **Contents:** The dataset includes details of 541,909 transactions, such as stock codes, descriptions, quantities, unit prices, customer IDs, and the countries where the purchases were made.

## 📊 Dataset Summary

- **Total Instances:** 541,909 transactions
- **Total Unique Transactions:** 24,446
- **Columns:**
  - `StockCode`: Unique code for each item.
  - `Description`: Description of the item.
  - `Quantity`: Number of units of the item purchased.
  - `InvoiceNo`: Invoice number (used to group transactions).
  - `UnitPrice`: Price per unit of the item.
  - `CustomerID`: Identifier for the customer making the purchase.
  - `Country`: Country where the purchase was made.

### Sample Data
![moredata](https://github.com/user-attachments/assets/d5126c3e-f0d5-41a2-a2d0-b85513b5e1bb)

## 🧩 Frequent Itemsets

Frequent itemsets are groups of items that are often purchased together. Identifying these itemsets helps businesses understand which products are popular in combination and can inform strategies such as bundling or cross-promotions.

- **Total Frequent Itemsets Identified:** 136
- **Example Itemsets and Support:**
  - `(6 RIBBONS RUSTIC CHARM)` with a support of 0.039311 (3.93% of transactions)
  - `(ALARM CLOCK BAKELIKE GREEN)` with a support of 0.040947 (4.09% of transactions)
  - `(JUMBO BAG RED RETROSPOT, JUMBO SHOPPER VINTAGE RED PAISLEY)` with a support of 0.027939 (2.79% of transactions)

## 🔗 Association Rules

Association rules are generated to uncover relationships between different products in transactions. These rules indicate how the purchase of one item (antecedent) influences the purchase of another item (consequent).

- **Total Association Rules Generated:** 13
- **Metrics:**
  - **Confidence:** The likelihood that the consequent is purchased when the antecedent is purchased.
  - **Lift:** A measure of how much more likely the consequent is to be purchased compared to if it was unrelated to the antecedent.

### Example Association Rules

1. **Rule:** `(ALARM CLOCK BAKELIKE RED) → (ALARM CLOCK BAKELIKE GREEN)`
   - **Confidence:** 59.76%
   - **Lift:** 14.59
   - **Interpretation:** Customers who buy the red version of the alarm clock are highly likely to also buy the green version.

2. **Rule:** `(PINK REGENCY TEACUP AND SAUCER) → (GREEN REGENCY TEACUP AND SAUCER)`
   - **Confidence:** 80.40%
   - **Lift:** 18.59
   - **Interpretation:** The purchase of one color variant of the Regency teacup and saucer significantly increases the likelihood of purchasing another color variant.

### Visualizing Association Rules

![heatmap](https://github.com/user-attachments/assets/415233d2-f4ac-4613-b2ad-b0fcad4b5ff5)
Explanation: This heatmap visualizes the lift metric for the identified frequent itemsets, providing an intuitive way to understand the strength of associations between different items.

### 📈 Conclusion
This analysis of e-commerce transaction data reveals significant associations between various products, particularly color variants and related items. Businesses can utilize these insights to:

- Optimize product placement and bundling.
- Design targeted marketing campaigns.
- Improve inventory management by anticipating demand for commonly paired items.

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

### One-hot encode the transaction data
```python
encoder = TransactionEncoder()
encoded_array = encoder.fit(trans).transform(trans)
```
### Convert the encoded array into a DataFrame
```python
df_itemsets = pd.DataFrame(encoded_array, columns=encoder.columns_)
from mlxtend.frequent_patterns import apriori
```
### Identify frequent itemsets using the Apriori algorithm
```python
frequent_itemsets = apriori(df_itemsets, min_support=0.025, use_colnames=True)
```
### Print the frequent itemsets
```python
print(frequent_itemsets)
from mlxtend.frequent_patterns import apriori
```
### Identify frequent itemsets using the Apriori algorithm
```python
frequent_itemsets = apriori(df_itemsets, min_support=0.025, use_colnames=True)
```
### Print the frequent itemsets
```python
print(frequent_itemsets)
import matplotlib.pyplot as plt
import seaborn as sns
```
### Prepare the rules for plotting
```python
rules_plot = pd.DataFrame()
rules_plot['antecedents'] = rules['antecedents'].apply(lambda x: ','.join(list(x)))
rules_plot['consequents'] = rules['consequents'].apply(lambda x: ','.join(list(x)))
rules_plot['lift'] = rules['lift'].apply(lambda x: round(x, 2))
```
### Create a pivot table for the heatmap
```python
pivot = rules_plot.pivot(index='antecedents', columns='consequents', values='lift')
```
### Create a heatmap using Seaborn
```python
plt.figure(figsize=(12, 8))
sns.set(font_scale=1.1)
ax = sns.heatmap(pivot, annot=True, fmt='.2f', cmap='coolwarm', linewidths=.5, linecolor='black')
```
### Display the heatmap
```python
plt.tight_layout()
plt.show()
```
## 📈 Summary
The project effectively demonstrates how to analyze transaction data to uncover patterns in customer purchasing behavior. By identifying frequent itemsets and generating association rules, businesses can gain insights into product relationships and use these insights to optimize inventory, promotions, and product placements.
