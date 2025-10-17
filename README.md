# 🏠 Bengaluru Home Price Prediction

An end-to-end **Machine Learning project** to predict house prices in **Bengaluru, India**, using regression models.  
This notebook demonstrates the full workflow from **data cleaning to deployment**.

---

## 📘 Overview

This project takes a real estate dataset from Bengaluru and:
- Cleans and preprocesses the data
- Removes outliers and inconsistent records
- Performs feature engineering
- Builds and evaluates regression models
- Exports the model for deployment (e.g., in a Flask web app)

The goal is to predict property prices based on **location**, **square footage**, **number of bedrooms (BHK)**, and **bathrooms**.

---

## 🧠 Dataset Description

Each row in the dataset represents a house listing with the following attributes:

| Column | Description |
|--------|--------------|
| `area_type` | Type of area (Super built-up, Plot, etc.) |
| `availability` | Availability status |
| `location` | Locality in Bengaluru |
| `size` | Number of bedrooms (e.g., 2 BHK) |
| `society` | Society name |
| `total_sqft` | Total area in square feet |
| `bath` | Number of bathrooms |
| `balcony` | Number of balconies |
| `price` | Price in lakhs |

---

## ⚙️ Steps Performed

### 1️⃣ Data Cleaning
- Dropped less useful columns (`area_type`, `society`, `availability`, `balcony`)
- Filled or removed missing values
- Converted `size` to numeric (BHK count)
- Cleaned `total_sqft` by averaging ranges like “2100–2850”

### 2️⃣ Feature Engineering
- Created a new feature `price_per_sqft`
- Reduced rare locations to an “other” category
- Removed unrealistic data (e.g., very small area per BHK)
- Removed inconsistent records (e.g., 2BHK costlier than 3BHK in same location)

### 3️⃣ Model Building
- Applied **Linear Regression** as the base model  
- Compared with **Lasso** and **Decision Tree Regressor** using GridSearchCV
- Evaluated using **cross-validation (ShuffleSplit)**

### 4️⃣ Model Export
- Saved the model using `pickle` or `joblib`
- Stored column metadata in `columns.json`
- Defined helper function:
  ```python
  def predict_home_price(location, sqft, bath, bhk):
      # Returns estimated price for given parameters
