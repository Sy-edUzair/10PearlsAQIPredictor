# 🌍 Karachi Pearls AQI Predictor

An end-to-end machine learning system for predicting Air Quality Index (AQI) in Karachi, Pakistan using multi-horizon forecasting with LightGBM.

## 📋 Overview

This project implements a production-ready AQI prediction system that forecasts air quality 24, 48, and 72 hours ahead using historical pollution data, meteorological features, and advanced feature engineering techniques.

## 🗂️ Project Structure

- **`pearlsaqipredictor.py/PearlsAQIPredictor.ipynb`** - Main experimental notebook containing EDA, model experimentation, and initial development and everything. (THIS CONTAINS MAIN PROJECT LOGIC AND EVERYTHING)
- **`finalaqipredictor.py`** - Production workflow file with modular pipeline architecture for deployment and github workflows.
- **`requirements.txt`** - Python dependencies
- **`.github/workflows/`** - CI/CD automation for feature and training pipelines

## ✨ Key Features

- **Multi-Horizon Forecasting**: Predicts AQI for 24h, 48h, and 72h ahead
- **Real-Time Data Integration**: Fetches pollution data from OpenWeather API and meteorological data from Meteostat
- **Feature Store Integration**: Uses Hopsworks for scalable feature management
- **Advanced Feature Engineering**: Cyclical encodings, lag features, rolling statistics, and interaction terms
- **Production Dashboard**: Interactive Gradio interface for real-time predictions
- **Automated Pipelines**: Hourly feature updates and daily model retraining via GitHub Actions

## 🚀 Quick Start

### Installation

```bash
pip install -r requirements.txt
```

### Environment Variables

Create a `.env` file or set the following in COLAB:

```
OPENWEATHER_API_KEY=your_api_key
HOPSWORKS_API_KEY=your_api_key
```

### Running Pipelines

```bash
  run PearlsAQIPredictor.ipynb (has everything)
```
OR 
```bash
# Run feature pipeline (data collection & processing)
python finalaqipredictor.py --task feature

# Run training pipeline
python finalaqipredictor.py --task train

# Launch dashboard
python finalaqipredictor.py --task dashboard
```

## 📊 Model Performance
The project trained 3 models on a TimeSeriesSplit. These were the average performances:
       Model      RMSE      MAE       R2
RandomForest 12.012505 9.331104 0.782127
xgb          12.610045 9.813469 0.751713
lgbm         11.752731 9.176450 0.771479

Out which LightGBM was the best, hence it was trained on an holdout evaluation with a temporal split. The final LightGBM MultiOutput model achieves:

**aqi_24** (24 hour forecast): RMSE=19.128, MAE=12.321, R²=0.746
**aqi_48** (48 hour forecast): RMSE=22.074, MAE=15.418, R²=0.641
**aqi_72** (72 hour forecast): RMSE=22.392, MAE=16.368, R²=0.611

## 🔧 Technical Stack

- **ML Framework**: LightGBM with MultiOutputRegressor
- **Feature Store**: Hopsworks
- **Data Sources**: OpenWeather API, Meteostat
- **Frontend**: Gradio
- **Preprocessing**: PowerTransformer, StandardScaler
- **Orchestration**: GitHub Actions

## 📈 Key Features Used

- Pollutant concentrations (PM2.5, PM10, NO2, SO2)
- Meteorological data (temperature, humidity, pressure, wind speed)
- Temporal features (cyclical encodings for hour, day, month)
- Lag features (1-day, 2-day, 3-day AQI history)
- Rolling statistics (3-day mean and standard deviation)
- Interaction features (PM2.5×humidity, NO2×temperature)

## 🤝 Contributing

This project was developed as part of the 10Pearls Internship Program for the field of Data Sceience

## 📄 License

MIT License

## 📧 Contact

For questions or collaboration opportunities, please open an issue in the repository.

---

**Note**: See `REPORT.md` for detailed methodology, experiments, and research findings.
