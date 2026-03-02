# 📡 ADHD Behavioral Monitoring via Fitbit Accelerometer

> **Wearable data acquisition system for studying attention and focus patterns in ADHD patients during educational tasks.**

[![Fitbit SDK](https://img.shields.io/badge/Fitbit%20SDK-5.0.2-00B0B9)](https://dev.fitbit.com/)
[![Platform](https://img.shields.io/badge/Device-Fitbit%20Versa%203-blue)]()
[![Research](https://img.shields.io/badge/Domain-ADHD%20Research-purple)]()

---

## 👨‍🔬 Research Team
* **Lead Researcher:** Md. Fazlay Rabby, B.Sc. in EEE, ULAB
* **Supervisor:** Abul Barkat Mollah Sayeed Ud Doulah, Ph.D. in Electrical Engineering (The University of Alabama, USA); Associate Professor, Dept. of EEE, Southeast University (SEU).

---

## 🧠 Research Overview
This project implements a wearable data acquisition pipeline using the **Fitbit Versa 3** smartwatch to continuously collect 3-axis accelerometer data from ADHD patients during educational activities. The goal is to identify motor behavior signatures—such as fidgeting, restlessness, or hyperkinetic movement—that correlate with attentional states during focused learning tasks.



### 🎯 Research Objectives
* Differentiate between attentive and inattentive states using wrist-worn 3-axis accelerometer data.
* Analyze movement signatures characteristic of hyperactivity during structured educational tasks.
* Develop a foundation for lightweight on-device ML (TinyML) to classify behavioral states from raw IMU data.

---

## ⚙️ System Architecture



The system consists of three modular components:
1.  **fitbit-app/**: The Fitbit OS watch app (JavaScript) responsible for raw accelerometer data sampling and internal storage management.
2.  **android-app/**: The companion Android server app that facilitates binary data transfer via the Fitbit File Transfer API and performs CSV conversion.
3.  **analysis/**: A Python-based analysis pipeline (Jupyter Notebook) featuring data cleaning, descriptive statistics, and signal visualization.

---

## 🔬 Data Collection Protocol

### Sensor Specifications
| Parameter | Value |
|-----------|-------|
| **Device** | Fitbit Versa 3 |
| **Sensor** | 3-axis MEMS Accelerometer |
| **Axes** | X (lateral), Y (vertical), Z (anteroposterior) |
| **Output Format** | CSV (Timestamp, X, Y, Z) |

---

## 🚀 Setup & Deployment

### Prerequisites
* **Node.js (v14+)** and **Fitbit SDK CLI** for watch app compilation.
* **Android Studio** to build and deploy the mobile data-bridge server.
* **Python 3.x** with Pandas, NumPy, and Matplotlib for signal processing.

---

## 📚 Attribution & Acknowledgments
This research pipeline utilizes the communication infrastructure provided by the **fitbit-accel-fetcher** open-source project by [gondwanasoft](https://github.com/gondwanasoft/fitbit-accel-fetcher).

**Key Research Modifications:**
* Project adapted for ADHD behavioral monitoring and hyperkinetic signature detection.
* Implementation of a custom Python-based signal processing and analysis workflow.
* Structured for academic reproducibility in Intelligent Systems and Biomedical Signal Processing research.