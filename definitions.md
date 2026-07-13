# 3D Vision Glossary (Definitions)

> Fundamental terminology for **3D Mapping**, **Visual Odometry (VO)**, **Visual-Inertial Odometry (VIO)**, **Depth Estimation**, **Structure from Motion (SfM)** and **SLAM**.

---

# Contents

1. Coordinate Systems
2. Camera Model
3. Camera Motion
4. 3D Geometry
5. Mapping Concepts
6. SLAM Concepts
7. Optimization
8. Recommended Reading

---

# 1. Coordinate Systems

## World Coordinate System
A fixed global reference frame describing the environment.

## Camera Coordinate System
A local coordinate system attached to the camera.

## Image Coordinate System

```math
p=(u,v)
```

## Normalized Image Coordinates

```math
x_n=K^{-1}x
```

Used after removing intrinsic camera parameters.

## Homogeneous Coordinates

```math
X=
\begin{bmatrix}
x\\
y\\
z\\
1
\end{bmatrix}
```

Advantages

- Unified transformations
- Projective geometry
- Camera projection

---

# 2. Camera Model

## Camera
Projects a 3D scene onto a 2D image plane.

## Pinhole Camera Model

```math
\lambda x=
K
\begin{bmatrix}
R&t
\end{bmatrix}
X
```

## Intrinsic Parameters

- Focal length
- Principal point
- Pixel size
- Skew

```math
K=
\begin{bmatrix}
f_x&0&c_x\\
0&f_y&c_y\\
0&0&1
\end{bmatrix}
```

## Extrinsic Parameters

```math
T=
\begin{bmatrix}
R&t\\
0&1
\end{bmatrix}
```

## Camera Calibration

Estimation of intrinsic parameters and lens distortion.

## Lens Distortion

- Radial distortion
- Tangential distortion

## Field of View (FoV)

Defines the observable angular range.

## Baseline

```math
B=\|C_1-C_2\|
```

Distance between stereo cameras.

---

# 3. Camera Motion

## Pose

```math
T=
\begin{bmatrix}
R&t\\
0&1
\end{bmatrix}
```

Pose belongs to

```math
T\in SE(3)
```

## Translation

```math
t=
\begin{bmatrix}
t_x\\
t_y\\
t_z
\end{bmatrix}
```

## Rotation Matrix

```math
R\in SO(3)
```

```math
R^TR=I
```

```math
det(R)=1
```

## Euler Angles

- Roll
- Pitch
- Yaw

## Quaternion

Compact rotation representation without gimbal lock.

## Ego-motion

Motion of the observing camera.

## Scale

Metric conversion factor.

## Drift

Accumulated trajectory error.

## 6-DoF

- X,Y,Z translation
- Roll, Pitch, Yaw rotation

---

# 4. 3D Geometry

## Depth

```math
Z>0
```

## Disparity

```math
Z=\frac{fB}{d}
```

## Triangulation

```math
X=f(x_1,x_2)
```

## Epipolar Geometry

Relationship between two calibrated views.

## Essential Matrix

```math
x'^TEx=0
```

## Fundamental Matrix

```math
x'^TFx=0
```

## Homography

```math
x'=Hx
```

## Point Cloud

```math
P=\{(x_i,y_i,z_i)\}
```

Point attributes may include RGB, normals and semantic labels.

## Surface Normal

Perpendicular vector to a surface.

## Mesh

Polygon-based surface representation.

---

# 5. Mapping Concepts

## Sparse Mapping

Reconstructs only salient landmarks.

## Dense Mapping

Reconstructs most visible surfaces.

## Semantic Mapping

Combines geometry with semantic labels.

## Occupancy Grid

Free / Occupied / Unknown cells.

## Voxel

Volumetric equivalent of a pixel.

## Octree

Hierarchical spatial representation.

## TSDF

Truncated Signed Distance Function.

## ESDF

Euclidean Signed Distance Field.

## Gaussian Splatting

Scene representation using 3D Gaussians.

## Neural Radiance Fields (NeRF)

Continuous neural scene representation.

---

# 6. SLAM Concepts

## Visual Odometry (VO)

Camera motion estimation using images.

## Visual-Inertial Odometry (VIO)

Camera and IMU fusion.

## Structure from Motion (SfM)

Joint recovery of camera poses and sparse geometry.

## SLAM

Simultaneous Localization and Mapping.

## Dynamic SLAM

SLAM in dynamic environments.

## Keyframe

Frame selected for optimization.

## Keypoint

Representative image feature.

Examples

- ORB
- SIFT
- AKAZE

## Landmark

Persistent reconstructed 3D point.

## Loop Closure

Recognition of previously visited places.

## Relocalization

Recovery after tracking failure.

---

# 7. Optimization

## Bundle Adjustment

```math
\min \sum \|x-\hat{x}\|^2
```

Joint optimization of camera poses and landmarks.

## Pose Graph Optimization

Global optimization over camera poses.

## Factor Graph

Graph representation of estimation constraints.

## Robust Loss Functions

- Huber
- Cauchy
- Tukey

---

# Recommended Reading

- Multiple View Geometry in Computer Vision
- Computer Vision: Algorithms and Applications
- Probabilistic Robotics
- Visual SLAM: From Theory to Practice
