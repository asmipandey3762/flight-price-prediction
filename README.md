# ✈️ Flight Price Prediction using Machine Learning

Predictive Analytics project — predicting flight ticket prices in India using 5 different regression models and comparing their performance.

## 📌 About the Project

Flight ticket prices keep changing based on airline, route, timing, class and how early we book. The aim of this project is to predict the `price` of a flight ticket using these features.

Complete workflow followed:
1. **Data Cleaning** – removing unwanted columns, missing values, duplicates, category check and outlier removal
2. **Exploratory Data Analysis (EDA)** – class wise, airline wise, days left, stops, timings and route wise analysis
3. **Feature Engineering** – label/ordinal encoding + one hot encoding
4. **Model Building** – 5 regression models
5. **Model Evaluation** – R² Score, MSE, RMSE, MAE + 5-fold Cross Validation

## 📊 Dataset

- **Name:** Flight Price Prediction (EaseMyTrip)
- **Source:** Kaggle — [shubhambathwal/flight-price-prediction](https://www.kaggle.com/datasets/shubhambathwal/flight-price-prediction)
- **Rows:** 3,00,153 | **Columns:** 12
- Data scraped from EaseMyTrip for flights between 6 metro cities — Delhi, Mumbai, Bangalore, Kolkata, Hyderabad, Chennai (Feb–Mar 2022)

| Column | Description |
|---|---|
| airline | 6 airlines – Vistara, Air India, Indigo, GO FIRST, AirAsia, SpiceJet |
| flight | Flight code (dropped) |
| source_city / destination_city | From and to city |
| departure_time / arrival_time | Time slot (Early Morning, Morning, ... Late Night) |
| stops | zero / one / two_or_more |
| class | Economy or Business |
| duration | Total travel time in hours |
| days_left | Days between booking and travel date |
| **price** | **Ticket price in ₹ (Target)** |

## 🤖 Models Used

1. Linear Regression
2. Ridge Regression
3. Decision Tree Regressor
4. Random Forest Regressor
5. XGBoost Regressor

## 📈 Results

| Rank | Model | R² Score (Accuracy) | MSE | RMSE (₹) | MAE (₹) | 5-Fold CV R² |
|---|---|---|---|---|---|---|
| 1 | **XGBoost** | **0.9874 (98.74%)** | 65,38,317 | 2,557 | 1,342 | 0.9795 |
| 2 | Random Forest | 0.9864 (98.64%) | 70,46,288 | 2,654 | 1,119 | 0.9785 |
| 3 | Decision Tree | 0.9811 (98.11%) | 97,88,739 | 3,129 | 1,419 | 0.9695 |
| 4 | Linear Regression | 0.9096 (90.96%) | 4,67,61,203 | 6,838 | 4,536 | 0.9098 |
| 5 | Ridge Regression | 0.9096 (90.96%) | 4,67,61,199 | 6,838 | 4,536 | 0.9098 |

> Since this is a regression problem, R² score is used as accuracy.

**XGBoost performed the best** with 98.74% R² score and the lowest MSE/RMSE. On average its prediction is off by only ~₹1,342 (MAE). Cross validation scores are very close to test scores, so the model is stable.

## 🌐 Live Demo

**👉 Netlify:** https://flight-price-prediction-asmi.netlify.app
**👉 Render:** https://flight-price-prediction.onrender.com

Select source/destination city, airline, class, stops, timings and days left — the trained XGBoost model predicts the ticket price instantly in the browser. It also shows a chart of how the fare changes if you book on a different day. (Website code is in the `docs/` folder.)

### Deploy your own copy

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/asmipandey3762/flight-price-prediction)
[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/asmipandey3762/flight-price-prediction)

Both platforms read their settings from the repo (`netlify.toml` and `render.yaml`) and publish the `docs/` folder as a static site — no build step needed.

## 📄 Project Report

The complete 45-page project report (dataset, cleaning, EDA, models, results, web demo) is in the `report/` folder — [PDF](report/Flight_Price_Prediction_Report.pdf) | [Word](report/Flight_Price_Prediction_Report.docx).

## 🔍 Key Insights

- **Class** is the biggest factor – Business class tickets are ~8x costlier than Economy
- Tickets booked in the **last 1-2 weeks** are much costlier, prices are lowest 15+ days before travel
- **Non-stop** and **late night** flights are generally cheaper
- **Vistara and Air India** are the costliest airlines, **AirAsia and Indigo** the cheapest
- Linear models are not enough because the relation between days left / duration and price is non-linear
- Tree based ensemble models (Random Forest, XGBoost) give the best results

## 🛠️ Tech Stack

Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost, Jupyter Notebook

## ▶️ How to Run

```bash
git clone https://github.com/asmipandey3762/flight-price-prediction.git
cd flight-price-prediction
pip install -r requirements.txt
jupyter notebook Flight_Price_Prediction.ipynb
```

## 📁 Project Structure

```
├── Flight_Price_Prediction.ipynb   # main notebook (cleaning, EDA, models)
├── Clean_Dataset.csv               # dataset (from Kaggle)
├── docs/
│   ├── index.html                  # interactive demo webpage
│   └── model.json                  # trained XGBoost model exported for the webpage
├── report/
│   ├── Flight_Price_Prediction_Report.pdf
│   └── Flight_Price_Prediction_Report.docx
├── netlify.toml                    # Netlify deploy config
├── render.yaml                     # Render deploy config
├── requirements.txt
└── README.md
```

## 🚀 Future Scope

- Hyperparameter tuning using GridSearchCV
- Try LightGBM and CatBoost
- Collect data for more cities (currently 6 metro cities / 30 routes) and a longer time period
- Deploy as a web app using Streamlit where user enters flight details and gets the predicted price

---
Made by **Asmi Pandey** ✨
