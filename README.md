#  Coimbra Real Estate Price Prediction (2025)

This repository analyzes the residential real estate market in the **Coimbra district, Portugal**, and applies machine learning models to predict **apartment asking prices**, following a **CRISP-DM–based methodology**.

The project is based on a cleaned subset of the *Real Estate Listings in Portugal* dataset and focuses on understanding the drivers of housing prices, with particular attention to **energy efficiency**, **construction period**, **location**, and **property characteristics**.

---

##  Project Objectives

- Analyze price determinants in the Coimbra residential real estate market  
- Study the relationship between **energy certification** and property values  
- Build and compare machine learning models for price prediction  
- Benchmark model predictions against real market listings  

---

##  Dataset

- **Source:** Kaggle – *Real Estate Listings in Portugal (2024)*
- **Scope:** Coimbra district only
- **Property types:** Apartments and houses (ML stage restricted to apartments)

### Main Variables

**Target**
- `Price` (€)

**Structural & Size**
- LivingArea, TotalArea
- NumberOfBedrooms, NumberOfBathrooms
- ConstructionYear

**Energy & Amenities**
- EnergyCertificate
- Elevator
- Parking

**Location**
- City
- Town (parish-level)

---

##  Data Cleaning & Filtering

The cleaning process is grounded in **domain knowledge** and exploratory analysis:

- Coimbra district filtering  
- Residential properties only (Apartment / House)  
- Price cap at €500,000, defined based on an IQR (Tukey) outlier analysis to exclude extreme values and focus on the typical residential market.  
- Removal of physically inconsistent records:
  - TotalArea = 0
  - LivingArea < 16 m²
  - TotalRooms < 1
- Energy certificates `"NC"` treated as missing  
- Median imputation for TotalRooms  
- Extremely large properties excluded (TotalArea > 10,000 m²)

Final cleaned dataset: **3,937 properties**

---

##  Exploratory Data Analysis (EDA)

Key insights:

- Prices show a **right-skewed distribution**
- Strong positive relationship between:
  - Price ↔ ConstructionYear
  - Price ↔ NumberOfBathrooms
- Size-related variables are highly correlated → multicollinearity
- Significant spatial heterogeneity at **town level**
- Apartments are more expensive on average than houses
- Energy-efficient and newer buildings command higher prices

---

##  Machine Learning Models

Modeling restricted to **apartments only** (1,669 observations).

### Models Compared

| Model | MAE (€) | RMSE (€) | R² |
|------|--------|---------|----|
| Linear Regression | ~41,000 | ~54,500 | 0.66 |
| Random Forest | ~26,000 | ~39,000 | 0.83 |

**Random Forest** shows superior overall performance due to its ability to capture:
- Non-linear relationships
- Feature interactions
- Multicollinearity

---

##  Case Study Prediction

**Apartment configuration**
- Location: Santo António dos Olivais, Coimbra  
- LivingArea: 100 m²  
- TotalArea: 110 m²  
- Year: 2020  
- Bedrooms: 3  
- Bathrooms: 2  
- Parking: 1  
- Elevator: Yes  
- Energy Certificate: C  

### Predicted Prices

| Model | Predicted Price |
|-----|----------------|
| Linear Regression | €209,000 |
| Random Forest | €165,000 |

### Market Benchmark (Idealista)

- Comparable listings: €227,500 – €299,500  
- Models tend to **underestimate premium new-build apartments**, likely due to unobserved features (condition, floor level, views, neighborhood quality).

---

## Project Structure

```text
coimbra-real-estate-price-prediction-2025/
│
├── data/
│   ├── raw/
│   │   └── portugal_listinigs.csv
│   └── processed/
│       └── coimbra_clean.csv
│
├── notebooks/
│   ├── 01_data_loading_and_cleaning.ipynb
│   ├── 02_exploratory_data_analysis.ipynb
│   └── 03_modeling_and_evaluation.ipynb
│
├── src/
│   ├── __init__.py
│   ├── data_cleaning.py
│   ├── feature_engineering.py
│   ├── modeling.py
│   └── evaluation.py
│
├── figures/
│   ├── price_distribution.png
│   ├── spearman_correlation_heatmap.png
│   ├── city_average_prices.png
│   └── rf_real_vs_pred.png
│
├── requirements.txt
├── README.md
└── LICENSE

```
## How to Run the Project
```text
git clone https://github.com/joaofilipesilva-data/eda-ml-coimbra-real-estate-2025.git
cd eda-ml-coimbra-real-estate-2025
python3 -m venv .venv
source .venv/bin/activate   # On Windows: .venv\Scripts\activate
pip install -r requirements.txt

```
## Author
 João Silva 
Data Science for Management & Junior Data Analysts
Academic project focused on exploratory data analysis and machine learning applied to residential real estate price prediction in the Coimbra district (Portugal).



