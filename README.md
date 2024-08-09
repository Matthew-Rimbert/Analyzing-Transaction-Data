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
