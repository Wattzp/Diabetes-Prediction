# Diabetes-Prediction
This dataset is designed to facilitate the prediction of diabetes based on various diagnostic measurements. It contains health-related features of individuals and a binary outcome variable indicating whether they have diabetes. This dataset is well-suited for practicing binary classification tasks.

## Table of Contents

- [INTRODUCTION](#introduction)  
- [OBJECTIVES](#objectives)  
- [DATA CLEANING TASKS](#data-cleaning-tasks)  
- [EXPLORATORY DATA ANALYSIS](#exploratory-data-analysis)  
- [DASHBOARD REPORTING](#dashboard-reporting)  
- [Tech Stack](#tech-stack)  
- [Key Findings from Snitch Fashion Sales Visualizations](#Key-Findings-from-Snitch-Fashion-Sales-Visualizations)    
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











