# Analysis-and-Visualization-of-COVID-19-Dataset
```
Name : Vikhram S
Reg No : 212222060295
```
## Aim

To analyse a large real-world COVID-19 dataset using Python by performing data exploration and visualizing key trends through various plots such as line graph, bar chart, pie chart, scatter plot, and histogram for meaningful insights.

## Algorithm

### 1. Import libraries: Pandas, Matplotlib, and NumPy.

### 2. Load dataset covid_cases.csv using Pandas.

### 3. Explore dataset:

Display first few rows

Show dataset shape

Display column names

Check and handle missing values

### 4. Basic data analysis:

Total number of records

Statistical summary using describe()

### 5. Data preprocessing:

Convert date column into datetime format (if present)

Group data by date for global trend

Group by country for top affected countries

### 6. Visualizations using Matplotlib:

Line Graph: Global trend of confirmed cases over time

Bar Chart: Top 10 countries by confirmed cases

Pie Chart: Case distribution of top 5 countries

Scatter Plot: Confirmed vs. Deaths

Histogram: Distribution of active cases

### 7. Label charts: Add titles, axis labels, legends, colors

### 8. Display all graphs

### 9. End

```Python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
```

### Step 1: Load Dataset
```Python
df = pd.read_csv("covid_cases.csv")
```

### Step 2: Explore Dataset
```Python
print("\n----- First 5 Rows -----")
print(df.head())

print("\n----- Dataset Shape -----")
print(df.shape)

print("\n----- Column Names -----")
print(df.columns)

print("\n----- Missing Values -----")
print(df.isnull().sum())

# Handle missing values (optional)
df = df.fillna(0)
```
### Step 3: Basic Exploration
```Python

print("\n----- Total Records -----")
print(len(df))

print("\n----- Statistical Summary -----")
print(df.describe())
```

### Step 4: Data Preprocessing
```Python

# Convert date column if present
if 'Date' in df.columns:
    df['Date'] = pd.to_datetime(df['Date'])

# Global trend (confirmed cases per date)
if 'Date' in df.columns and 'Confirmed' in df.columns:
    global_trend = df.groupby('Date')['Confirmed'].sum()

# Top 10 countries by total confirmed cases
if 'Country' in df.columns and 'Confirmed' in df.columns:
    top10 = df.groupby('Country')['Confirmed'].sum().sort_values(ascending=False).head(10)

# Top 5 countries for pie chart
top5 = top10.head(5)
```

### Step 5: Visualization
```Python
# 1. Line Graph – Global Confirmed Trend
plt.figure(figsize=(10,5))
plt.plot(global_trend.index, global_trend.values)
plt.title("Global Trend of Confirmed COVID-19 Cases Over Time")
plt.xlabel("Date")
plt.ylabel("Total Confirmed Cases")
plt.grid(True)
plt.show()

# 2. Bar Chart – Top 10 Countries by Confirmed Cases
plt.figure(figsize=(10,5))
plt.bar(top10.index, top10.values)
plt.title("Top 10 Countries by Confirmed COVID-19 Cases")
plt.xlabel("Country")
plt.ylabel("Total Confirmed Cases")
plt.xticks(rotation=45)
plt.show()

# 3. Pie Chart – Top 5 Affected Countries
plt.figure(figsize=(8,8))
plt.pie(top5.values, labels=top5.index, autopct='%1.1f%%')
plt.title("Case Distribution of Top 5 Affected Countries")
plt.show()

# 4. Scatter Plot – Confirmed vs Deaths
plt.figure(figsize=(8,6))
plt.scatter(df['Confirmed'], df['Deaths'])
plt.title("Scatter Plot: Confirmed Cases vs Deaths")
plt.xlabel("Confirmed Cases")
plt.ylabel("Deaths")
plt.grid(True)
plt.show()

# 5. Histogram – Distribution of Active Cases
if 'Active' in df.columns:
    plt.figure(figsize=(8,6))
    plt.hist(df['Active'], bins=20)
    plt.title("Histogram of Active COVID-19 Cases")
    plt.xlabel("Active Cases")
    plt.ylabel("Frequency")
    plt.show()
else:
    print("\nNo 'Active' column found in dataset for Histogram.")
```


