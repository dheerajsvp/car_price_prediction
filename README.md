# Used Car Price Prediction

A machine learning web app that estimates the resale price of a used car from its year, showroom price, mileage, fuel type, seller type, transmission, and ownership history.

**Live app:** _add your Streamlit Cloud link here once deployed_

## Overview

Used car prices depend on many interacting factors, and sellers often over- or under-price their cars relative to the market. This project trains a regression model on historical resale data and serves it through an interactive Streamlit interface, so a user can enter their car's details and get an instant price estimate.

## Approach

1. **Data cleaning and preparation** — encoded categorical features (fuel type, seller type, transmission) and split the data into training and test sets.
2. **Model comparison** — trained and evaluated three regression models to compare a simple linear baseline against models that can capture non-linear pricing patterns:

   | Model | R² | MAE (Lakhs) | RMSE (Lakhs) |
   |---|---|---|---|
   | Linear Regression | 0.84 | 1.27 | 1.71 |
   | Lasso Regression | 0.85 | 1.19 | 1.66 |
   | **Random Forest** | **0.96** | **0.48** | **0.86** |

3. **Feature importance** — Random Forest attributes ~88% of its predictive power to the car's current showroom price, followed by manufacturing year and kilometers driven, which matches how used car pricing works in practice.
4. **Deployment** — the best-performing model (Random Forest) is saved with `joblib` and served through a Streamlit app (`car_app.py`) with a sidebar for input and a live price estimate, expected price range, and a gauge visualization.

## Dataset

`car_data.csv` — 301 used car listings with the following fields: `Car_Name`, `Year`, `Selling_Price`, `Present_Price`, `Kms_Driven`, `Fuel_Type`, `Seller_Type`, `Transmission`, `Owner`.

## Tech stack

Python, Pandas, NumPy, Scikit-learn, Streamlit, Plotly, joblib

## Running locally

```bash
git clone https://github.com/dheerajsvp/car_price_prediction.git
cd car_price_prediction
pip install -r requirements.txt
streamlit run car_app.py
```

The trained model (`car_prediction_model.pkl`) is already included, so the app runs immediately without retraining.

## Project structure

```
├── car_app.py                  # Streamlit app
├── car_prediction_model.pkl    # Trained Random Forest model
├── car_data.csv                # Training data
├── requirements.txt
└── README.md
```

## Possible improvements

- Retrain with a larger, more recent dataset covering more makes and models
- Add engine size and horsepower as features
- Deploy to Streamlit Community Cloud for a live demo link
