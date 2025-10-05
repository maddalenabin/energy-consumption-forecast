# Energy Demand Prediction
This repository contains a prototype machine learning solution for forecasting hourly heat demand in a given area.  
The model predicts demand 24 hours ahead, using historical consumption and weather forecast data.  


## 🧠 Project Goal

- Predict hourly heat demand 24 hours ahead.
- Evaluate model performance for February 1–7, 2019.
- Prototype a baseline solution that can later be improved with more features and models.


## 📁 Repository Structure
```
├── 01-notebooks/
│ ├── 01-explore.ipynb # Data exploration and insights
│ ├── 02-feature.ipynb # Feature engineering
│ └── 03-modeling.ipynb # Model training, evaluation, and forecasting
│
├── 02-data/
│ ├── case-demand-prediction-nytt-data.csv # raw dataset
│ ├── data_cleaned_engineered_24h.csv 
│ └── data_cleaned_engineered.csv # cleaned and engineered data ready for modeling
│
└── README.md # Project documentation
```

## Data

- **Period:** 2012–2019  
- **Target:** `consumed_heat`  
- **Main features:**
  - Temperature (`temp`)
  - Cloud coverage (`cloud`)
  - Wind speed and direction (`wind_speed`, `wind_direction`)
  - Holiday indicators (`holiday_in_general`, `school_holiday_period`, `public_holiday_period`)
  - Temporal features (`hour`, `day`, `month`, `year`, `day_of_week`, `is_weekend`)
  - Lag features (`lag_24` — consumption from 24h before)


## Modeling

### Model
- **Algorithm:** `GradientBoostingRegressor`
- **Parameters:**  
  `n_estimators=300`, `learning_rate=0.1`, `max_depth=5`
- **Train/Test split:** 94% / 6% (first week of February 2019 used for testing)

### Performance
| Metric | Value |
|--------|--------|
| MAE | 0.76 kWh |
| RMSE | 1.08 |
| MSE | 1.18 |
| Avg. Demand | 21.0 kWh |
| Relative Error | 3.64% |

- The small gap between MAE and RMSE suggests no large outliers.  
- The model performs as a solid baseline for hourly forecasting.


## Insights

- Demand is negatively correlated with temperature: higher demand in colder weather.
- Seasonal and hourly patterns are strong.
- Public holidays slightly increase consumption, while school/general holidays reduce it.


## Next Steps

### Feature Engineering
- Add short-term lag (`lag_1`)
- Include temperature lag (24h) and forecast error.
- Combine holiday features into a single binary flag.

### Model Improvements
- Use train/validation/test split with Grid Search.
- Try XGBoost for faster training and built-in regularization (L1/L2).
- Analyze feature importance.

### Evaluation
- Compare predicted vs. actual demand over time.
- Analyze correlation between predicted demand and temperature.
- Check for overfitting using training/validation loss.
