
AAI-530 - Final Project
# SentinelMesh Edge: IoT Intrusion Detection System

This repository contains the machine learning pipeline and theoretical system architecture for **SentinelMesh Edge**, an IoT-based intrusion detection system developed for the AAI-530 (Artificial Intelligence and the Internet of Things) final project.

## Project Overview
The rapid proliferation of IoT devices has expanded the attack surface for malicious actors. SentinelMesh Edge proposes a defense-in-depth, edge-computing architecture that minimizes cloud latency by performing real-time machine learning inference directly on the local network. 

This project utilizes a two-tier machine learning approach:
1. **Reactive Classification (1D-CNN):** A deep learning model that performs binary classification on incoming network flows to detect active attacks.
2. **Proactive Forecasting (LSTM):** A time-series prediction model that establishes a baseline of normal network traffic rates to provide early-warning anomaly detection before an attack fully materializes.

## Dataset
The models are trained and validated on a balanced 240,000-record subset of the **CIC-IoT-2023** dataset, published by the Canadian Institute for Cybersecurity. 
* The dataset encompasses network flow telemetry from 105 real IoT device types.
* It includes 34 specific attack categories (DDoS, DoS, Reconnaissance, etc.) and one Benign class.

## Repository Contents
* `test_cnn.ipynb`: The primary Jupyter Notebook containing the complete end-to-end pipeline. This includes Exploratory Data Analysis (EDA), data preprocessing (StandardScaler/MinMaxScaler), the 1D-CNN model architecture and evaluation, and the LSTM time-series forecasting model.
* `SentinelMesh_Final_Subset.csv`: The balanced dataset used for model training and validation.
* `SentinelMesh_diagram.png`: The theoretical infrastructure diagram detailing the Device Layer, Edge Processing Layer, and Cloud Storage Layer.

## Model Performance
* **1D-CNN Classifier:** Achieved **98.81% validation accuracy** with 99% precision and 98% recall on attack traffic. Inference latency is <5 ms per flow.
* **LSTM Rate Predictor:** Successfully established a flat prediction baseline for normal packets-per-second (`Rate`), enabling anomaly alerts when live traffic exceeds the 2-sigma threshold.

## Dashboard
The Tableau Public dashboard visualizes model outputs and system status across four panels:
[SentinelMesh Edge — IoT Intrusion Detection Dashboard](PASTE_YOUR_PUBLIC_SHARE_LINK_HERE)

## How to Run
1. Clone this repository
2. Install dependencies: `pip install tensorflow==2.10 pandas numpy scikit-learn matplotlib seaborn`
3. Place `SentinelMesh_Final_Subset.csv` in the same directory as the notebook
4. Open `test_cnn.ipynb` and run all cells in order
> **Note:** GPU recommended. CNN training takes ~7 minutes.

## Technical Stack & Requirements
* **Language:** Python 3.10+
* **Framework:** TensorFlow 2.10.0 / Keras
* **Libraries:** Pandas, NumPy, Scikit-Learn, Matplotlib, Seaborn
* **Theoretical Protocols:** MQTT v3.1.1 (Telemetry), HTTPS REST API (Cloud Archival)
