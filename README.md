# Wearable Motor Behavior Monitoring for ASD via Fitbit Accelerometer

> A passive, wrist-worn data acquisition system for capturing 3-axis accelerometer signals in individuals with Autism Spectrum Disorder (ASD) during structured educational tasks.

[![Fitbit SDK](https://img.shields.io/badge/Fitbit%20SDK-5.0.2-00B0B9)](https://dev.fitbit.com/)
[![Platform](https://img.shields.io/badge/Device-Fitbit%20Versa%203-blue)]()
[![Domain](https://img.shields.io/badge/Domain-ASD%20Research-purple)]()
[![License](https://img.shields.io/badge/License-MIT-green)]()

---

## Research Team

| Role | Name | Affiliation |
|------|------|-------------|
| **Lead Researcher** | Md. Fazlay Rabby, B.Sc. in EEE | University of Liberal Arts Bangladesh (ULAB) |
| **Supervisor** | Abul Barkat Mollah Sayeed Ud Doulah, Ph.D. | Associate Professor, Dept. of EEE, Southeast University (SEU); Ph.D., The University of Alabama, USA |

---

## Overview

Individuals with Autism Spectrum Disorder frequently exhibit characteristic motor behaviors — repetitive movements, postural shifts, and hyperkinetic patterns — that correlate with attentional and cognitive states. This project deploys the **Fitbit Versa 3** as a continuous, passive IMU sensing platform to acquire 3-axis accelerometer data during educational sessions. The data feeds a signal processing pipeline aimed at identifying motor signatures associated with attentive and inattentive behavioral states, laying the groundwork for lightweight on-device classification via TinyML.

### Research Objectives

- Discriminate attentive from inattentive behavioral states using wrist-worn 3-axis accelerometer signals.
- Characterize motor signatures associated with repetitive movement and hyperactivity during structured tasks.
- Establish a feature engineering framework suitable for TinyML deployment on resource-constrained wearable hardware.

---

## System Architecture

```
┌──────────────────────────────────┐
│      Fitbit Versa 3 (Watch)      │
│  Continuous accelerometer        │
│  sampling; Binary Int16 storage  │
└───────────────┬──────────────────┘
                │  Fitbit File Transfer API
                ▼
┌──────────────────────────────────┐
│     Companion Smartphone App     │
│  Binary → CSV; HTTP POST         │
└───────────────┬──────────────────┘
                ▼
┌──────────────────────────────────┐
│       Android Server App         │
│  CSV storage on device           │
└───────────────┬──────────────────┘
                ▼
┌──────────────────────────────────┐
│    Python Analysis Pipeline      │
│  Preprocessing · EDA · Features  │
└──────────────────────────────────┘
```

**Components:**
- **`fitbit-app/`** — Fitbit OS watch app (JavaScript); handles accelerometer sampling and binary on-device storage.
- **`android-app/`** — Android companion server; manages Fitbit File Transfer API communication and CSV conversion.
- **`analysis/`** — Jupyter Notebook pipeline; data cleaning, descriptive statistics, and signal visualization.


---

## Data Collection

### Sensor Configuration

| Parameter | Value |
|-----------|-------|
| **Device** | Fitbit Versa 3 |
| **Sensor** | 3-axis MEMS Accelerometer |
| **Axes** | X — lateral, Y — vertical, Z — anteroposterior |
| **Scalar** | 500 (resolution: 0.002 m/s²) |
| **Storage Encoding** | Binary Int16 (4× efficiency over plain text) |
| **Output Format** | CSV — `Timestamp, X, Y, Z` |

### Sample Record

```csv
Timestamp,X,Y,Z
1332640128,-2.412,7.604,6.090
1332640128,0.038,6.742,7.296
1332640256,0.726,6.588,7.546
```

### Pilot Dataset Statistics

| Axis | Mean (m/s²) | Std Dev | Min | Max |
|------|-------------|---------|-----|-----|
| X | −0.11 | 2.45 | −14.59 | 8.12 |
| Y | 6.32 | 2.24 | −6.76 | 17.93 |
| Z | 7.12 | 2.49 | −18.14 | 15.67 |

*n = 1,080 accelerometer records.*

---

## Setup & Deployment

### Prerequisites

- **Node.js (v14+)** and Fitbit SDK CLI for watch app compilation.
- **Android Studio** to build and deploy the mobile data-bridge server.
- **Python 3.x** with `pandas`, `numpy`, and `matplotlib`.

### Installation

```bash
git clone https://github.com/fazlayofficial/fitbit-asd-accel-monitoring.git
cd fitbit-asd-accel-monitoring
npm install && npm run build

# Deploy to watch
npx fitbit
> connect device
> install
```

### Data Collection Workflow

1. Launch the **android-fitbit-fetcher** server on the paired smartphone.
2. Open **Accel Fetcher** on the Fitbit Versa 3 and press **START RECORDING**.
3. After the session, press **TRANSFER TO PHONE**.
4. In the server app, tap **GET DATA** and save the CSV.
5. Load into `analysis/fitbit_analysis.ipynb` for processing.

---

## Attribution & Acknowledgments

This pipeline builds upon the binary data transfer infrastructure of **[fitbit-accel-fetcher](https://github.com/gondwanasoft/fitbit-accel-fetcher)** by [gondwanasoft](https://github.com/gondwanasoft).

**Key modifications:**
- Adapted for ASD behavioral monitoring and motor signature analysis.
- Custom Python signal processing and analysis pipeline.
- Structured for academic reproducibility in Biomedical Signal Processing research.

---

## Ethics & Privacy

All data collection follows institutional research ethics protocols. No raw participant data is included in this repository. Only anonymized sample records are provided for reproducibility.

---


