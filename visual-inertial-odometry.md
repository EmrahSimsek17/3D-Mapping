# Visual-Inertial Odometry (VIO)

## Definition

Visual-Inertial Odometry combines image and IMU measurements for robust
motion estimation.

## Sensors

-   Camera
-   Accelerometer
-   Gyroscope

## Pipeline

Image + IMU → Synchronization → Feature Tracking → State Estimation →
Optimization

## Fusion Approaches

-   EKF-based
-   Optimization-based
-   Factor Graph

## Representative Systems

-   VINS-Mono
-   OKVIS
-   ORB-SLAM3
-   BASALT

## Metrics

-   ATE
-   RPE
-   Drift
-   Runtime

## Datasets

-   EuRoC MAV
-   TUM VI
-   ADVIO
-   Hilti

## Challenges

-   Sensor synchronization
-   Calibration
-   IMU bias
-   High-speed motion
