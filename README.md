# 🌍 Karachi Pearls AQI Predictor

An end-to-end machine learning system for predicting Air Quality Index (AQI) in Karachi, Pakistan using multi-horizon forecasting with LightGBM.

## 📋 Overview

This project implements a production-ready AQI prediction system that forecasts air quality 24, 48, and 72 hours ahead using historical pollution data, meteorological features, and advanced feature engineering techniques.

## 🗂️ Project Structure

- **`pearlsaqipredictor.py`** - Main experimental notebook containing EDA, model experimentation, and initial development
- **`finalaqipredictor.py`** - Production workflow file with modular pipeline architecture for deployment
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

Create a `.env` file or set the following:

```
OPENWEATHER_API_KEY=your_api_key
HOPSWORKS_API_KEY=your_api_key
```

### Running Pipelines

```bash
# Run feature pipeline (data collection & processing)
python finalaqipredictor.py --task feature

# Run training pipeline
python finalaqipredictor.py --task train

# Launch dashboard
python finalaqipredictor.py --task dashboard
```

## 📊 Model Performance

The final LightGBM MultiOutput model achieves:

- **24h Forecast**: RMSE ~12-15, MAE ~8-10, R² ~0.85
- **48h Forecast**: RMSE ~15-18, MAE ~10-12, R² ~0.80
- **72h Forecast**: RMSE ~18-22, MAE ~12-14, R² ~0.75

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

This project was developed as part of the Karachi Pearls initiative for environmental monitoring.

## 📄 License

MIT License

## 📧 Contact

For questions or collaboration opportunities, please open an issue in the repository.

---

**Note**: See `REPORT.md` for detailed methodology, experiments, and research findings.
