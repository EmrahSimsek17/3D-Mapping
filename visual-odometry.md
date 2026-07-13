# Visual Odometry (VO)

> A concise tutorial on **Visual Odometry (VO)** covering mathematical foundations, motion estimation, classical and learning-based methods, benchmark datasets, evaluation metrics, and current research directions.

---

## Contents

1. [Introduction](#1-introduction)
2. [Definition](#2-definition)
3. [Mathematical Foundations](#3-mathematical-foundations)
4. [Visual Odometry Pipeline](#4-visual-odometry-pipeline)
5. [VO Categories](#5-vo-categories)
6. [Motion Estimation Methods](#6-motion-estimation-methods)
7. [Optimization](#7-optimization)
8. [Deep Learning-Based VO](#8-deep-learning-based-vo)
9. [Evaluation Metrics](#9-evaluation-metrics)
10. [Benchmark Datasets](#10-benchmark-datasets)
11. [Representative Systems](#11-representative-systems)
12. [Research Challenges](#12-research-challenges)
13. [Future Directions](#13-future-directions)
14. [Useful Resources](#14-useful-resources)

---

# 1. Introduction

Visual Odometry estimates the motion of a camera from an ordered image sequence.

The term **odometry** refers to estimating the incremental motion of a moving platform. In Visual Odometry, this motion is inferred from visual observations rather than wheel encoders, GNSS, or other external positioning systems.

Typical application areas include:

- Autonomous driving
- UAV navigation
- Mobile robotics
- Augmented reality
- 3D mapping
- SLAM
- Inspection systems
- GPS-denied navigation

---

# 2. Definition

Given an image sequence

```math
\mathcal{I}=\{I_1,I_2,\ldots,I_N\},
```

Visual Odometry estimates the camera trajectory

```math
\mathcal{T}=\{T_1,T_2,\ldots,T_N\}.
```

Each camera pose can be represented by a rigid-body transformation

```math
T_t=
\begin{bmatrix}
R_t & t_t\\
0 & 1
\end{bmatrix},
```

where:

- \(R_t\in SO(3)\) is the camera rotation,
- \(t_t\in\mathbb{R}^3\) is the camera translation,
- \(T_t\in SE(3)\) is the homogeneous transformation matrix.

The relative motion between two consecutive frames is

```math
T_{t-1,t}=T_{t-1}^{-1}T_t.
```

For a monocular camera, translation is generally recovered only up to an unknown scale factor.

---

# 3. Mathematical Foundations

## 3.1 Camera Projection

A 3D point in world coordinates is written as

```math
X_w=
\begin{bmatrix}
X\\
Y\\
Z\\
1
\end{bmatrix}.
```

Its projection onto the image plane is

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
R & t
\end{bmatrix}
X_w,
```

where:

- \(K\) is the intrinsic camera matrix,
- \(R\) is the rotation matrix,
- \(t\) is the translation vector,
- \(\lambda\) is a projective scale factor,
- \((u,v)\) are pixel coordinates.

The intrinsic matrix is

```math
K=
\begin{bmatrix}
f_x & s & c_x\\
0 & f_y & c_y\\
0 & 0 & 1
\end{bmatrix}.
```

Here:

- \(f_x,f_y\) are focal lengths in pixel units,
- \(c_x,c_y\) are principal-point coordinates,
- \(s\) is the skew term.

---

## 3.2 Feature Correspondence

A visual feature observed in two frames creates a correspondence

```math
x_i \leftrightarrow x_i'.
```

These correspondences may be obtained through:

- Feature detection and descriptor matching
- Optical flow
- Learned correspondence networks
- Dense matching

Reliable correspondences are essential because incorrect matches directly degrade motion estimation.

---

## 3.3 Epipolar Constraint

For two calibrated camera views, corresponding normalized image points satisfy

```math
{x_i'}^{T} E x_i=0,
```

where \(E\) is the essential matrix.

The essential matrix is defined as

```math
E=[t]_{\times}R,
```

where \([t]_{\times}\) is the skew-symmetric matrix of the translation vector:

```math
[t]_{\times}=
\begin{bmatrix}
0 & -t_z & t_y\\
t_z & 0 & -t_x\\
-t_y & t_x & 0
\end{bmatrix}.
```

For uncalibrated pixel coordinates, the fundamental matrix is used:

```math
{x_i'}^{T} F x_i=0.
```

The relationship between the essential and fundamental matrices is

```math
F=K'^{-T}EK^{-1}.
```

---

## 3.4 Perspective-n-Point

If 3D scene points and their 2D image observations are known, camera pose can be estimated through the Perspective-n-Point problem.

```math
\hat{T}
=
\arg\min_T
\sum_{i=1}^{N}
\left\|
x_i-\pi(TX_i)
\right\|_2^2,
```

where:

- \(X_i\) is a 3D point,
- \(x_i\) is its observed image location,
- \(\pi(\cdot)\) is the camera projection function.

Common algorithms include:

- P3P
- EPnP
- Iterative PnP
- PnP with RANSAC

---

## 3.5 Triangulation

Triangulation reconstructs a 3D point from observations in multiple views.

Given projection matrices \(P_1\) and \(P_2\),

```math
x_1 \sim P_1X,
```

```math
x_2 \sim P_2X.
```

The 3D point estimate is obtained by minimizing reprojection error:

```math
\hat{X}
=
\arg\min_X
\sum_{j}
\left\|
x_j-\pi(P_jX)
\right\|_2^2.
```

---

## 3.6 Reprojection Error

Reprojection error measures the discrepancy between an observed feature and the projection of the estimated 3D point.

```math
e_i=
\left\|
x_i-\pi(TX_i)
\right\|_2.
```

The total reprojection objective is

```math
\mathcal{L}_{\mathrm{reproj}}
=
\sum_{i=1}^{N}
\rho
\left(
\left\|
x_i-\pi(TX_i)
\right\|_2^2
\right),
```

where \(\rho(\cdot)\) is often a robust loss function such as Huber or Cauchy loss.

---

# 4. Visual Odometry Pipeline

A typical Visual Odometry pipeline is:

```text
Image Sequence
      │
Camera Calibration
      │
Feature Detection or Dense Matching
      │
Feature Matching / Optical Flow
      │
Outlier Rejection
      │
Relative Motion Estimation
      │
Pose Refinement
      │
Trajectory Integration
```

Main stages:

1. Acquire calibrated image frames.
2. Detect or track visual correspondences.
3. Remove outliers using geometric consistency.
4. Estimate relative rotation and translation.
5. Refine pose with nonlinear optimization.
6. Accumulate relative transformations into a trajectory.

---

# 5. VO Categories

## 5.1 Monocular VO

Monocular VO uses a single camera.

### Advantages

- Low cost
- Low weight
- Simple hardware
- Passive sensing

### Limitations

- Scale ambiguity
- Sensitivity to initialization
- Weak robustness under pure rotation
- Difficulty in low-parallax motion

---

## 5.2 Stereo VO

Stereo VO uses two synchronized cameras with a known baseline.

Depth is related to disparity by

```math
Z=\frac{fB}{d}
```

where:

- \(Z\) is depth,
- \(f\) is focal length,
- \(B\) is the stereo baseline,
- \(d\) is disparity.

### Advantages

- Metric scale
- Better triangulation
- Improved robustness

### Limitations

- Requires stereo calibration
- Higher computational cost
- Limited depth accuracy at long range

---

## 5.3 RGB-D VO

RGB-D VO uses color images and direct depth measurements.

A pixel can be back-projected into 3D as

```math
X=
ZK^{-1}
\begin{bmatrix}
u\\
v\\
1
\end{bmatrix}.
```

### Advantages

- Direct metric depth
- Dense geometric information
- Strong indoor performance

### Limitations

- Restricted sensing range
- Sensitivity to reflective and transparent surfaces
- Outdoor performance limitations for some sensors

---

# 6. Motion Estimation Methods

## 6.1 Feature-Based Methods

Feature-based VO uses sparse keypoints and descriptors.

Typical feature detectors and descriptors include:

- FAST
- Harris
- SIFT
- SURF
- ORB
- AKAZE

A common pipeline is:

```text
Keypoint Detection
      │
Descriptor Extraction
      │
Feature Matching
      │
RANSAC
      │
Essential Matrix or PnP
      │
Pose Refinement
```

### Advantages

- Computationally efficient
- Robust to moderate illumination changes
- Easy integration with loop closure

### Limitations

- Weak performance in textureless scenes
- Feature distribution may be sparse or uneven

Representative systems:

- ORB-SLAM
- ORB-SLAM2
- ORB-SLAM3
- LIBVISO2

---

## 6.2 Direct Methods

Direct VO estimates motion by minimizing photometric error instead of matching descriptors.

The photometric objective may be written as

```math
\mathcal{L}_{\mathrm{photo}}
=
\sum_{p\in\Omega}
\rho
\left(
I_t(p)
-
I_{t+1}
\left(
\pi
\left(
T_{t,t+1}\pi^{-1}(p,D_t(p))
\right)
\right)
\right).
```

### Advantages

- Uses image intensity directly
- Can exploit more pixels
- Effective in low-feature environments

### Limitations

- Sensitive to illumination changes
- Sensitive to exposure variation
- Requires good initialization

Representative systems:

- DSO
- LSD-SLAM
- SVO

---

## 6.3 Semi-Direct and Hybrid Methods

Hybrid methods combine feature-based and direct components.

Typical strategies include:

- Feature-based initialization with direct refinement
- Sparse feature tracking with photometric optimization
- Learned correspondences with geometric pose estimation

These methods aim to balance robustness, speed, and accuracy.

---

## 6.4 Robust Estimation

RANSAC is frequently used to remove outliers.

Given candidate correspondences, RANSAC repeatedly:

1. Selects a minimal subset.
2. Estimates a geometric model.
3. Measures residuals.
4. Counts inliers.
5. Retains the best model.

A correspondence is often classified as an inlier when

```math
r_i<\tau
```

where \(r_i\) is the geometric residual and \(\tau\) is a threshold.

---

# 7. Optimization

## 7.1 Bundle Adjustment

Bundle Adjustment jointly optimizes camera poses and 3D landmarks.

```math
\min_{\{T_j\},\{X_i\}}
\sum_{i,j}
\rho
\left(
\left\|
x_{ij}
-
\pi(T_jX_i)
\right\|_2^2
\right).
```

### Variants

- Local Bundle Adjustment
- Sliding-Window Bundle Adjustment
- Global Bundle Adjustment

---

## 7.2 Pose Graph Optimization

A pose graph represents camera poses as nodes and relative transformations as edges.

The optimization objective is

```math
\min_{\{T_i\}}
\sum_{(i,j)\in\mathcal{E}}
\left\|
\mathrm{Log}
\left(
\hat{T}_{ij}^{-1}T_i^{-1}T_j
\right)
\right\|_{\Omega_{ij}}^2.
```

Pose graph optimization reduces accumulated drift and improves global trajectory consistency.

---

## 7.3 Loop Closure

Loop closure identifies previously visited locations.

Its main purposes are:

- Drift correction
- Global consistency
- Map reuse
- Long-term localization

Common place-recognition methods include:

- Bag of Visual Words
- NetVLAD
- Learned global descriptors

---

# 8. Deep Learning-Based VO

Learning-based VO replaces or augments classical components with neural networks.

## 8.1 End-to-End Regression

An end-to-end model predicts relative pose directly from consecutive frames:

```math
(\hat{R},\hat{t})
=
f_{\theta}(I_{t-1},I_t).
```

Representative systems:

- DeepVO
- VINet
- TartanVO

### Advantages

- Learns task-specific visual features
- Can model complex appearance variation

### Limitations

- Dataset dependence
- Generalization issues
- Metric scale inconsistency
- Reduced interpretability

---

## 8.2 Geometry-Aware Learning

Geometry-aware methods incorporate:

- Optical flow
- Depth
- Epipolar constraints
- Reprojection loss
- Pose consistency
- Cycle consistency

A combined objective may be written as

```math
\mathcal{L}
=
\lambda_p\mathcal{L}_{\mathrm{pose}}
+
\lambda_d\mathcal{L}_{\mathrm{depth}}
+
\lambda_f\mathcal{L}_{\mathrm{flow}}
+
\lambda_r\mathcal{L}_{\mathrm{reproj}}.
```

---

## 8.3 Deep Optimization Systems

Modern systems combine neural feature extraction with iterative geometric optimization.

Representative systems:

- DROID-SLAM
- DPVO

These methods preserve geometric structure while using learned components for correspondence and update estimation.

---

# 9. Evaluation Metrics

## 9.1 Absolute Trajectory Error

ATE measures global trajectory consistency.

After alignment, translational error at frame \(i\) is

```math
e_i=
\left\|
\mathrm{trans}
\left(
T_i^{-1}S\hat{T}_i
\right)
\right\|_2,
```

where \(S\) is an alignment transformation.

The root mean square ATE is

```math
ATE_{\mathrm{RMSE}}
=
\sqrt{
\frac{1}{N}
\sum_{i=1}^{N}
e_i^2
}.
```

---

## 9.2 Relative Pose Error

RPE measures local motion accuracy over a fixed interval \(\Delta\).

```math
E_i=
\left(
T_i^{-1}T_{i+\Delta}
\right)^{-1}
\left(
\hat{T}_i^{-1}\hat{T}_{i+\Delta}
\right).
```

Translational RPE is

```math
RPE_{\mathrm{trans}}
=
\sqrt{
\frac{1}{M}
\sum_{i=1}^{M}
\left\|
\mathrm{trans}(E_i)
\right\|_2^2
}.
```

---

## 9.3 KITTI Translation Error

KITTI reports average translation error as a percentage of traveled distance.

```math
t_{\mathrm{rel}}
=
\frac{1}{|\mathcal{S}|}
\sum_{s\in\mathcal{S}}
\frac{
\left\|
\mathrm{trans}(E_s)
\right\|_2
}{
l_s
}
\times 100.
```

---

## 9.4 KITTI Rotation Error

Rotation error is commonly reported in degrees per 100 meters.

```math
r_{\mathrm{rel}}
=
\frac{1}{|\mathcal{S}|}
\sum_{s\in\mathcal{S}}
\frac{
\theta(E_s)
}{
l_s
}.
```

---

## 9.5 Runtime Metrics

Runtime evaluation should report:

- Frames per second
- Per-frame latency
- Input resolution
- Hardware
- Numerical precision
- Preprocessing time
- Network inference time
- Optimization time
- Postprocessing time

Frames per second is

```math
FPS=
\frac{N_{\mathrm{frames}}}{T_{\mathrm{seconds}}}.
```

---

# 10. Benchmark Datasets

| Dataset | Sensor Configuration | Environment | Main Use |
|---|---|---|---|
| KITTI Odometry | Stereo cameras | Outdoor driving | VO and SLAM |
| EuRoC MAV | Stereo cameras + IMU | Indoor UAV | VO, VIO and SLAM |
| TUM RGB-D | RGB-D camera | Indoor | RGB-D VO and SLAM |
| KITTI-360 | Stereo cameras and additional sensors | Urban driving | Mapping and localization |
| Málaga Urban | Monocular/stereo cameras | Urban driving | VO |
| Oxford RobotCar | Multiple cameras and sensors | Long-term urban driving | Localization and robustness |
| TartanAir | Synthetic RGB, depth and pose | Diverse simulated scenes | Learning-based VO |
| ADVIO | Smartphone camera + IMU | Indoor and outdoor | VO and VIO |

---

# 11. Representative Systems

## Classical Systems

| Method | Category | Main Characteristic |
|---|---|---|
| ORB-SLAM | Feature-based | ORB features and loop closure |
| ORB-SLAM2 | Feature-based | Monocular, stereo and RGB-D |
| ORB-SLAM3 | Feature-based | Visual, visual-inertial and multi-map support |
| LSD-SLAM | Direct | Large-scale semi-dense monocular SLAM |
| DSO | Direct | Sparse direct photometric optimization |
| SVO | Semi-direct | Fast sparse alignment |

## Learning-Based Systems

| Method | Category | Main Characteristic |
|---|---|---|
| DeepVO | End-to-end | CNN and recurrent pose regression |
| GeoNet | Self-supervised | Joint depth, pose and flow learning |
| TartanVO | Learning-based | Generalization-oriented pose estimation |
| DROID-SLAM | Deep optimization | Recurrent dense bundle adjustment |
| DPVO | Deep optimization | Efficient patch-based VO |

---

# 12. Research Challenges

Major research challenges include:

- Monocular scale ambiguity
- Dynamic objects
- Motion blur
- Low-texture environments
- Illumination variation
- Repetitive patterns
- Rolling-shutter distortion
- Long-term drift
- Cross-domain generalization
- Real-time embedded deployment
- Reliable uncertainty estimation
- Robustness under high-speed motion

---

# 13. Future Directions

Current and emerging directions include:

- Semantic Visual Odometry
- Dynamic-scene VO
- Event-camera VO
- Foundation-model features
- Visual-language localization
- Neural scene representations
- Gaussian Splatting-assisted localization
- Self-supervised VO
- Uncertainty-aware pose estimation
- Edge AI and low-power VO
- Selective and event-driven visual processing

---

# 14. Useful Resources

## Libraries

- [OpenCV](https://opencv.org/)
- [Open3D](https://www.open3d.org/)
- [Ceres Solver](http://ceres-solver.org/)
- [GTSAM](https://gtsam.org/)
- [Sophus](https://github.com/strasdat/Sophus)
- [Pangolin](https://github.com/stevenlovegrove/Pangolin)
- [Eigen](https://eigen.tuxfamily.org/)
- [PyTorch](https://pytorch.org/)

## Suggested Learning Order

1. Linear algebra
2. Camera geometry
3. Feature detection and matching
4. Epipolar geometry
5. Essential and fundamental matrices
6. PnP
7. Triangulation
8. Bundle Adjustment
9. Visual Odometry
10. Visual-Inertial Odometry
11. SLAM
12. 3D Mapping

---

# Notes

Visual Odometry is a core component of autonomous perception systems. Classical methods remain strong because of their geometric interpretability, while modern systems increasingly combine learned correspondence estimation, dense optimization, semantic information, and uncertainty modeling.
