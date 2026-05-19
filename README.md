# AI-Driven Predictive Analytics for 5G Private Industrial IoT Networks

This repository contains the data processing pipelines, machine learning models, and simulation scripts developed to secure and optimize private 5G network services within Industrial IoT (IIoT) frameworks.

The project leverages the CIC-IDS2017 dataset to evaluate how behavioral machine learning models can mitigate data leakage, detect malicious anomalies, and assist the 5G Network Data Analytics Function (NWDAF) in maintaining Service Level Agreements (SLAs) at the network edge.

Project Architecture
-------------------------------

The system is designed to integrate directly with a private 5G Core deployment via Multi-access Edge Computing (MEC), allowing localized intelligence near the industrial shop floor.

1. **IIoT Device Layer:** Smart sensors, programmable logic controllers (PLCs), and robotic actuators generating high-frequency industrial telemetry.
2. **Private 5G Transport Layer:** Network slicing architectures separating heavy data streams (eMBB) from ultra-reliable low-latency control traffic (URLLC).
3. **Edge Compute Layer (MEC):** Localized servers running the predictive models to execute traffic monitoring and performance forecasting without cloud dependency.

Repository Structure
-------------------------------

```text
prediction_model/
├── data/
│   ├── all_normal_iot.csv       # Filtered benign baseline traffic samples
│   ├── reduced_data_1.csv       # Sampled attack payloads for initial testing
│   └── Thursday-WorkingHours-Morning-WebAttacks.pcap_ISCX.csv # Raw CIC-IDS2017 subset
├── models/
│   ├── trained_anomaly_detector.pkl # Hardened Random Forest Classifier for intrusion detection
│   └── latency_regressor.pkl        # Random Forest Regressor for QoS forecasting
├── notebooks/
│   └── 05BoT-IoT_Test.ipynb     # Pipeline for data sanitization, feature analysis, and training
└── README.md
```

Methodology and Model Hardening
-------------------------------

### 1\. Data Leakage Prevention (Behavioral Hardening)

To ensure the machine learning models learn legitimate behavioral patterns rather than static environment variables, a strict feature-dropping process is enforced. All network identifiers—including Source/Destination IPs, MAC addresses, timestamps, and specific ports (e.g., Destination Port)—are removed before training. This forces the classifier to identify threats like Web Attacks (SQLi, XSS) and Brute Force purely through flow behaviors, such as packet length variance and inter-arrival times.

### 2\. Dual-Engine Execution

*   **Classification Engine:** A RandomForestClassifier trained on sanitized behavioral features to achieve highly precise network anomaly detection without relying on metadata.
    
*   **Regression Engine:** A RandomForestRegressor implemented to project Quality of Service (QoS) parameters, forecasting throughput and latency variations to trigger proactive slice optimization.
    

Installation and Environment Setup
----------------------------------

This project is optimized for deployment within local environments or cloud-hosted infrastructure (such as Google Colab) requiring Google Drive persistence.

### Prerequisites

*   Python 3.10+
    
*   Pandas
    
*   Scikit-Learn
    
*   Joblib
    

Academic and Technical Frameworks
---------------------------------

This implementation aligns with the architectural requirements of the following standards and research frameworks:

*   **3GPP Technical Specification TS 23.288:** Architecture enhancements for data analytics automation in the 5G System (NWDAF).
    
*   **CIC-IDS2017 Dataset Evaluation Framework:** Behavioral profiles for network intrusion detection analysis.
