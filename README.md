# Integrated-GPS-IMU-Air-data-navigation-system-using-EKF

<h1 align="center">📡 Multisensor Navigation System with Kalman Filter, Bias Correction, and Fault Detection</h1>

<p align="center">
  <img src="figures/attitude_estimation.png" alt="Attitude Estimation" width="600"/>
</p>

<p align="center">
  <i>A comprehensive coursework project on advanced sensor fusion and fault diagnosis in autonomous navigation systems.</i>
</p>

---

## 🎯 Project Overview

This project demonstrates the integration of GPS, IMU, and air-data sensors into a unified navigation system using an **Iterated Extended Kalman Filter (IEKF)**. It is part of my coursework for the **Multisensor and Decision Systems** module at the University of Sheffield. The project is divided into three tasks:

- ✅ Integrated state estimation (position, velocity, attitude)
- 🧭 Online bias correction for IMU sensors
- 🚨 Fault detection using the Cumulative Sum (CUSUM) method

---

## 🧠 Key Concepts

- **Kalman Filtering:** Nonlinear IEKF to estimate 12 aircraft states
- **Bias Compensation:** Augmented state vector to estimate sensor offsets
- **Fault Detection:** Statistical CUSUM test to identify sensor failures

---

## 🗂️ Repository Structure

```
Multisensor-Systems-Report/
├── docs/
│   └── Multisensor_Systems_Report.pdf     # Full report document
│
├── figures/
│   ├── attitude_estimation.png            # Task 1
│   ├── pitch_bias_comparison.png          # Task 2
│   └── fault_detection_ax.png             # Task 3
│
└── README.md                              # This file
```

---

## 🔬 Task Breakdown

### 🚀 Task 1: Navigation State Estimation

An IEKF was implemented to estimate position, velocity, and attitude. The results show convergence of innovations and alignment with measured values.

<p align="center">
  <img src="figures/attitude_estimation.png" alt="Attitude Estimation" width="500"/>
</p>

### ⚙️ Task 2: Sensor Bias Identification and Removal

Biases in the IMU readings caused systematic errors in state estimation. Augmenting the state vector with bias terms corrected these errors.

<p align="center">
  <img src="figures/pitch_bias_comparison.png" alt="Pitch Bias Comparison" width="500"/>
</p>

### 🚧 Task 3: Fault Detection with CUSUM

CUSUM test reliably identified abrupt shifts in sensor data and mitigated their effect by adjusting filter confidence.

<p align="center">
  <img src="figures/fault_detection_ax.png" alt="Fault Detection Ax" width="500"/>
</p>

---

