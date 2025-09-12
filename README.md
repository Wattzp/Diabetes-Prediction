# Diabetes-Prediction
This dataset is designed to facilitate the prediction of diabetes based on various diagnostic measurements. It contains health-related features of individuals and a binary outcome variable indicating whether they have diabetes. This dataset is well-suited for practicing binary classification tasks.

## Table of Contents

- [INTRODUCTION](#introduction)  
- [OBJECTIVES](#objectives)  
- [DATA CLEANING TASKS](#data-cleaning-tasks)  
- [EXPLORATORY DATA ANALYSIS](#exploratory-data-analysis)  
- [DASHBOARD REPORTING](#dashboard-reporting)  
- [Tech Stack](#tech-stack)  
- [Key Findings](#key-findings)
- [Conclusion](#conclusion)   
- [License](#license)  

---


## INTRODUCTION
Diabetes is among the most prevalent chronic diseases in the United States, impacting millions of Americans each year and exerting a significant financial burden on the economy. Diabetes is a serious chronic disease in which individuals lose the ability to effectively regulate levels of glucose in the blood, and can lead to reduced quality of life and life expectancy. After different foods are broken down into sugars during digestion, the sugars are then released into the bloodstream. This signals the pancreas to release insulin. Insulin helps enable cells within the body to use those sugars in the bloodstream for energy. Diabetes is generally characterized by either the body not making enough insulin or being unable to use the insulin that is made as effectively as needed.

Complications like heart disease, vision loss, lower-limb amputation, and kidney disease are associated with chronically high levels of sugar remaining in the bloodstream for those with diabetes. While there is no cure for diabetes, strategies like losing weight, eating healthily, being active, and receiving medical treatments can mitigate the harms of this disease in many patients. Early diagnosis can lead to lifestyle changes and more effective treatment, making predictive models for diabetes risk important tools for public and public health officials.

The scale of this problem is also important to recognize. The Centers for Disease Control and Prevention has indicated that as of 2018, 34.2 million Americans have diabetes and 88 million have prediabetes. Furthermore, the CDC estimates that 1 in 5 diabetics, and roughly 8 in 10 prediabetics are unaware of their risk. While there are different types of diabetes, type II diabetes is the most common form and its prevalence varies by age, education, income, location, race, and other social determinants of health. Much of the burden of the disease falls on those of lower socioeconomic status as well. Diabetes also places a massive burden on the economy, with diagnosed diabetes costs of roughly $327 billion dollars and total costs with undiagnosed diabetes and prediabetes approaching $400 billion dollars annually.

## OBJECTIVES

- Provide a clear overview of the diabetes dataset, including its structure, key features, and clinical context.  
- Clean and preprocess the data by handling missing or zero-value entries, normalizing distributions, and engineering derived features (e.g., age bands, BMI categories).  
- Perform exploratory data analysis to uncover patterns and relationships—using summary statistics, pivot tables, and visualizations—to identify the strongest predictors of diabetes.  
- Build and compare multiple binary classification models (e.g., logistic regression, decision trees, ensemble methods), tuning hyperparameters and assessing performance with metrics such as accuracy, precision, recall, and AUC.  
- Interpret model results to highlight the most influential risk factors, and package the best model in an interactive dashboard for real-time risk assessment and stakeholder reporting.  

## Data Cleaning Tasks

- Replace zeroes with missing values  
  - In **Glucose**, **BloodPressure**, **SkinThickness**, **Insulin**, and **BMI**, convert 0 entries to `NaN` to distinguish true zeroes from missing measurements.  

- Impute missing data  
  - For each feature with `NaN`, choose an imputation strategy (e.g., median for skewed distributions like Insulin, mean for roughly symmetric features).  

- Remove duplicate records  
  - Identify and drop any rows that repeat all feature values to ensure each patient appears only once.  

- Validate and convert data types  
  - Ensure all medical measurements are numeric and **Outcome** is stored as an integer or categorical type.  

- Detect and handle outliers  
  - Use the 1.5 × IQR rule on key features (Glucose, BMI, Age) to flag extreme values, then decide whether to cap, transform, or remove them.  

- Create derived features  
  - Engineer an **AgeGroup** column (e.g., “20–29”, “30–39”) and a **BMICategory** (e.g., underweight, normal, overweight, obese) for stratified analysis.  

- Scale or normalize features  
  - Apply standard scaling or min–max normalization to continuous predictors before modeling to ensure comparability of coefficients and improve algorithm convergence.  

- Verify clinical value ranges  
  - Check that all measurements fall within plausible medical bounds (e.g., 0 < Glucose < 300) and correct or remove entries outside those limits.  

- Document cleaning steps  
  - Record each transformation and imputation in a data‐processing script or notebook, and export the final cleaned dataset as `diabetes_cleaned.csv`.


## Exploratory Data Analysis
---

### 1. Setup

```python
import pandas as pd, numpy as np
import matplotlib.pyplot as plt, seaborn as sns

sns.set(style="whitegrid")
plt.rcParams["figure.figsize"] = (10, 6)

df = pd.read_csv("diabetes.csv")
```

---

### 2. Data Overview

```python
df.shape
df.dtypes
df.head()
df.describe().T
```

---

### 3. Missing & Zero Values

```python
(df == 0).sum()
(df == 0).mean() * 100
```

---

### 4. Univariate Analysis

```python
df.drop("Outcome", axis=1).hist(bins=20, edgecolor="k")
plt.tight_layout(); plt.show()

for col in df.columns[:-1]:
    sns.boxplot(x="Outcome", y=col, data=df)
    plt.title(f"{col} by Outcome"); plt.show()
```

---

### 5. Correlation & Pairplot

```python
sns.heatmap(df.corr(), annot=True, cmap="coolwarm")
plt.title("Correlation Matrix"); plt.show()

sns.pairplot(df, hue="Outcome", vars=["Glucose","BMI","Age","Insulin"])
plt.show()
```

---

### 6. Outlier Detection

```python
Q1 = df.quantile(0.25)
Q3 = df.quantile(0.75)
IQR = Q3 - Q1

outliers = ((df < (Q1 - 1.5 * IQR)) | (df > (Q3 + 1.5 * IQR))).sum()
outliers
```

---

### 7. Outcome-Based Feature Differences

```python
pos, neg = df[df.Outcome==1], df[df.Outcome==0]
{col: pos[col].mean() - neg[col].mean() for col in df.columns[:-1]}
```

---

## DASHBOARD REPORTING 


![DiabetesPredictiion](https://github.com/user-attachments/assets/41614404-80a2-4d80-80aa-945df7ad3b7d)



## Tech Stack

Python | Pandas | Seaborn | Plotly | Excel | Jupyter Notebook [Download Here](https://www.anaconda.com/download)

### 📊 Visualization Tools Used  
- **Seaborn & Matplotlib** for static plots  
- **Plotly Express** for interactive dashboards  
- **Pivot Tables in Excel** for grouped summaries and prevalence analysis

---

## Key Findings

#### 1. **Glucose Levels as Primary Indicator**  
- Diabetic patients consistently exhibit higher glucose readings.  
- Histogram and scatter plots show a clear separation between diabetic and non-diabetic groups, confirming glucose as the most predictive feature.

#### 2. **BMI and Age Influence Risk**  
- Boxplots reveal that individuals with diabetes tend to have higher BMI values.  
- Age-based analysis shows diabetes prevalence increases sharply after age 40, with the highest rates in the 50–69 age group.

#### 3. **Insulin and Skin Thickness Variability**  
- Scatter plots show wide variation in insulin levels among diabetics, suggesting different subtypes or stages of insulin resistance.  
- Skin thickness correlates moderately with BMI, indicating its role in obesity-related risk.

#### 4. **Feature Relationships via Correlation Matrix**  
- Strong positive correlations observed between Glucose, BMI, Age, and the diabetes outcome.  
- Weak correlations for BloodPressure and SkinThickness suggest limited predictive power.

#### 5. **Scatter Matrix Reveals Clustering**  
- Interactive Plotly scatter matrix shows diabetic patients clustering in high-glucose and high-BMI regions.  
- Hover features allow patient-level inspection, enhancing interpretability.

#### 6. **Class Imbalance in Outcome Distribution**  
- Count plots confirm a 65:35 split between non-diabetic and diabetic cases.  
- This imbalance is crucial for model training and evaluation strategies.

---

### Conclusion  
These visualizations provide strong evidence that glucose, BMI, and age are the most influential features in predicting diabetes. The insights gained here lay the foundation for effective model building and real-time risk assessment tools.

---
## License
MIT License

Copyright (c) 2025 [Wattzp](https://github.com/Wattzp)

Permission is hereby granted, free of charge, to any person obtaining a copy  
of this software and associated documentation files (the "Software"), to deal  
in the Software without restriction, including without limitation the rights  
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell  
copies of the Software, and to permit persons to whom the Software is  
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all  
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR  
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,  
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE  
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER  
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,  
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE  
SOFTWARE.



