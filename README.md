# sentinel_ai_gateway
Sentinel AI Gateway is a hybrid edge-AI predictive maintenance system using MPU6050 and DHT11 on Arduino for real-time RMS/Kurtosis extraction. A TensorFlow LSTM model classifies machine health as SAFE/WARNING/CRITICAL. A local digital twin (Flask) stores state and a Streamlit dashboard visualizes live system data.

# Sentinel AI Gateway  
### A Hybrid Edge–Based Predictive Maintenance & Digital Twin System  
**Team Skyantra — Shashi Kumar C • Ronak Soni • Nainshi**  
Technognition 2025 — ProtoThon (Theme: Circuit Minds)

---

## Overview
Sentinel AI Gateway is a full-stack hybrid edge–AI predictive maintenance system built using Arduino, MPU6050, DHT11, TensorFlow LSTM, and a Local Digital Twin.  
It performs real-time vibration analysis, feature extraction, anomaly detection, and state synchronization with a live dashboard.

This project demonstrates a complete Industry 4.0 pipeline from sensing → AI inference → digital twin → visualization.

---

## 🛠️ Hardware Components
| Component | Purpose |
|----------|---------|
| **Arduino UNO** | Edge data acquisition and preprocessing |
| **MPU6050** | 3-axis vibration sensor for RMS/Kurtosis |
| **DHT11** | Temperature sensor |
| **USB Serial** | Data transfer to inference engine |

---

## 📡 Edge Signal Processing

### ✔ Sampling
- 128 accelerometer samples per inference window  
- Continuous rolling buffer

 RMS = sqrt( (1/N) * Σ xi² )

### ✔ RMS (Root Mean Square)


Kurtosis = Σ(xi - μ)⁴ / (N * σ⁴)



### ✔ Arduino Output Format


---

## 🤖 Machine Learning — TensorFlow LSTM
A time-series LSTM classifier predicts machine health using 128×3 feature windows.

### Model Architecture
```python
model = keras.Sequential([
    keras.layers.Input((128,3)),
    keras.layers.LSTM(64),
    keras.layers.Dense(32, activation='relu'),
    keras.layers.Dense(1, activation='sigmoid')
])

Output


Probability of fault between 0–1


State Logic
ProbabilityState< 0.5SAFE0.5–0.85WARNING≥ 0.85CRITICAL
Training


Script: train_tf.py


Model saved as:


model_tf/model.h5
model_tf/meta.json

Dataset used:
synthetic_dataset.csv


🛰️ Real-Time Inference Pipeline
Script: test_serial_tf.py
Handles:


Serial read


Feature normalization


TensorFlow inference


Posting results to digital twin backend


Printing system state


Example Output
[WARNING] p=0.721  RMS=0.01245  KURT=6.91  TEMP=31.2


🏭 Local Digital Twin Backend (Flask)
Script: local_twin.py
Responsibilities:


Store real-time machine state


Maintain history buffer


Provide REST API for dashboard


Synchronize ML inference and visualization


JSON Payload Example
{
  "rms": 0.0123,
  "kurtosis": 7.42,
  "temperature": 32.1,
  "probability": 0.88,
  "state": "CRITICAL"
}


📊 Real-Time Dashboard (Streamlit)
Script: twin_dashboard.py
Shows:


RMS trend


Kurtosis trend


Temperature


Fault probability


System state indicator


Digital twin history


Run:
streamlit run twin_dashboard.py


📁 Repository Structure
Sentinel-AI-Gateway/
│
├── model_utils_tf.py        # TensorFlow model utilities
├── train_tf.py              # LSTM training script
├── test_serial_tf.py        # Real-time inference
├── local_twin.py            # Digital Twin backend
├── twin_dashboard.py        # Visualization dashboard
│
├── model_tf/
│   ├── model.h5
│   └── meta.json
│
├── synthetic_dataset.csv
└── README.md


🔧 How to Run the Full System
1️⃣ Upload Arduino Code
Using RMS + Kurtosis extraction.
2️⃣ Train ML Model
python train_tf.py

3️⃣ Start Digital Twin Backend
python local_twin.py

4️⃣ Start Visualization Dashboard
streamlit run twin_dashboard.py

5️⃣ Start Real-Time Inference
python test_serial_tf.py


🧩 Key Technical Features


Embedded vibration analytics


Statistical feature extraction (RMS/Kurtosis)


LSTM time-series classification


Low-latency edge inference architecture


Local Digital Twin implementation


Real-time telemetry visualization


Scalable, modular codebase


IoT-ready (MQTT/REST expandable)



🧑‍💻 Team Skyantra


Shashi Kumar C


Ronak Soni


Nainshi




---

If you want:

✔ a **GitHub project banner image**  
✔ repository tags  
✔ shields.io badges  
✔ a LICENSE file  
✔ CONTRIBUTING.md  
✔ a professional ASCII architecture diagram  

Just say **“add GitHub enhancements”**.











