# Depth Estimation

> A concise tutorial on **Depth Estimation**, covering mathematical
> foundations, geometric and learning-based approaches, evaluation
> metrics, benchmark datasets, and current research directions.

------------------------------------------------------------------------

# Contents

1.  Introduction
2.  Definition
3.  Mathematical Foundations
4.  Depth Estimation Pipeline
5.  Depth Estimation Categories
6.  Classical Methods
7.  Deep Learning Methods
8.  Self-Supervised Learning
9.  Evaluation Metrics
10. Benchmark Datasets
11. Representative Models
12. Research Challenges
13. Future Directions
14. Resources

------------------------------------------------------------------------

# 1. Introduction

Depth Estimation predicts the distance between a camera and scene
points. It is a fundamental component of autonomous driving, robotics,
UAV navigation, augmented reality, and 3D reconstruction.

Typical applications include

-   Autonomous Driving
-   Mobile Robotics
-   UAV Navigation
-   3D Mapping
-   SLAM
-   Augmented Reality
-   Medical Imaging
-   Industrial Inspection

------------------------------------------------------------------------

# 2. Definition

Given an RGB image

``` math
I\in\mathbb{R}^{H\times W\times3}
```

the objective is to estimate a depth map

``` math
D\in\mathbb{R}^{H\times W}
```

where each pixel stores the distance from the camera.

Outputs may be

-   Relative Depth
-   Metric Depth
-   Dense Depth
-   Sparse Depth

------------------------------------------------------------------------

# 3. Mathematical Foundations

## Camera Projection

``` math
x=K[R|t]X
```

## Stereo Geometry

Depth is computed from disparity.

``` math
Z=\frac{fB}{d}
```

where

-   **Z** : depth
-   **f** : focal length
-   **B** : baseline
-   **d** : disparity

Greater disparity indicates a closer object.

------------------------------------------------------------------------

## Triangulation

A 3D point is reconstructed from multiple image observations.

``` math
X=\operatorname{triangulate}(x_1,x_2)
```

------------------------------------------------------------------------

# 4. Depth Estimation Pipeline

``` text
Input Image(s)
      │
Feature Extraction
      │
Depth Prediction
      │
Refinement
      │
Depth Map
```

Common stages

-   Image preprocessing
-   Feature extraction
-   Multi-scale fusion
-   Depth prediction
-   Edge refinement

------------------------------------------------------------------------

# 5. Depth Estimation Categories

## Monocular Depth Estimation

Uses a single RGB image.

Advantages

-   Low hardware cost
-   Suitable for embedded systems

Limitations

-   Scale ambiguity
-   Challenging metric depth recovery

------------------------------------------------------------------------

## Stereo Depth Estimation

Uses two synchronized cameras.

Advantages

-   Metric depth
-   High geometric accuracy

Limitations

-   Requires calibration
-   Sensitive to textureless regions

------------------------------------------------------------------------

## Multi-View Stereo (MVS)

Uses multiple overlapping images.

Advantages

-   Dense reconstruction
-   High-quality geometry

Applications

-   Photogrammetry
-   3D Mapping

------------------------------------------------------------------------

## RGB-D Depth

Uses dedicated depth sensors such as structured light or Time-of-Flight
cameras.

Representative sensors

-   Intel RealSense
-   Azure Kinect
-   Orbbec

------------------------------------------------------------------------

# 6. Classical Methods

Representative algorithms

-   Block Matching
-   Semi-Global Matching (SGM)
-   Graph Cuts
-   Dynamic Programming

Advantages

-   Geometrically interpretable
-   No training required

Limitations

-   Sensitive to lighting
-   Computationally demanding

------------------------------------------------------------------------

# 7. Deep Learning Methods

## Supervised Learning

Uses ground-truth depth maps.

Representative models

-   Eigen et al.
-   DORN
-   BTS
-   AdaBins

------------------------------------------------------------------------

## Transformer-based Models

Representative methods

-   ZoeDepth
-   Depth Anything
-   Metric3D

Advantages

-   Strong global context
-   Excellent generalization

------------------------------------------------------------------------

# 8. Self-Supervised Learning

Self-supervised approaches learn depth using image reconstruction
without dense depth labels.

Typical supervision

-   Photometric consistency
-   View synthesis
-   Pose estimation

Representative models

-   Monodepth2
-   PackNet-SfM
-   ManyDepth

Advantages

-   No ground-truth depth required
-   Large-scale training

Limitations

-   Dynamic objects
-   Occlusions
-   Illumination changes

------------------------------------------------------------------------

# 9. Evaluation Metrics

Absolute Relative Error

``` math
AbsRel=
\frac1N\sum\frac{|D-\hat D|}{D}
```

Squared Relative Error

``` math
SqRel=
\frac1N\sum\frac{(D-\hat D)^2}{D}
```

Root Mean Square Error

``` math
RMSE=
\sqrt{\frac1N\sum(D-\hat D)^2}
```

Log RMSE

``` math
RMSE_{log}
```

Threshold Accuracy

``` math
\delta<1.25
```

Higher values indicate better predictions.

------------------------------------------------------------------------

# 10. Benchmark Datasets

  Dataset         Domain       Sensor
  --------------- ------------ --------------
  KITTI Depth     Driving      Stereo
  NYUv2           Indoor       RGB-D
  ETH3D           Multi-view   Stereo
  ScanNet         Indoor       RGB-D
  TUM RGB-D       SLAM         RGB-D
  DDAD            Driving      Multi-sensor
  Virtual KITTI   Synthetic    Stereo

------------------------------------------------------------------------

# 11. Representative Models

  Model              Year Main Idea
  ---------------- ------ ----------------------------
  Eigen              2014 CNN depth estimation
  Monodepth          2017 Self-supervised stereo
  Monodepth2         2019 Monocular self-supervision
  BTS                2020 Local planar guidance
  AdaBins            2021 Adaptive depth bins
  ZoeDepth           2023 Zero-shot metric depth
  Depth Anything     2024 Foundation depth model
  Metric3D           2024 Metric monocular depth

------------------------------------------------------------------------

# 12. Research Challenges

-   Scale ambiguity
-   Thin structures
-   Reflective surfaces
-   Transparent objects
-   Dynamic scenes
-   Adverse weather
-   Long-range depth estimation
-   Real-time embedded inference

------------------------------------------------------------------------

# 13. Future Directions

Emerging research topics

-   Foundation Models
-   Metric Monocular Depth
-   Event Camera Depth
-   RGB-IMU Depth Estimation
-   Semantic-guided Depth
-   Gaussian Splatting
-   Neural Radiance Fields (NeRF)
-   Edge AI Depth Estimation

------------------------------------------------------------------------

# 14. Useful Resources

## Libraries

-   OpenCV
-   Open3D
-   PyTorch
-   Kornia
-   TensorRT

## Conferences

-   CVPR
-   ICCV
-   ECCV
-   3DV
-   ICRA

## Journals

-   IEEE TPAMI
-   IJCV
-   Pattern Recognition
-   Image and Vision Computing

## Suggested Learning Order

1.  Camera Geometry
2.  Stereo Vision
3.  Multi-View Geometry
4.  Visual Odometry
5.  Depth Estimation
6.  3D Mapping
7.  SLAM

------------------------------------------------------------------------

# Notes

Depth Estimation is one of the key building blocks of modern 3D
perception systems. In practical applications, it is commonly integrated
with Visual Odometry, Semantic Segmentation, and 3D Mapping to enable
accurate scene understanding and autonomous navigation.
