# 📡 Integrated Aircraft Navigation and Fault Detection System

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
- Plot state estimates for all 12 states.
- Comment on innovation stability and convergence.

---

### 🔹 Task 2: Sensor Bias Correction
Investigate the effect of **constant IMU sensor bias**.

#### 🔸 Task 2.1
- Compare estimated trajectories with those from Task 1.
- Identify variables most affected by bias.

#### 🔸 Task 2.2
- Augment state vector to include 6 IMU biases.
- Estimate them as states (bias terms = constant).
- Plot and validate bias estimation through convergence.

---

### 🔹 Task 3: Fault Detection and Mitigation

#### 🔸 Task 3.1
- Identify time of fault occurrences using abnormal innovation behavior.
- Plot innovation history.

#### 🔸 Task 3.2
- Model biases as random walk processes with added process noise.
- Redesign Kalman filter and plot updated innovation history.
- Compare results to Task 3.1.

#### 🔸 Task 3.3
- Use CUSUM algorithm to detect faults in inputs: Ax, Ay, Az, p, q, r.

#### 🔸 Task 3.4
- Detect **frozen angle of attack (α)** sensor.
- Assume fault source is known.
- Without increasing state vector, adapt innovation-based FDD.

---

### 🔹 Task 4: Performance Evaluation (Code Submission)
Submit Kalman filter implementation with:
- Robust estimation
- Effective fault detection

---

## 📂 Repository Structure

```
Integrated-GPS-IMU-Air-data-navigation-system-using-EKF/
│
├── figures/
│   ├── figure_task1_attitude_estimation.png
│   ├── figure_task2_bias_comparison.png
│   ├── figure_task3_cusum_ax.png
│
├── docs/
│   └── ACS6124_Assignment.pdf
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

⭐️ *If this project interests you or helps your learning, consider starring the repository!* ⭐️

---
---

## 🖼️ Figures

### 📊 Task 1: Navigation State Estimation
![Body-frame velocities](figures/uvw_KF.png)

![Orientation](figures/psi_KF.png)

![Rotational rates](figures/v_wxe_KF.png)

![Acceleration](figures/xyz_KF.png)

*Estimated roll, pitch, and yaw using IEKF.*

### 📊 Task 2: Sensor Bias Analysis
![Body-frame velocities Bias](figures/uvw_sensor_bias.png)

![Orientation Bias](figures/theta_sensor_bias.png)

![Wind Component in z Direction Bias](figures/VwzE_sensor_bias.png)
*Comparison of trajectories from biased vs. unbiased IMU input.*

![Rotational rates Bias Estimation](figures/b_pqr_rectified.png)

![Acceleration Bias Estimation](figures/b_xyz_rectified.png)

*Convergence of estimated IMU bias terms.*

### 📊 Task 3: Fault Detection and Mitigation

![Fault Detection for Body-frame velocities](figures/UVW_fault.png)

![Fault Detection for Orientation](figures/phi_theta_psi_fault.png)

![Fault Detection for Rotational rates](figures/Vwxe_fault.png)

![Fault Detection for Acceleration](figures/xyz_fault.png)

![Fault Correction for Body-frame velocities](figures/uvw_fault_correction.png)

![Fault Correction for Orientation](figures/phi_fault_correction.png)

![Fault Correction for Rotational rates](figures/vw_fault_correction.png)

![Fault Correction for Acceleration](figures/xyz_fault_correction.png)

![CUSUM Detection for Ax](figures/a_x.png)
*CUSUM test result showing fault detection in Ax.*

![CUSUM Detection for Ay](figures/a_y.png)
*CUSUM test result showing fault detection in Ay.*

![CUSUM Detection for Az](figures/a_z.png)
*CUSUM test result showing fault detection in Az.*

![CUSUM Detection for P](figures/bp.png)
*CUSUM test result showing fault detection in P.*

![CUSUM Detection for Q](figures/bq.png)
*CUSUM test result showing fault detection in Q.*

![CUSUM Detection for R](figures/br.png)
*CUSUM test result showing fault detection in R.*

![Innovation History](figures/innov_history.png)
*Innovation signal over time, highlighting fault responses.*

![Angle of Attack Fault](figures/aoa.png)
*Detection and mitigation of AoA sensor freeze (Task 3.4).*
