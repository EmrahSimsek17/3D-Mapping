# Depth Estimation

> A comprehensive tutorial on **Depth Estimation**, covering geometry, classical and deep learning approaches, evaluation metrics, benchmark datasets, representative models, and future research directions.

---

# Contents

1. Introduction
2. Definition
3. Mathematical Foundations
4. Depth Estimation Pipeline
5. Categories
6. Classical Methods
7. Deep Learning Methods
8. Self-Supervised Learning
9. Evaluation Metrics
10. Benchmark Datasets
11. Representative Models
12. Representative Papers
13. Research Challenges
14. Future Directions
15. Useful Resources

---

# 1. Introduction

Depth Estimation aims to recover the distance between the camera and every visible point in a scene. The output is usually a dense depth map where each pixel represents the estimated distance from the camera.

Applications include

- Autonomous Driving
- Mobile Robotics
- UAV Navigation
- 3D Mapping
- SLAM
- Augmented Reality
- Medical Imaging
- Industrial Inspection

---

# 2. Definition

Given an RGB image

```math
I\in\mathbb{R}^{H\times W\times3},
```

estimate a depth map

```math
D=f(I),
```

where

```math
D\in\mathbb{R}^{H\times W}.
```

Each pixel stores the estimated distance from the camera center to the corresponding scene point.

Output types

- Relative Depth
- Metric Depth
- Dense Depth
- Sparse Depth

---

# 3. Mathematical Foundations

## Camera Projection

```math
\lambda
\begin{bmatrix}
u\\
v\\
1
\end{bmatrix}
=
K
\begin{bmatrix}
R&t
\end{bmatrix}
X
```

where

- **K** : intrinsic matrix
- **R** : rotation matrix
- **t** : translation vector

## Stereo Geometry

Depth is inversely proportional to disparity.

```math
Z=\frac{fB}{d}
```

where

- **Z** : depth
- **f** : focal length
- **B** : stereo baseline
- **d** : disparity

Large disparity → Near object

Small disparity → Far object

## Triangulation

A 3D point is reconstructed from multiple observations.

```math
X=f(x_1,x_2)
```

where **f** denotes the triangulation function.

---

# 4. Depth Estimation Pipeline

```text
Input Image(s)
      │
Image Preprocessing
      │
Feature Extraction
      │
Multi-scale Feature Fusion
      │
Depth Prediction
      │
Depth Refinement
      │
Depth Map
```

---

# 5. Categories

## Monocular Depth Estimation

Advantages

- Single camera
- Low cost
- Passive sensing
- Lightweight
- Suitable for embedded AI

Limitations

- Scale ambiguity
- Metric depth is difficult
- Domain shift
- Long-range estimation is challenging

## Stereo Depth Estimation

Advantages

- Metric depth
- Accurate geometry
- Mature algorithms

Limitations

- Camera calibration required
- Sensitive to textureless regions
- Higher computational cost

## Multi-View Stereo (MVS)

Uses multiple overlapping images.

Typical pipeline

```text
Image Collection
      │
Camera Pose Estimation
      │
Sparse SfM
      │
Dense MVS
      │
Mesh Reconstruction
```

Applications

- Photogrammetry
- Digital Twins
- 3D Mapping

## RGB-D Depth Estimation

Representative sensors

- Intel RealSense
- Azure Kinect
- Orbbec
- OAK-D

Depth technologies

- Structured Light
- Time-of-Flight
- Active Stereo

---

# 6. Classical Methods

Representative algorithms

- Block Matching
- Semi-Global Matching (SGM)
- Graph Cuts
- Dynamic Programming

### Semi-Global Matching (SGM)

Advantages

- High accuracy
- Widely adopted
- Efficient implementation

Common implementation

- OpenCV StereoSGBM

---

# 7. Deep Learning Methods

### Supervised

Representative models

- Eigen et al.
- DORN
- BTS
- AdaBins
- NewCRFs

### Transformer-based

Representative models

- ZoeDepth
- Depth Anything
- Metric3D
- UniDepth
- Marigold

Advantages

- Strong global reasoning
- Excellent generalization

---

# 8. Self-Supervised Learning

Representative models

- Monodepth2
- PackNet-SfM
- ManyDepth

Typical objective

```math
L=L_{photo}+\lambda L_{smooth}
```

Common losses

- Photometric Loss
- Edge-aware Smoothness Loss
- Pose Consistency Loss

Advantages

- No dense labels
- Large-scale training

Limitations

- Dynamic objects
- Occlusions
- Illumination variation

---

# 9. Evaluation Metrics

## Absolute Relative Error

```math
AbsRel=
\frac{1}{N}
\sum
\frac{|D-\hat D|}{D}
```

## Squared Relative Error

```math
SqRel=
\frac{1}{N}
\sum
\frac{(D-\hat D)^2}{D}
```

## Root Mean Square Error

```math
RMSE=
\sqrt{
\frac1N
\sum
(D-\hat D)^2
}
```

## Threshold Accuracy

```math
\delta_i=
\max
\left(
\frac{D_i}{\hat D_i},
\frac{\hat D_i}{D_i}
\right)
```

Report

- δ < 1.25
- δ < 1.25²
- δ < 1.25³

Higher threshold accuracy is better.

---

# 10. Benchmark Datasets

| Dataset | Indoor | Outdoor | Sensor | Metric Depth |
|---|:---:|:---:|---|:---:|
| KITTI Depth | | ✓ | Stereo | ✓ |
| NYUv2 | ✓ | | RGB-D | ✓ |
| ScanNet | ✓ | | RGB-D | ✓ |
| ETH3D | ✓ | ✓ | Stereo | ✓ |
| DDAD | | ✓ | Multi-sensor | ✓ |
| TUM RGB-D | ✓ | | RGB-D | ✓ |
| Virtual KITTI | | ✓ | Synthetic | ✓ |

---

# 11. Representative Models

| Model | Year | Type | Supervision |
|---|---:|---|---|
| Eigen | 2014 | CNN | Supervised |
| Monodepth | 2017 | CNN | Self-supervised |
| Monodepth2 | 2019 | CNN | Self-supervised |
| BTS | 2020 | CNN | Supervised |
| AdaBins | 2021 | CNN | Supervised |
| ZoeDepth | 2023 | Transformer | Metric |
| Depth Anything | 2024 | Foundation Model | Pretrained |
| Metric3D | 2024 | Transformer | Metric |

---

# 12. Representative Papers

| Paper | Contribution |
|---|---|
| Eigen et al. (2014) | First CNN-based monocular depth estimation |
| Monodepth (2017) | Self-supervised stereo learning |
| Monodepth2 (2019) | Monocular self-supervised depth |
| AdaBins (2021) | Adaptive depth binning |
| ZoeDepth (2023) | Zero-shot metric depth |
| Depth Anything (2024) | Foundation model for depth estimation |

---

# 13. Research Challenges

- Scale ambiguity
- Thin structures
- Reflective surfaces
- Transparent objects
- Dynamic scenes
- Long-range estimation
- Domain adaptation
- Embedded real-time inference

---

# 14. Future Directions

- Foundation Models
- Vision Foundation Models
- Video Depth Estimation
- Event Camera Depth
- RGB-IMU Depth Estimation
- Semantic-guided Depth
- Gaussian Splatting
- Neural Radiance Fields (NeRF)
- Edge AI Depth Estimation
- Generalizable Metric Depth

---

# 15. Useful Resources

## Libraries

- OpenCV
- Open3D
- PyTorch
- Kornia
- TensorRT

## Conferences

- CVPR
- ICCV
- ECCV
- 3DV
- ICRA

## Journals

- IEEE TPAMI
- IJCV
- Pattern Recognition
- Image and Vision Computing

## Suggested Learning Order

1. Camera Geometry
2. Stereo Vision
3. Multi-View Geometry
4. Visual Odometry
5. Depth Estimation
6. 3D Mapping
7. SLAM

---

# Notes

Modern depth estimation systems increasingly combine geometric constraints, transformer architectures, self-supervised learning, and foundation models to achieve robust and generalizable depth prediction across diverse environments.
