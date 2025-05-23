# 📡 Integrated Aircraft Navigation and Fault Detection System

**Course:** ACS6124 – Multisensor and Decision Systems  
**University:** The University of Sheffield  
**Lecturer:** Dr. Yuanbo Nie  
**Author:** Samanta Suprio Sujoy  
**Assessment:** Part I – Multisensor Systems (50% of module marks)  
**Year:** 2022–2023

---

## 📘 Project Overview

This project develops an integrated aircraft navigation system using measurements from:
- Inertial Measurement Unit (IMU),
- GPS with attitude sensors,
- Air-data system (airspeed, angle of attack, slip).

It utilizes **Iterated Extended Kalman Filters (IEKF)** to estimate aircraft states and incorporates real-time **sensor fault detection (CUSUM)** and **bias correction**.

---

## 🧪 Tasks Overview

### 🔹 Task 1: Kalman Filter Design
Design a navigation model with 12 states:
- Position: xE, yE, zE
- Velocity: u, v, w
- Attitude: φ, θ, ψ
- Wind components: VwxE, VwyE, VwzE

#### 🔸 Task 1.1
Derive Jacobian matrices for:
- F = ∂f/∂x (state transition),
- G = ∂g/∂ω (process noise),
- H = ∂h/∂x (measurement).

#### 🔸 Task 1.2
Run IEKF on dataset `dataTask1.mat`:
- Plot state estimates for all 12 states.
- Comment on innovation stability and convergence.

---

### 🔹 Task 2: Sensor Bias Correction
Using `dataTask2.mat`, investigate the effect of **constant IMU sensor bias**.

#### 🔸 Task 2.1
- Re-run Task 1 without modifying the model.
- Compare estimated trajectories with those from Task 1.
- Identify variables most affected by bias.

#### 🔸 Task 2.2
- Augment state vector to include 6 IMU biases.
- Estimate them as states (bias terms = constant).
- Plot and validate bias estimation through convergence.

---

### 🔹 Task 3: Fault Detection and Mitigation

#### 🔸 Task 3.1
Use `dataTask3_1.mat` with unmodeled sensor faults:
- Plot innovation history.
- Identify time of fault occurrences using abnormal innovation behavior.

#### 🔸 Task 3.2
- Model biases as random walk processes with added process noise.
- Redesign Kalman filter and plot updated innovation history.
- Compare results to Task 3.1.

#### 🔸 Task 3.3
- Use CUSUM algorithm to detect faults in inputs: Ax, Ay, Az, p, q, r.
- Use `dataTask2.mat` as nominal reference, and `dataTask3_1.mat` for detection.
- Justify method, display detection results, and plot alarms.

#### 🔸 Task 3.4
- Detect **frozen angle of attack (α)** sensor in `dataTask3_2.mat`.
- Assume fault source is known.
- Without increasing state vector, adapt innovation-based FDD.
- Plot detection and mitigation evidence.

---

### 🔹 Task 4: Performance Evaluation (Code Submission)
Submit Kalman filter implementation with:
- Robust estimation
- Effective fault detection

Your submission will be assessed on:
- **Estimation WMSE** (Weighted Mean Squared Error)
- **Fault Detection Timing Accuracy**
- **Bias/Fault Signal Estimation Accuracy**

Refer to `SubmissionTemplate.m` and `testYourScript.m` for script requirements.

---

## 📂 Repository Structure

```
Multisensor-Systems-Project/
│
├── data/
│   ├── dataTask1.mat
│   ├── dataTask2.mat
│   ├── dataTask3_1.mat
│   └── dataTask3_2.mat
│
├── figures/
│   ├── figure_task1_attitude_estimation.png
│   ├── figure_task2_bias_comparison.png
│   ├── figure_task3_cusum_ax.png
│
├── docs/
│   └── ACS6124_Assignment.pdf
│
├── code/
│   ├── IEKF_main.m
│   ├── Jacobian_derivation.m
│   ├── run_task1.m
│   ├── run_task2_bias_model.m
│   ├── run_task3_cusum.m
│   └── SubmissionTemplate.m
│
└── README.md
```

---

## 🎓 Learning Outcomes

- Develop and apply nonlinear Kalman Filters for high-dimensional sensor fusion.
- Model and estimate systematic sensor biases.
- Design fault detection schemes using innovation and statistical thresholds (CUSUM).
- Apply MATLAB for engineering-grade algorithm deployment.

---

## 🧠 Skills Demonstrated

- ✅ Nonlinear state estimation (EKF, IEKF)
- ✅ Sensor bias and fault modeling
- ✅ MATLAB programming and simulation
- ✅ Fault-tolerant systems
- ✅ Aircraft kinematics and dynamics modeling
- ✅ Data visualization and innovation analysis

---

## 📚 Key Concept Definitions

### 🔄 Iterated Extended Kalman Filter (IEKF)
The **IEKF** is an enhancement of the Extended Kalman Filter (EKF) used for nonlinear systems. In each time step, IEKF:
1. Linearizes the system around the current state estimate.
2. Applies multiple correction iterations (typically 2–3) within the measurement update step.
3. Improves convergence and stability for highly nonlinear systems like aircraft dynamics.

---

### 📈 Kalman Filter Innovation
**Innovation** is the difference between the actual sensor measurement and the predicted measurement from the filter:
```
Innovation = z_measured - z_predicted
```
It reflects how much new information is in the current measurement. Large innovations may indicate a fault or anomaly.

---

### ⚠️ CUSUM (Cumulative Sum) Fault Detection
**CUSUM** is a sequential analysis technique used to detect abrupt changes in a signal. It accumulates deviations of sensor values or residuals from their expected behavior:
- A **two-sided CUSUM** tracks both positive and negative deviations.
- Once the cumulative sum exceeds a defined threshold, a **fault alarm** is triggered.

In this project, CUSUM is applied to Kalman filter innovations to detect faults in sensors like IMU accelerometers and gyros.

---

### 🔄 Sensor Bias Modeling
Sensor biases are slow-changing or constant errors in measurements. For IMUs, typical biases are:
- Constant offset in accelerometer or gyroscope readings.
- Modeled as either:
  - **Constant Bias**: Treated as fixed but unknown (estimated via filter).
  - **Random Walk**: Treated as slow-varying and modeled with small process noise.

In this project, biases are estimated by **augmenting the Kalman Filter state vector**.

---

### 🛫 Aircraft Kinematic Model
Aircraft position and attitude evolve over time based on:
- Body-frame velocities (u, v, w)
- Orientation (Euler angles: φ, θ, ψ)
- Rotational rates (p, q, r)
- Acceleration (Ax, Ay, Az)

The system model uses simplified flat-Earth equations to relate these quantities and is nonlinear due to trigonometric dependencies on attitude angles.

---

## 💼 How to Use This Project in Your Portfolio

On LinkedIn or your resume, list this project as:

> **Aircraft Navigation and Fault Detection System** – Designed a multisensor estimator using Iterated Kalman Filtering, estimated IMU biases in-flight, and implemented CUSUM-based fault detection for aircraft sensor anomalies.

Include the GitHub link and optionally attach PDF report with visual results.

---

⭐️ *If this project interests you or helps your learning, consider starring the repository!* ⭐️

---
---

## 🖼️ Figures

### 📊 Task 1: Navigation State Estimation
![Attitude Estimation](figures/figure_task1_attitude_estimation.png)
*Estimated roll, pitch, and yaw using IEKF.*

### 📊 Task 2: Sensor Bias Analysis
![Bias Comparison](figures/figure_task2_bias_comparison.png)
*Comparison of trajectories from biased vs. unbiased IMU input.*

![Bias Estimation](figures/figure_task2_bias_estimation.png)
*Convergence of estimated IMU bias terms.*

### 📊 Task 3: Fault Detection and Mitigation
![CUSUM Detection for Ax](figures/figure_task3_cusum_ax.png)
*CUSUM test result showing fault detection in Ax.*

![Innovation History](figures/figure_task3_innovation_history.png)
*Innovation signal over time highlighting fault responses.*

![Angle of Attack Fault](figures/figure_task3_aoa_fault.png)
*Detection and mitigation of AoA sensor freeze (Task 3.4).*
