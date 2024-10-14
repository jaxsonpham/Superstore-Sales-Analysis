# Superstore Sales Analysis

## Overview

This project is a data analysis of a **Superstore Sales** dataset using **Python** and libraries like `pandas`, `plotly`, and `plotly.express`. The dataset includes sales, customer, and product details, which are analyzed to understand trends, missing data, outliers, and relationships between key variables.

### Requirements

- Python 3.x
- pandas
- plotly

### Installation

To set up the environment and run the code:

1. Install the required libraries:
   ```bash
   pip install pandas plotly
   ```
   
2. Download or import the dataset file `Superstore_Sales.csv` into the working directory.

### Code Breakdown

1. **Importing Libraries**:
   - `pandas`: For data manipulation and analysis.
   - `plotly`: For interactive visualizations.

   ```python
   import pandas as pd
   import plotly.express as px
   ```

2. **Loading the Dataset**:
   The dataset is loaded from a CSV file using `pandas.read_csv()`.

   ```python
   df = pd.read_csv('Superstore_Sales.csv')
   ```

3. **Understanding the Dataset Structure**:
   Using `df.info()`, we get an overview of the dataset, including the number of entries, columns, and data types.

   ```python
   df.info()
   ```

4. **Handling Missing Values**:
   - The missing values in `Customer ID` are imputed with the most frequent value (mode).
   - Missing values in `Sales` and `Quantity` are filled with the median.

   ```python
   df['Customer ID'].fillna(df['Customer ID'].mode()[0], inplace=True)
   df['Sales'].fillna(df['Sales'].median(), inplace=True)
   df['Quantity'].fillna(df['Quantity'].median(), inplace=True)
   ```

5. **Data Type Conversion**:
   The `Ship Date` column is converted to a `datetime` object to ensure proper date handling.

   ```python
   df['Ship Date'] = pd.to_datetime(df['Ship Date'])
   ```

6. **Visualizing Data**:
   - **Sales Distribution**: A histogram shows the distribution of sales.
   - **Quantity Distribution**: Another histogram for quantity distribution.

   ```python
   fig = px.histogram(df, x='Sales', nbins=100, title='Distribution of Sales')
   fig.show()
   
   fig = px.histogram(df, x='Quantity', nbins=100, title='Distribution of Quantity')
   fig.show()
   ```

7. **Outlier Detection**:
   Boxplots are created for `Sales`, `Quantity`, `Discount`, and `Profit` to visualize and handle outliers. Sales outliers above the 99th percentile are capped.

   ```python
   upper_bound = df['Sales'].quantile(0.99)
   df.loc[df['Sales'] > upper_bound, 'Sales'] = upper_bound
   
   fig = px.box(df, y='Sales', title='Outliers for Sales')
   fig.show()
   ```

8. **Removing Duplicates**:
   The code checks for duplicate rows and removes them from the dataset.

   ```python
   df.drop_duplicates(inplace=True)
   ```

9. **Summary Statistics**:
   The `describe()` function is used to get summary statistics for both numerical and categorical columns.

   ```python
   df.describe()
   ```

10. **Filtering Data**:
    A filtering function is applied to limit the dataset to sales greater than $1000.

    ```python
    filtered_df = df[df['Sales'] > 1000]
    ```

### Output

The code outputs multiple visualizations and summary statistics to understand the sales, quantity, and profitability trends in the dataset. The outliers and missing data are addressed to ensure clean data analysis.
