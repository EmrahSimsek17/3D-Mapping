# Visual-Inertial Odometry (VIO)

> A concise tutorial on **Visual-Inertial Odometry (VIO)** covering
> sensor fusion, mathematical foundations, estimation methods, benchmark
> datasets, evaluation metrics, and representative systems.

------------------------------------------------------------------------

# Contents

1.  Introduction
2.  Definition
3.  Mathematical Foundations
4.  VIO Pipeline
5.  Sensor Fusion
6.  Estimation Methods
7.  Optimization
8.  Evaluation Metrics
9.  Benchmark Datasets
10. Representative Systems
11. Research Challenges
12. Future Directions
13. Resources

------------------------------------------------------------------------

# 1. Introduction

Visual-Inertial Odometry estimates the six-degree-of-freedom (6-DoF)
motion of a moving platform by combining **camera** and **Inertial
Measurement Unit (IMU)** observations.

Compared with Visual Odometry, VIO is generally more robust during rapid
motion, temporary visual degradation, and low-texture environments.

Applications include

-   UAV Navigation
-   Autonomous Driving
-   Mobile Robotics
-   AR/VR
-   Handheld Devices
-   Inspection Robots

------------------------------------------------------------------------

# 2. Definition

Given synchronized image and IMU measurements

``` math
I=\{I_1,\cdots,I_n\}
```

``` math
U=\{a_t,\omega_t\}
```

estimate the camera trajectory

``` math
T=\{R_t,t_t\}
```

where

-   **R** : rotation
-   **t** : translation
-   **a** : accelerometer
-   **ω** : gyroscope

------------------------------------------------------------------------

# 3. Mathematical Foundations

## State Vector

``` math
x=[R,p,v,b_g,b_a]
```

where

-   R : orientation
-   p : position
-   v : velocity
-   b_g : gyroscope bias
-   b_a : accelerometer bias

------------------------------------------------------------------------

## Motion Model

``` math
x_k=f(x_{k-1},u_k)
```

using IMU integration.

------------------------------------------------------------------------

## Camera Projection

``` math
x=K[R|t]X
```

------------------------------------------------------------------------

## IMU Measurements

Accelerometer

``` math
a_m=a+b_a+n_a
```

Gyroscope

``` math
\omega_m=\omega+b_g+n_g
```

where

-   b : sensor bias
-   n : measurement noise

------------------------------------------------------------------------

# 4. VIO Pipeline

``` text
Images + IMU
      │
Time Synchronization
      │
Feature Tracking
      │
IMU Preintegration
      │
State Estimation
      │
Optimization
      │
Trajectory
```

Typical modules

-   Camera calibration
-   IMU calibration
-   Feature extraction
-   Feature tracking
-   Sensor fusion
-   Pose optimization

------------------------------------------------------------------------

# 5. Sensor Fusion

## Loosely Coupled

Camera and IMU are processed independently before fusion.

Advantages

-   Simpler implementation

Limitations

-   Lower accuracy

------------------------------------------------------------------------

## Tightly Coupled

Visual and inertial measurements are jointly optimized.

Advantages

-   Higher robustness
-   Better accuracy
-   Preferred in modern systems

------------------------------------------------------------------------

# 6. Estimation Methods

## Extended Kalman Filter (EKF)

Recursive probabilistic estimation.

Prediction

``` math
x_k^-=f(x_{k-1})
```

Correction

``` math
x_k=x_k^-+K(z-Hx_k^-)
```

Advantages

-   Real-time
-   Low computational cost

------------------------------------------------------------------------

## Sliding Window Optimization

Optimizes only recent states.

Advantages

-   Accurate
-   Real-time

Used by

-   VINS-Mono
-   BASALT

------------------------------------------------------------------------

## Factor Graph Optimization

Represents measurements as graph constraints.

Common solvers

-   GTSAM
-   Ceres Solver

Advantages

-   High accuracy
-   Flexible optimization

------------------------------------------------------------------------

# 7. IMU Preintegration

IMU samples between two frames are summarized into a compact constraint.

Benefits

-   Reduced optimization cost
-   High-frequency IMU utilization

Widely adopted in modern VIO frameworks.

------------------------------------------------------------------------

# 8. Evaluation Metrics

Trajectory metrics

-   Absolute Trajectory Error (ATE)
-   Relative Pose Error (RPE)

Other metrics

-   Translation Drift
-   Rotation Drift
-   Runtime
-   Tracking Success
-   CPU/GPU Usage

------------------------------------------------------------------------

# 9. Benchmark Datasets

  Dataset      Sensors              Environment
  ------------ -------------------- ----------------
  EuRoC MAV    Stereo + IMU         Indoor
  TUM VI       Stereo + IMU         Indoor
  ADVIO        Phone Camera + IMU   Indoor/Outdoor
  Hilti SLAM   Multi-sensor         Construction
  KITTI        Stereo               Driving
  NTU VIRAL    Multi-sensor         Large-scale

------------------------------------------------------------------------

# 10. Representative Systems

Classical

-   MSCKF
-   ROVIO
-   OKVIS

Optimization-based

-   VINS-Mono
-   VINS-Fusion
-   BASALT
-   ORB-SLAM3

Learning-based

-   DeepVIO
-   VINet

------------------------------------------------------------------------

# 11. Research Challenges

-   Sensor synchronization
-   IMU bias estimation
-   Scale consistency
-   Fast camera motion
-   Dynamic environments
-   Low-texture scenes
-   Rolling shutter
-   Real-time embedded deployment

------------------------------------------------------------------------

# 12. Future Directions

Emerging topics

-   Learning-based sensor fusion
-   Event Camera + IMU
-   Visual-Language Localization
-   Neural Scene Representations
-   Foundation Models
-   Edge AI VIO
-   Semantic VIO
-   Multi-camera VIO

------------------------------------------------------------------------

# 13. Useful Resources

## Libraries

-   GTSAM
-   Ceres Solver
-   Sophus
-   OpenCV
-   Eigen
-   Pangolin
-   ROS

## Conferences

-   CVPR
-   ICCV
-   ICRA
-   IROS
-   RSS

## Journals

-   IEEE TPAMI
-   IJCV
-   RA-L
-   Image and Vision Computing

## Suggested Learning Order

1.  Camera Geometry
2.  IMU Fundamentals
3.  Visual Odometry
4.  Sensor Fusion
5.  Kalman Filter
6.  Factor Graph Optimization
7.  Visual-Inertial Odometry
8.  SLAM

------------------------------------------------------------------------

# Notes

Modern VIO systems combine robust visual tracking with high-frequency
inertial sensing to provide accurate, low-drift motion estimation.
Optimization-based and tightly coupled approaches currently dominate
state-of-the-art research due to their superior accuracy and robustness.
