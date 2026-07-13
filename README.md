# 3D Mapping

> A research-oriented repository covering camera-based **3D
> perception**, including **Visual Odometry (VO)**, **Visual-Inertial
> Odometry (VIO)**, **Depth Estimation**, and **3D Mapping**. This
> repository provides concise tutorials, mathematical foundations,
> benchmark datasets, representative methods, and useful research
> resources.

------------------------------------------------------------------------

## Research Scope

The repository focuses on four closely related research topics that form
the perception pipeline of modern autonomous systems.

``` text
Image Sequence
      │
      ▼
Visual Odometry (VO)
      │
      ▼
Visual-Inertial Odometry (VIO)
      │
      ▼
Depth Estimation
      │
      ▼
3D Mapping
```

### Main Topics

-   📷 Visual Odometry (VO)
-   📡 Visual-Inertial Odometry (VIO)
-   🌄 Depth Estimation
-   🗺️ 3D Mapping

------------------------------------------------------------------------

# Learning Roadmap

A recommended study order for newcomers:

1.  Camera Geometry
2.  Linear Algebra & Optimization
3.  Image Processing Fundamentals
4.  Feature Detection & Matching
5.  Multiple View Geometry
6.  Visual Odometry
7.  Visual-Inertial Odometry
8.  Depth Estimation
9.  3D Mapping
10. SLAM

------------------------------------------------------------------------

# Repository Structure

``` text
3D-Mapping/
│
├── README.md
├── definitions.md
├── visual-odometry.md
├── visual-inertial-odometry.md
├── depth-estimation.md
└── 3d-mapping.md
```

------------------------------------------------------------------------

# Repository Overview

## Definitions

Introduces the fundamental terminology used throughout the repository.

Topics include

-   Pose
-   Rotation
-   Translation
-   Camera Coordinates
-   Ego-motion
-   Scale
-   Point Cloud
-   Depth
-   Map
-   SLAM

------------------------------------------------------------------------

## Visual Odometry (VO)

Visual Odometry estimates the six-degree-of-freedom (6-DoF) camera
motion using only image sequences.

Main contents

-   Mathematical formulation
-   Motion estimation
-   Feature-based methods
-   Direct methods
-   Learning-based VO
-   Evaluation metrics
-   Benchmark datasets
-   State-of-the-art methods

------------------------------------------------------------------------

## Visual-Inertial Odometry (VIO)

Visual-Inertial Odometry combines image measurements with inertial data
from an IMU to estimate robust camera motion.

Main contents

-   IMU fundamentals
-   Sensor fusion
-   EKF
-   Factor Graph Optimization
-   Sliding Window Optimization
-   VINS-Mono
-   ORB-SLAM3
-   Evaluation metrics

------------------------------------------------------------------------

## Depth Estimation

Depth Estimation predicts the distance between the camera and scene
points.

Main contents

-   Monocular depth estimation
-   Stereo depth estimation
-   Multi-view stereo
-   Self-supervised learning
-   Metric depth estimation
-   Benchmark datasets

------------------------------------------------------------------------

## 3D Mapping

3D Mapping reconstructs a geometric representation of the observed
environment.

Main contents

-   Point Clouds
-   TSDF
-   Occupancy Maps
-   Octrees
-   Semantic Mapping
-   Neural Mapping
-   Gaussian Splatting
-   NeRF

------------------------------------------------------------------------

# Benchmark Datasets

  -----------------------------------------------------------------------
  Research Area                  Representative Datasets
  ------------------------------ ----------------------------------------
  Visual Odometry                KITTI Odometry, EuRoC MAV, TUM RGB-D

  Visual-Inertial Odometry       EuRoC MAV, TUM VI, ADVIO, Hilti

  Depth Estimation               KITTI Depth, NYUv2, ETH3D, ScanNet

  3D Mapping                     Replica, ScanNet, Matterport3D,
                                 KITTI-360
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# Evaluation Metrics

Common evaluation metrics include

-   Absolute Trajectory Error (ATE)
-   Relative Pose Error (RPE)
-   Translation Error
-   Rotation Error
-   RMSE
-   Absolute Relative Error
-   Scale Drift
-   Chamfer Distance
-   Completeness
-   Reconstruction Accuracy

------------------------------------------------------------------------

# Representative Methods

## Visual Odometry

-   ORB-SLAM
-   DSO
-   LSD-SLAM
-   DeepVO
-   DROID-SLAM

## Visual-Inertial Odometry

-   VINS-Mono
-   OKVIS
-   BASALT
-   ORB-SLAM3

## Depth Estimation

-   Monodepth2
-   ZoeDepth
-   Depth Anything
-   Metric3D

## 3D Mapping

-   KinectFusion
-   ElasticFusion
-   Voxblox
-   BundleFusion
-   Gaussian Splatting
-   NeRF

------------------------------------------------------------------------

# Applications

These techniques are widely used in

-   Autonomous Driving
-   UAV Navigation
-   Mobile Robotics
-   Augmented Reality
-   Virtual Reality
-   Digital Twins
-   Indoor Navigation
-   Inspection Robots
-   Smart Cities

------------------------------------------------------------------------

# Useful Resources

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
-   Robotics and Automation Letters (RA-L)
-   Image and Vision Computing
-   Pattern Recognition

## Open-Source Libraries

-   OpenCV
-   Open3D
-   COLMAP
-   GTSAM
-   Ceres Solver
-   Sophus
-   Pangolin
-   PyTorch

------------------------------------------------------------------------

# Repository Goals

-   Introduce the mathematical foundations of camera-based 3D
    perception.
-   Summarize representative methods and algorithms.
-   Present benchmark datasets and evaluation metrics.
-   Provide concise tutorials for each research topic.
-   Collect influential papers and open-source implementations.
-   Support students and researchers working on autonomous systems,
    robotics, and computer vision.
