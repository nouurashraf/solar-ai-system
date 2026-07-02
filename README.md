#  Smart AI System for Solar Panel Energy Prediction and Fault Detection

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-R²%3D0.9994-orange.svg)
![Streamlit](https://img.shields.io/badge/Streamlit-Dashboard-red.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

A complete AI-powered system that predicts solar panel energy output and detects faults in real time using machine learning.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Dataset](#dataset)
- [Models](#models)
- [Results](#results)
- [Installation](#installation)
- [Usage](#usage)
- [Dashboard](#dashboard)
- [Technologies](#technologies)

---

## 🔍 Overview

This project builds an end-to-end AI system for solar power plants that:

1. **Predicts** the expected electricity output based on weather conditions
2. **Detects faults** such as partial shading, temperature anomalies, and faulty panels
3. **Visualizes** everything in an interactive dashboard

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| ⚡ Energy Prediction | Predicts AC Power output from weather data |
| 🚨 Fault Detection | Detects anomalies using Isolation Forest |
| 🌡️ Fault Classification | Classifies faults into Temperature Anomaly, Partial Shading, Low Efficiency |
| 📊 Interactive Dashboard | 4-page Streamlit app with live predictions |
| 📁 Batch Analysis | Upload CSV and get predictions for all records |

---

## 📁 Project Structure

```
solar-ai-system/
│
├── 📓 notebook/
│   └── smart-ai-system-solar.ipynb     ← Main Kaggle notebook (all phases)
│
├── 🖥️ app/
│   └── app.py                          ← Streamlit dashboard
│
├── 📊 data/                            ← (not included - download from Kaggle)
│   ├── Plant_1_Generation_Data.csv
│   ├── Plant_1_Weather_Sensor_Data.csv
│   ├── Plant_2_Generation_Data.csv
│   └── Plant_2_Weather_Sensor_Data.csv
│
├── 🤖 models/                          ← Trained model files
│   ├── xgb_model.pkl
│   ├── iso_forest.pkl
│   └── scaler_fault.pkl
│
├── 📈 output/                          ← Generated output files
│   ├── powerbi_main.csv
│   ├── powerbi_daily.csv
│   ├── powerbi_faults.csv
│   └── model_comparison.csv
│
├── requirements.txt
├── .gitignore
└── README.md
```

---

## 📦 Dataset

**Source:** [Solar Power Generation Data — Kaggle](https://www.kaggle.com/datasets/anikannal/solar-power-generation-data)

| Property | Value |
|----------|-------|
| Records | 136,476 |
| Plants | 2 |
| Inverters | 22 per plant |
| Period | 34 days (May–June 2020) |
| Frequency | Every 15 minutes |

**Features used:**

| Feature | Description |
|---------|-------------|
| `IRRADIATION` | Solar irradiance (W/m²) |
| `AMBIENT_TEMPERATURE` | Ambient temperature (°C) |
| `MODULE_TEMPERATURE` | Panel temperature (°C) |
| `HOUR_SIN / HOUR_COS` | Cyclical hour encoding |
| `TEMP_DIFF` | Module - Ambient temperature |
| `AC_POWER_LAG1/2/3` | Previous power readings |

---

## 🤖 Models

### Phase 2 — Forecasting

| Model | MAE (kW) | RMSE (kW) | R² |
|-------|----------|-----------|-----|
| Random Forest | 11.49 | 25.20 | 0.9941 |
| **XGBoost ✅** | **3.29** | **8.35** | **0.9994** |
| LSTM | 57.31 | 133.15 | 0.8358 |

**Winner: XGBoost** — R² = 0.9994 (explains 99.94% of variance)

### Phase 3 — Fault Detection

**Model:** Isolation Forest (`contamination=0.05`)

| Fault Type | Count |
|-----------|-------|
| Temperature Anomaly | 1,923 |
| General Anomaly | 1,511 |
| Partial Shading / Faulty Panel | 10 |
| **Total** | **3,444** |

---

## 📊 Results

```
┌─────────────────────────────────────────┐
│         XGBoost Final Results           │
├─────────────────────────────────────────┤
│  MAE  :  3.29 kW                        │
│  RMSE :  8.35 kW                        │
│  R²   :  0.9994  (99.94% accuracy)      │
│  Max Power : 1,410 kW                   │
└─────────────────────────────────────────┘
```

---

## ⚙️ Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/solar-ai-system.git
cd solar-ai-system

# Install dependencies
pip install -r requirements.txt
```

---

## 🚀 Usage

### Run the Dashboard

```bash
cd app
streamlit run app.py
```

Open your browser at `http://localhost:8501`

### Run the Notebook

Upload `notebook/smart-ai-system-solar.ipynb` to [Kaggle](https://kaggle.com) and add the dataset.

---

## 🖥️ Dashboard

The Streamlit app has 4 pages:

| Page | Description |
|------|-------------|
| 🏠 Overview | Project summary, model comparison, architecture |
| 🔮 Live Prediction | Real-time power prediction with gauge chart |
| 🚨 Fault Detection | Fault classification with alerts |
| 📊 Batch Analysis | Upload CSV and download predictions |

---

## 🛠️ Technologies

| Category | Tools |
|----------|-------|
| Language | Python 3.8+ |
| ML Models | XGBoost, Random Forest, LSTM, Isolation Forest |
| Deep Learning | TensorFlow / Keras |
| Dashboard | Streamlit, Plotly |
| Data Processing | Pandas, NumPy, Scikit-learn |
| Visualization | Matplotlib, Seaborn |
| BI Tool | Microsoft Power BI |

---

## 🏗️ System Architecture

```
Weather Sensors
(Irradiation, Temperature, Humidity)
        ↓
Feature Engineering
(18 features: time, physical, lag)
        ↓
┌──────────────────┐    ┌──────────────────┐
│ XGBoost          │    │ Isolation Forest │
│ Forecasting      │    │ Fault Detection  │
│ R² = 0.9994      │    │ 3,444 faults     │
└──────────────────┘    └──────────────────┘
        ↓                        ↓
Predicted Power (kW)      Fault Type & Alert
        ↓                        ↓
════════════════════════════════════════
         Smart Solar Dashboard
     (Streamlit + Power BI)
════════════════════════════════════════
```

---

## 👩‍💻 Author

**Nour Ashraf**
New Mansoura University

---

## 📄 License

This project is licensed under the MIT License.
