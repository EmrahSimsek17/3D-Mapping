# Visual Odometry (VO)

> A concise tutorial on **Visual Odometry (VO)** covering mathematical
> foundations, motion estimation, classical and learning-based methods,
> benchmark datasets, evaluation metrics, and current research
> directions.

------------------------------------------------------------------------

# Contents

1.  Introduction
2.  Definition
3.  Mathematical Foundations
4.  Visual Odometry Pipeline
5.  VO Categories
6.  Motion Estimation Methods
7.  Optimization
8.  Deep Learning-based VO
9.  Evaluation Metrics
10. Benchmark Datasets
11. Representative Systems
12. Research Challenges
13. Future Directions
14. Resources

------------------------------------------------------------------------

# 1. Introduction

Visual Odometry (VO) estimates the **6-DoF** motion of a camera using
image sequences. Unlike GPS-based localization, VO relies entirely on
visual information, making it suitable for autonomous vehicles, UAVs,
robots, and AR/VR systems operating in GPS-denied environments.

Typical applications include

-   Autonomous Driving
-   UAV Navigation
-   Mobile Robotics
-   Augmented Reality
-   3D Mapping
-   SLAM

------------------------------------------------------------------------

# 2. Definition

Given an image sequence

``` math
I=\{I_1,I_2,\cdots,I_n\}
```

estimate the camera trajectory

``` math
T=\{R_t,t_t\}
```

where

-   **R** : rotation
-   **t** : translation

For monocular cameras, motion is estimated only up to an unknown scale
unless additional information is available.

------------------------------------------------------------------------

# 3. Mathematical Foundations

## Camera Projection

``` math
x=K[R|t]X
```

where

-   **K** : intrinsic matrix
-   **R** : rotation matrix
-   **t** : translation vector

------------------------------------------------------------------------

## Feature Correspondence

Matching feature points between consecutive frames

``` math
p_i \leftrightarrow p_i'
```

provides geometric constraints for motion estimation.

------------------------------------------------------------------------

## Essential Matrix

For calibrated cameras

``` math
x'^TEx=0
```

The Essential Matrix encodes relative rotation and translation.

------------------------------------------------------------------------

## Perspective-n-Point (PnP)

Estimate camera pose from 2D--3D correspondences

``` math
T=\operatorname{PnP}(X,x)
```

------------------------------------------------------------------------

## Triangulation

Recover a 3D point from multiple observations

``` math
X=\operatorname{triangulate}(x_1,x_2)
```

------------------------------------------------------------------------

# 4. Visual Odometry Pipeline

``` text
Image Sequence
      │
Camera Calibration
      │
Feature Detection
      │
Feature Matching / Tracking
      │
Motion Estimation
      │
Pose Refinement
      │
Trajectory
```

Typical stages

-   Image preprocessing
-   Feature extraction
-   Correspondence estimation
-   Motion estimation
-   Local optimization
-   Trajectory estimation

------------------------------------------------------------------------

# 5. VO Categories

## Monocular VO

Uses a single RGB camera.

Advantages

-   Low cost
-   Lightweight
-   Passive sensing

Limitations

-   Scale ambiguity

------------------------------------------------------------------------

## Stereo VO

Uses synchronized stereo cameras.

Advantages

-   Metric scale
-   Improved robustness

Limitations

-   Calibration required
-   Higher computational cost

------------------------------------------------------------------------

## RGB-D VO

Uses RGB images together with depth measurements.

Representative sensors

-   Intel RealSense
-   Azure Kinect

Advantages

-   Dense geometric information
-   Accurate scale estimation

------------------------------------------------------------------------

# 6. Motion Estimation Methods

## Feature-based Methods

Estimate motion from sparse feature correspondences.

Representative detectors

-   SIFT
-   SURF
-   ORB
-   FAST
-   AKAZE

Representative systems

-   ORB-SLAM
-   LIBVISO

Advantages

-   Robust
-   Computationally efficient

------------------------------------------------------------------------

## Direct Methods

Estimate motion directly from pixel intensities.

Representative systems

-   DSO
-   LSD-SLAM
-   SVO

Advantages

-   Uses all image information
-   Better in low-feature scenes

Limitations

-   Sensitive to illumination changes

------------------------------------------------------------------------

## Hybrid Methods

Combine feature-based and direct estimation.

Goal

Improve robustness while maintaining efficiency.

------------------------------------------------------------------------

# 7. Optimization

## Bundle Adjustment

Joint optimization of camera poses and 3D points.

``` math
\min \sum ||x-\hat{x}||^2
```

------------------------------------------------------------------------

## Pose Graph Optimization

Reduces accumulated drift by jointly optimizing camera poses.

------------------------------------------------------------------------

## Loop Closure

Recognizes previously visited locations and improves global consistency.

------------------------------------------------------------------------

# 8. Deep Learning-based VO

Representative architectures

-   DeepVO
-   GeoNet
-   TartanVO
-   DROID-SLAM
-   DPVO

Common inputs

-   RGB images
-   Optical Flow
-   Depth
-   Semantic Segmentation

Advantages

-   Learns robust visual representations
-   Better adaptation to challenging environments

Limitations

-   Requires large datasets
-   Generalization remains challenging

------------------------------------------------------------------------

# 9. Evaluation Metrics

Trajectory metrics

-   Absolute Trajectory Error (ATE)
-   Relative Pose Error (RPE)

Translation error

``` math
e_t=\|t-\hat t\|
```

Rotation error

Measured in degrees or radians per unit distance.

Other metrics

-   Scale Drift
-   Runtime
-   FPS
-   Memory Usage

------------------------------------------------------------------------

# 10. Benchmark Datasets

  Dataset           Sensor         Main Usage
  ----------------- -------------- ------------------------
  KITTI Odometry    Stereo         Outdoor VO
  EuRoC MAV         Stereo + IMU   Indoor UAV
  TUM RGB-D         RGB-D          Indoor VO
  KITTI-360         Stereo         Large-scale mapping
  Malaga            Monocular      Urban driving
  Oxford RobotCar   Multi-camera   Long-term localization

------------------------------------------------------------------------

# 11. Representative Systems

Classical

-   ORB-SLAM
-   ORB-SLAM2
-   ORB-SLAM3
-   DSO
-   LSD-SLAM
-   SVO

Learning-based

-   DeepVO
-   GeoNet
-   TartanVO
-   DROID-SLAM
-   DPVO

------------------------------------------------------------------------

# 12. Research Challenges

-   Scale ambiguity
-   Dynamic objects
-   Motion blur
-   Low-texture environments
-   Illumination changes
-   Rolling shutter
-   Long-term drift
-   Real-time embedded deployment

------------------------------------------------------------------------

# 13. Future Directions

Emerging topics

-   Learning-based VO
-   Semantic Visual Odometry
-   Event Camera VO
-   Neural Scene Representations
-   Gaussian Splatting
-   Foundation Models
-   Visual-Language Localization
-   Edge AI Visual Odometry

------------------------------------------------------------------------

# 14. Useful Resources

## Libraries

-   OpenCV
-   Open3D
-   Sophus
-   Ceres Solver
-   GTSAM
-   Pangolin
-   Eigen
-   PyTorch

## Conferences

-   CVPR
-   ICCV
-   ECCV
-   ICRA
-   IROS
-   RSS

## Journals

-   IEEE TPAMI
-   IJCV
-   RA-L
-   Pattern Recognition
-   Image and Vision Computing

## Suggested Learning Order

1.  Camera Geometry
2.  Feature Detection & Matching
3.  Epipolar Geometry
4.  PnP & Triangulation
5.  Bundle Adjustment
6.  Visual Odometry
7.  Visual-Inertial Odometry
8.  SLAM
9.  3D Mapping

------------------------------------------------------------------------

# Notes

Visual Odometry is one of the core components of modern autonomous
perception systems. It provides reliable camera motion estimation and
forms the basis of SLAM, 3D Mapping, and autonomous navigation. Current
research increasingly combines geometric methods with deep learning,
semantics, and neural scene representations to improve robustness in
dynamic and challenging environments.
