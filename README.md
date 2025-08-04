
# 🚀 Military Base Clustering and Analysis using Big Data Tools

**Capstone Project – INSY 8413 | Introduction to Big Data Analytics**  
**Academic Year**: 2024–2025, Semester III  
**Prepared by**: Milindi Shema David  
**Student ID**: 25914

---

## 📘 Project Overview

This project focuses on analyzing U.S. Department of Defense (DoD) military base data using **Python** and **Power BI** to:

- Explore the geographical and operational patterns of military installations
- Apply **unsupervised machine learning (KMeans clustering)** to group similar bases
- Design an **interactive and visually appealing Power BI dashboard**
- Demonstrate the power of Big Data tools in solving real-world government sector problems

---

## 🏛️ Selected Sector

> ✅ **Government**

This dataset belongs to the transportation/government domain and offers insights into the spatial and administrative structure of military sites.

---

## ❓ Problem Statement

**How can clustering and exploratory data analytics help understand the operational distribution and geographical spread of U.S. military installations across different states and military branches?**

---

## 📂 Dataset Information

- **Dataset Title**: Military Bases
- **Source**: [USDOT Open Data - Military Bases](https://geodata.bts.gov/datasets/usdot::military-bases/explore)
- **File Format**: CSV
- **Rows & Columns**: ~2,000 rows × 6 main attributes used
- **Data Type**: Structured
- **Preprocessing Required**: ✅ Yes

---

## 🧪 Python Analytics (Jupyter Notebook)

All analysis was conducted in `military_bases.ipynb` using the following steps:

---

### 🔹 1. Import Libraries and Load CSV

```python
import pandas as pd
df = pd.read_csv("NTAD_Military_Bases.csv")
```

> **Why?** To read and inspect the original structured CSV file into a manageable DataFrame.

---

### 🔹 2. Data Cleaning & Column Selection

```python
df_clean = df[[
    'Site Name',
    'Site Operational Status',
    'Site Reporting Component Code',
    'State Name Code',
    'Shape__Area',
    'Shape__Length'
]].copy()

df_clean.columns = ['site_name', 'status', 'component', 'state', 'area', 'length']
df_clean.dropna(inplace=True)
df_clean['component'] = df_clean['component'].str.strip().str.upper()
```

> **Why?**
> - Reduce to relevant columns only
> - Standardize naming for consistency
> - Remove missing data for model reliability

---

### 🔹 3. Exploratory Data Analysis (EDA)

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Bar chart: bases by component
sns.countplot(data=df_clean, x='component')

# Histogram: area distribution
sns.histplot(df_clean['area'], bins=30, kde=True)
```

> **Why?**  
> To visualize distribution and frequency across different dimensions like branch (component), state, and base size.

---

### 🔹 4. Feature Engineering for Clustering

```python
from sklearn.preprocessing import LabelEncoder

df_clean['component_code'] = LabelEncoder().fit_transform(df_clean['component'])
df_clean['status_code'] = LabelEncoder().fit_transform(df_clean['status'])
```

> **Why?**  
> Machine learning algorithms need numerical input. Label encoding converts categorical values to integers.

---

### 🔹 5. KMeans Clustering

```python
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score

X = df_clean[['component_code', 'status_code', 'area', 'length']]
kmeans = KMeans(n_clusters=3, random_state=42)
df_clean['cluster'] = kmeans.fit_predict(X)
silhouette_score(X, df_clean['cluster'])
```

> **Why?**  
> KMeans was used to group similar bases. Silhouette Score evaluates the cohesion and separation of clusters.

---

### 🔹 6. Export Data for Power BI

```python
df_clean.to_csv("cleaned_military_bases.csv", index=False)
```

> **Why?**  
> Exported clean and enriched data (with clusters) to a CSV file for use in Power BI dashboarding.

---

## 📊 Power BI Dashboard

### 🟨 Page 1: Military Base Overview
- **Card**: Total base count
- **Donut Chart**: Distribution by operational status (`status`)
- **Bar Chart**: Bases per branch (`component`)
- **Map**: Count of bases per state (`state`)

### 🟦 Page 2: Clustering Insights
- **Scatter Plot**: Area vs Length colored by `cluster`
- **Bar Chart**: Base count per cluster
- **Slicer**: Cluster filter
- **Cluster Summary Table**: Avg. area and length by cluster

### 🟥 Page 3: Drilldown by State & Component
- **Matrix Table**: State × Component base counts
- **Bar Chart**: Base count
- **Slicers**: For component and status
- **Drillthrough Page**: Base details per selected state

---

## 🧠 Innovation Features

| Feature             | Description |
|---------------------|-------------|
| 🎯 Cluster Labeling  | DAX calculated column to explain cluster groups |
| 🗺 Custom Tooltips   | Visuals include interactive custom hover tooltips |
| 🎨 Theming           | Custom color scheme aligned with U.S. military colors |

---

---

## 📢 Final Remarks

This project demonstrates the application of **Python**, **Machine Learning**, and **Power BI** to solve a real-world government problem using public data and Big Data analytics tools. It showcases data cleaning, visualization, clustering, and insight communication effectively.

---

## 📧 Submission

Prepared by: **Milindi Shema David**  
Student ID: **25914**  
Course: **INSY 8413 – Introduction to Big Data Analytics**  
Instructor: **Eric Maniraguha**  
Academic Year: 2024–2025, Semester III

---

> _"Whatever you do, work at it with all your heart, as working for the Lord, not for human masters." — Colossians 3:23_
