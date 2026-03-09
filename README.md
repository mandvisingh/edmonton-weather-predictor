Here is a professional, high-impact `README.md` for your GitHub repository. It’s designed to showcase your technical decision-making and your growth as an AI/ML engineer.

---

# Edmonton Weather Predictor: 67-Year Time-Series Analysis

A Machine Learning project using **Random Forest Regression** to predict daily temperatures in Edmonton, Alberta, leveraging historical data from 1959 to 2026. This project focuses on solving common time-series challenges like data gaps, station transitions, and extreme volatility.

## 🚀 Key Results

* **Mean Absolute Error (MAE):** 2.73°C
* **R² Score:** 0.9124
* **Improvement over Baseline:** Outperformed the Persistence Baseline (predicting tomorrow is the same as today) by **0.13°C**.

## 🛠️ Tech Stack

* **Data Handling:** `Pandas`, `NumPy`, `JSON`
* **Machine Learning:** `Scikit-Learn` (RandomForestRegressor)
* **Data API:** Environment Canada Daily Climate API
* **Visualization:** `Matplotlib`, `Seaborn`

---

## 📈 Engineering Workflow

### 1. Data Rectification & Engineering

One of the core challenges was a raw dataset with significant missing days.

* **Dataset Expansion:** Used `.resample('D')` and **Linear Interpolation** to expand the dataset from 15,014 rows to **24,403 continuous days**.
* **Temporal Continuity:** Ensured that "Lag" features were mathematically correct by filling time gaps, allowing the model to have a consistent memory.

### 2. Feature Engineering

To help the model "understand" weather patterns, I engineered several domain-specific features:

* **Cyclical Time Features:** Transformed months into `Sine` and `Cosine` waves to represent the circular nature of seasons.
* **Memory Features:** Implemented `temp_lag_1` (yesterday's temperature) as the primary signal.
* **Momentum Features:** Added `temp_change_1d` to capture the velocity of temperature drops/rises (essential for Edmonton's cold fronts).

### 3. Model Optimization

The model was tuned to find the "Sweet Spot" between complexity and generalization:

* **Architecture:** Random Forest Regressor (`n_estimators=100`, `max_depth=15`).
* **Validation:** Used a chronological split (Train/Test) to ensure the model was tested on future data it hadn't seen before.
* **Analysis:** Used **Residual Plots** to identify that the model performs best on average days but tends to "regress toward the mean" during extreme polar vortex events.

---

## 📂 Project Structure

```text
├── data/
│   └── weather_data_interpolated.csv  # 24k+ rows of continuous data
├── notebooks/
│   └── Edmonton_Weather_ML.ipynb      # Full training and EDA pipeline
├── models/
│   └── weather_forest_v1.pkl          # Exported model for deployment
├── README.md
└── requirements.txt

```

---

## 🧠 Lessons Learned

* **Simplicity Wins:** Adding too many complex rolling averages actually increased the MAE (from 2.68 to 2.84). Returning to a leaner feature set improved accuracy and prevented overfitting.
* **Persistence Trap:** Beating the "Simple Guess" in weather is difficult. Every 0.1°C improvement requires significant feature refinement.
* **Data Integrity:** In time-series, a single missing day can break the "logic" of your lag features. Proper resampling is as important as the model itself.

---

## 🔮 Next Steps

* Implement an **LSTM (Long Short-Term Memory)** neural network to compare against the Random Forest.
* Integrate Barometric Pressure and Wind Speed to improve accuracy during sudden cold fronts.
* Deploy as a small React/Firebase web app to show real-time Edmonton forecasts.
