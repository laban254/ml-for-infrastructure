# ML for Infrastructure

[![CI Status](https://github.com/laban254/ml-for-infrastructure/actions/workflows/ci.yml/badge.svg)](https://github.com/laban254/ml-for-infrastructure/actions/workflows/ci.yml)
[![Python Version](https://img.shields.io/badge/Python-3.10+-blue)](https://www.python.org/)
[![Theme](https://img.shields.io/badge/Context-Observability--First-blueviolet)](#-infrastructure-intelligence)
[![License](https://img.shields.io/badge/License-MIT-green)](#-philosophy--license)
[![Open in Colab](https://img.shields.io/badge/Open%20in-Colab-orange?logo=googlecolab)](https://colab.research.google.com/github/laban254/ml-for-infrastructure)

---

## Documentation
- [Getting Started](docs/GETTING-STARTED.md) - 5-minute quickstart guide
- [Setup & Installation](docs/SETUP.md) - Detailed installation instructions
- [Architecture](docs/ARCHITECTURE.md) - Project structure and design
- [Contributing](docs/CONTRIBUTING.md) - Contribution guidelines
- [Development](docs/DEVELOPMENT.md) - Developer guide for agents

---

## What this is
**ML for Infrastructure** provides Machine Learning workflows tailored for modern observability. Every module leverages system telemetry — CPU, memory, network, and logs — to solve real production failure scenarios.

---

## Capabilities

### 📡 Intelligent Monitoring (`03_machine_learning/` & `05_sre_applications/`)
Solving the "hard" problems in production using ML:
*   **Anomaly Detection:** Native **Isolation Forest** implementation to detect DDoS attacks and database locks without manual thresholds.
*   **Log Clustering:** Automatic grouping of millions of unstructured logs into "Healthy", "Slow", and "Failing" behaviors.
*   **Predictive scaling:** Forecasting application latency based on concurrent connection spikes using Regression models.

### ⚙️ MLOps & Production Pipelines
ML is only useful if it runs reliably in a CI/CD environment.
*   **Leakage-Free Pipelines:** Preprocessing + models bundled for consistent deployment.
*   **Operational Metrics:** Prioritizing **Precision (Alert Fatigue)** and **Recall (Missed Outages)** over simple binary accuracy.
*   **Automated Tuning:** Self-optimizing hyperparameters for API timeout prediction via **GridSearchCV**.

### 📊 Observability Visuals (`02_visualization/`)
Professional-grade reporting designed for post-mortems and incident analysis.
*   **RCA Dashboards:** Automated charts with alert thresholds and OOM event markers.
*   **Drift Detection:** Using statistical tests (KS-test) to detect when infrastructure performance shifts permanently.

---

## 🔧 Automation & Tooling
Built with a DevOps mindset, the hub includes CLI tools for speed and reproducibility.

### 📥 Data Ingestion (`fetch_data.py`)
Centralized data fetching with built-in **Integrity Verification (MD5 Hashes)**.
```bash
python fetch_data.py --quick     # Ingest small samples for fast testing
python fetch_data.py --full      # Ingest full datasets for training
python fetch_data.py --verify    # Verify data integrity against known hashes
```

### 🎛️ Execution Modes (`notebook_toggle.py`)
Toggle between fast iteration and complete training directly from the CLI or within Jupyter.
*   **Quick Mode:** Uses 10% of data and 1/10th of iterations for instant feedback.
*   **Full Mode:** Leverages all CPU cores (`n_jobs=-1`) and full datasets for production-grade models.

---

## 🚀 Run it live — zero install

Every notebook carries **Open in Colab** and **Open in Binder** badges at the top. Click one and the notebook runs in a free cloud runtime — no setup, nothing to install. The flagship scenarios ship with **interactive sliders** (drag the Isolation Forest sensitivity, the alert threshold, or the drift magnitude and watch the result update) plus **"Try it yourself" exercises** with reveal-on-click solutions.

> 📌 Notebooks are committed **with their outputs already rendered**, so you can read the full story — charts, metrics, insights — straight from GitHub without running anything.

Best notebooks to start with:

| Scenario | Notebook | You'll learn |
| --- | --- | --- |
| 🚨 Anomaly detection | [`prometheus_anomaly.ipynb`](05_sre_applications/anomaly_detection/prometheus_anomaly.ipynb) | Isolation Forest vs Z-score on CPU telemetry — interactive |
| 📉 Data drift | [`data_drift.ipynb`](05_sre_applications/model_monitoring/data_drift.ipynb) | KS-test drift detection — interactive |
| 🧮 NumPy foundations | [`numpy.ipynb`](01_foundations/numpy/numpy.ipynb) | Vectorized metric analysis — interactive |
| 🩺 Server health | [`classification.ipynb`](03_machine_learning/scikit-learn/supervised-learning-algorithms/classification.ipynb) | Multi-class triage with feature importance |

---

## ⚡ Quick Start (local install)

1.  **Clone & Install**
    ```bash
    git clone https://github.com/laban254/ml-for-infrastructure.git
    cd ml-for-infrastructure
    pip install -r requirements.txt            # light core stack — runs most notebooks
    pip install -r requirements-deep.txt       # optional: keras, pytorch, pyspark, mlflow
    ```

2.  **Ingest Sample Data**
    ```bash
    python fetch_data.py --quick
    ```

3.  **Run a Scenario**
    Open `05_sre_applications/anomaly_detection/prometheus_anomaly.ipynb` to see the Isolation Forest in action — then drag the sensitivity slider.

---

## ⚖️ License
We prioritize **Precision** (avoiding Alert Fatigue) ensuring that when a model fires, it's worth an engineer's attention.

*Distributed under the MIT license.*
