# Definitions

> This document introduces the fundamental terminology used in
> camera-based **3D Mapping**, **Visual Odometry (VO)**,
> **Visual-Inertial Odometry (VIO)**, **Depth Estimation**, and
> **SLAM**.

------------------------------------------------------------------------

# Contents

1.  Coordinate Systems
2.  Camera Model
3.  Camera Motion
4.  Depth & Geometry
5.  Mapping Concepts
6.  SLAM Terminology

------------------------------------------------------------------------

# 1. Coordinate Systems

## World Coordinate System

A fixed global reference frame describing the environment.

------------------------------------------------------------------------

## Camera Coordinate System

A local coordinate system attached to the camera.

The camera center is the origin.

------------------------------------------------------------------------

## Image Coordinate System

The 2D coordinate system used to represent pixels.

``` math
p=(u,v)
```

------------------------------------------------------------------------

## Homogeneous Coordinates

Homogeneous coordinates simplify geometric transformations.

``` math
X=[x,y,z,1]^T
```

------------------------------------------------------------------------

# 2. Camera Model

## Pinhole Camera Model

The most widely used mathematical camera model.

Projection equation

``` math
x=K[R|t]X
```

where

-   **K** : intrinsic matrix
-   **R** : rotation matrix
-   **t** : translation vector

------------------------------------------------------------------------

## Intrinsic Parameters

Describe the internal properties of a camera.

Typical parameters

-   Focal length
-   Principal point
-   Pixel size
-   Skew

Intrinsic matrix

``` math
K=
\begin{bmatrix}
f_x&0&c_x\\
0&f_y&c_y\\
0&0&1
\end{bmatrix}
```

------------------------------------------------------------------------

## Extrinsic Parameters

Describe the camera pose relative to the world.

``` math
T=[R|t]
```

------------------------------------------------------------------------

# 3. Camera Motion

## Pose

Pose defines the camera position and orientation.

``` math
Pose=(R,t)
```

------------------------------------------------------------------------

## Rotation Matrix

Represents camera orientation.

Properties

-   Orthogonal
-   Determinant = 1

``` math
R^TR=I
```

------------------------------------------------------------------------

## Translation

Translation represents camera displacement.

``` math
t=[t_x,t_y,t_z]^T
```

------------------------------------------------------------------------

## Ego-motion

The motion of the camera itself, independent of moving objects.

------------------------------------------------------------------------

## Scale

Scale converts relative motion into metric distance.

Monocular systems cannot recover metric scale without additional
information.

------------------------------------------------------------------------

## Six Degrees of Freedom (6-DoF)

A camera pose consists of

-   Translation (x,y,z)
-   Rotation (roll,pitch,yaw)

------------------------------------------------------------------------

# 4. Depth & Geometry

## Depth

Depth is the distance between a scene point and the camera.

``` math
Z>0
```

------------------------------------------------------------------------

## Disparity

In stereo vision,

``` math
Z=\frac{fB}{d}
```

where

-   f : focal length
-   B : baseline
-   d : disparity

------------------------------------------------------------------------

## Baseline

The distance between two cameras in a stereo system.

------------------------------------------------------------------------

## Point Cloud

A collection of 3D points representing scene geometry.

``` math
P=\{(x_i,y_i,z_i)\}
```

------------------------------------------------------------------------

## Sparse Reconstruction

Only salient feature points are reconstructed.

------------------------------------------------------------------------

## Dense Reconstruction

Depth is estimated for most image pixels.

------------------------------------------------------------------------

# 5. Mapping Concepts

## Map

A geometric representation of an environment.

Common map types

-   Point Cloud
-   Mesh
-   Occupancy Grid
-   TSDF
-   Octree

------------------------------------------------------------------------

## Semantic Map

A map containing both geometry and semantic labels.

------------------------------------------------------------------------

## TSDF

Truncated Signed Distance Function.

Frequently used for dense volumetric mapping.

------------------------------------------------------------------------

## Occupancy Grid

Represents free and occupied space using discrete cells.

------------------------------------------------------------------------

## Loop Closure

Recognizing a previously visited location to reduce accumulated drift.

------------------------------------------------------------------------

## Bundle Adjustment

Joint optimization of camera poses and 3D points.

Objective

``` math
\min\sum ||x-\hat x||^2
```

------------------------------------------------------------------------

# 6. SLAM Terminology

## Visual Odometry (VO)

Estimates camera motion using image sequences.

------------------------------------------------------------------------

## Visual-Inertial Odometry (VIO)

Combines image and IMU measurements for robust motion estimation.

------------------------------------------------------------------------

## Depth Estimation

Predicts scene depth from one or more images.

------------------------------------------------------------------------

## Structure from Motion (SfM)

Recovers both camera motion and sparse scene geometry from multiple
images.

------------------------------------------------------------------------

## Simultaneous Localization and Mapping (SLAM)

Simultaneously estimates camera pose while constructing a map.

------------------------------------------------------------------------

## Dynamic SLAM

SLAM systems capable of handling moving objects.

------------------------------------------------------------------------

## Global Optimization

Reduces accumulated trajectory drift by optimizing all poses jointly.

------------------------------------------------------------------------

# Recommended Reading

-   Multiple View Geometry in Computer Vision
-   Computer Vision: Algorithms and Applications
-   Visual SLAM: From Theory to Practice
-   Probabilistic Robotics

------------------------------------------------------------------------

# Related Documents

-   Visual Odometry
-   Visual-Inertial Odometry
-   Depth Estimation
-   3D Mapping
