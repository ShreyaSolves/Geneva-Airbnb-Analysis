# GENEVA Project - Analysis of Airbnb Listings in Geneva

## Overview  
The **GENEVA Project** analyzes Airbnb listings in Geneva, Switzerland, using a dataset (`geneva_listings.csv`) containing 2,458 listings across 75 features.  
The project explores **pricing patterns, neighborhood characteristics, and key factors influencing listing prices and amenities**, providing insights into Geneva's short-term rental market.

---

## Objectives  
- **Data Cleaning**: Handle missing values and preprocess the dataset.  
- **Exploratory Data Analysis (EDA)**: Summarize key metrics (price, accommodates, cleanliness scores) by neighborhood and room type.  
- **Visualization**: Highlight pricing trends, accommodation capacity, review scores, and correlations.  
- **Geospatial Analysis**: Map listings to analyze spatial distribution and price variations.  
- **Text Analysis**: Generate a word cloud from neighborhood descriptions.  
- **Predictive Modeling**:  
  - Regression models to predict listing prices.  
  - Classification model to predict the presence of amenities (e.g., TV).  
- **Model Evaluation**: Assess model performance and address skewness and class imbalance.  

---

## Dataset  
- **Source**: `geneva_listings.csv`  
- **Rows**: 2,458  
- **Columns**: 75  

### Key Features  
- **Numerical**: price, accommodates, bedrooms, bathrooms, number_of_reviews, review_scores_rating  
- **Categorical**: neighbourhood_cleansed, room_type  
- **Geospatial**: latitude, longitude  
- **Text**: neighborhood_overview  

---

## Methodology  

### Data Cleaning  
- Dropped columns with >50% missing values:  
  `license, neighbourhood_group_cleansed, calendar_updated, host_neighbourhood, neighbourhood, host_about`.  
- Imputed missing values:  
  - `bedrooms`, `bathrooms`: Median  
  - `host_response_time`: Mode  
- Cleaned `price` column (removed currency symbols, converted to numeric).  

### Exploratory Data Analysis  
- Summary statistics by neighborhood:  
  - Avg. price, accommodates, cleanliness, reviews, count of entire homes.  
- Commune de Genève: 1,322 entire home listings (dominant).  

### Visualizations  
- **Bar Plot**: Avg. price by neighborhood (Bellevue highest).  
- **Boxplot**: Price distribution by room type (entire homes most expensive).  
- **Strip Plot**: Accommodation capacity in top 5 neighborhoods.  
- **Line Plot**: Avg. review scores by neighborhood (Collex-Bossy, Puplinge = perfect).  
- **Correlation Heatmap**: Strong bedroom-bathroom-accommodates correlation; weak link between price and reviews.  
- **Scatter Map**: Listings spatial distribution with price gradient.  
- **Word Cloud**: Frequent terms like *lake*, *old town*, *quartier*.  

### Modeling  
#### Multiple Linear Regression (Price Prediction)  
- **Features**: accommodates, bedrooms, bathrooms, number_of_reviews, review_scores_rating, room_type, neighbourhood_cleansed.  
- **Initial model (raw price)**: R² = 0.051 (poor fit due to skewness).  
- **Log-transformed price**: R² = 0.423. Key predictors: accommodates, bedrooms, bathrooms, room_type.  

#### k-Nearest Neighbors (k-NN) Classification (TV Presence)  
- **Target**: `has_tv` (binary from amenities).  
- **Features**: accommodates, bedrooms, bathrooms, number_of_reviews, review_scores_rating.  
- **Accuracy**: 63.2% → ~68% after downsampling for class balance.  

### Evaluation  
- **Regression**: Adjusted R² = 0.410, p < 0.0001; condition number ~9420 (possible multicollinearity).  
- **Classification**: Accuracy ~68%; confusion matrix + classification report used.  

---

## Key Findings  
- **Pricing**: Entire homes/apartments command higher prices; Bellevue & Cologny are premium.  
- **Neighborhoods**: Commune de Genève dominates; Vernier & Meyrin show dispersed listings.  
- **Guest Satisfaction**: Smaller areas (Collex-Bossy, Puplinge) score higher reviews.  
- **Amenities**: TV presence moderately predictable (~68%).  
- **Market Segmentation**: Central = convenience-focused; periphery = upscale/premium.  

---

## Requirements  
- Python 3.x  
- Libraries:  
  ```bash
  pip install pandas numpy seaborn matplotlib plotly wordcloud scikit-learn statsmodels
