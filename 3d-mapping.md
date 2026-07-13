# 3D Mapping

> A concise tutorial covering the fundamentals of **3D Mapping**,
> including map representations, reconstruction pipelines, dense and
> sparse mapping, semantic mapping, evaluation metrics, benchmark
> datasets, and current research directions.

------------------------------------------------------------------------

# Contents

1.  Introduction
2.  Definition
3.  Mapping Pipeline
4.  Mathematical Foundations
5.  Map Representations
6.  Reconstruction Methods
7.  Semantic 3D Mapping
8.  Optimization
9.  Evaluation Metrics
10. Benchmark Datasets
11. Representative Systems
12. Research Challenges
13. Future Directions
14. Resources

------------------------------------------------------------------------

# 1. Introduction

3D Mapping aims to reconstruct a consistent three-dimensional
representation of an environment from sensor observations.

Unlike Visual Odometry, which estimates only camera motion, 3D Mapping
additionally reconstructs the surrounding scene.

Typical applications include

-   Autonomous Driving
-   UAV Navigation
-   Mobile Robotics
-   Digital Twins
-   Smart Cities
-   Mixed Reality
-   Industrial Inspection
-   Indoor Navigation

------------------------------------------------------------------------

# 2. Definition

Given camera observations

``` math
I=\{I_1,I_2,\cdots,I_n\}
```

and corresponding camera poses

``` math
T=\{T_1,T_2,\cdots,T_n\}
```

the objective is to estimate a map

``` math
M=f(I,T)
```

where **M** may represent geometry, semantics, or both.

Outputs commonly include

-   Sparse Point Cloud
-   Dense Point Cloud
-   Mesh
-   Occupancy Grid
-   TSDF Volume
-   Neural Scene Representation

------------------------------------------------------------------------

# 3. Mapping Pipeline

``` text
Images
   │
Visual Odometry / VIO
   │
Depth Estimation
   │
3D Point Generation
   │
Map Fusion
   │
Optimization
   │
Final Map
```

Typical stages

-   Pose estimation
-   Depth estimation
-   Point triangulation
-   Map fusion
-   Loop closure
-   Global optimization

------------------------------------------------------------------------

# 4. Mathematical Foundations

## Camera Projection

``` math
x=K[R|t]X
```

where

-   K : intrinsic matrix
-   R : rotation
-   t : translation

------------------------------------------------------------------------

## Triangulation

A 3D point is reconstructed from multiple observations.

```math
X = \mathrm{Triangulate}(x_1,x_2)
```

------------------------------------------------------------------------

## Point Cloud

A point cloud consists of

``` math
P=\{(x_i,y_i,z_i)\}
```

Each point may additionally contain

-   RGB color
-   Surface normal
-   Semantic label
-   Confidence score

------------------------------------------------------------------------

# 5. Map Representations

## Sparse Map

Stores only salient feature points.

Advantages

-   Memory efficient
-   Fast optimization

Limitations

-   Limited scene detail

------------------------------------------------------------------------

## Dense Map

Reconstructs most visible surfaces.

Advantages

-   Rich geometry
-   Suitable for navigation

Limitations

-   High computational cost

------------------------------------------------------------------------

## Mesh

Represents surfaces using connected triangles.

Applications

-   Visualization
-   Simulation
-   Digital twins

------------------------------------------------------------------------

## Occupancy Grid

Divides the environment into discrete cells.

Each cell is classified as

-   Occupied
-   Free
-   Unknown

------------------------------------------------------------------------

## TSDF

The Truncated Signed Distance Function stores the signed distance to the
nearest surface.

Widely used in dense RGB-D mapping systems.

------------------------------------------------------------------------

## Neural Scene Representation

Recent methods represent scenes using neural networks.

Representative approaches

-   NeRF
-   Gaussian Splatting
-   Neural Sparse Voxel Fields

------------------------------------------------------------------------

# 6. Reconstruction Methods

## Structure from Motion (SfM)

Recovers sparse geometry and camera poses from multiple images.

Representative software

-   COLMAP
-   OpenMVG

------------------------------------------------------------------------

## Multi-View Stereo (MVS)

Generates dense geometry after camera poses are known.

Representative systems

-   COLMAP MVS
-   OpenMVS

------------------------------------------------------------------------

## RGB-D Mapping

Uses depth cameras for dense mapping.

Representative systems

-   KinectFusion
-   ElasticFusion

------------------------------------------------------------------------

## Monocular Mapping

Uses only RGB images.

Advantages

-   Low hardware cost

Limitations

-   Scale ambiguity
-   Depth estimation required

------------------------------------------------------------------------

# 7. Semantic 3D Mapping

Definition

Semantic 3D Mapping combines geometric reconstruction with semantic
understanding.

Typical pipeline

RGB Image

↓

Semantic Segmentation

↓

Depth Estimation

↓

Pose Estimation

↓

Semantic Map Fusion

Applications

-   Autonomous robots
-   Scene understanding
-   Object-level navigation

------------------------------------------------------------------------

# 8. Optimization

## Bundle Adjustment

Jointly optimizes camera poses and 3D points.

``` math
\min\sum ||x-\hat x||^2
```

------------------------------------------------------------------------

## Loop Closure

Detects previously visited locations to reduce accumulated drift.

Benefits

-   Improved global consistency
-   Reduced trajectory error

------------------------------------------------------------------------

## Pose Graph Optimization

Optimizes all camera poses simultaneously.

Common libraries

-   GTSAM
-   Ceres Solver
-   g2o

------------------------------------------------------------------------

# 9. Evaluation Metrics

Trajectory Metrics

-   Absolute Trajectory Error (ATE)
-   Relative Pose Error (RPE)

Geometry Metrics

-   Chamfer Distance
-   RMSE
-   Accuracy
-   Completeness

Map Quality

-   Surface Coverage
-   Reconstruction Density
-   Memory Usage
-   Runtime

------------------------------------------------------------------------

# 10. Benchmark Datasets

  Dataset        Sensor       Main Usage
  -------------- ------------ -----------------------
  KITTI-360      RGB          Outdoor Mapping
  ScanNet        RGB-D        Indoor Mapping
  Matterport3D   RGB-D        Indoor Reconstruction
  Replica        RGB-D        Synthetic Mapping
  ETH3D          Multi-view   Reconstruction
  TUM RGB-D      RGB-D        SLAM & Mapping
  EuRoC MAV      Stereo+IMU   VIO

------------------------------------------------------------------------

# 11. Representative Systems

Classical

-   KinectFusion
-   ElasticFusion
-   BundleFusion
-   Voxblox
-   ORB-SLAM3

Learning-based

-   NeuralRecon
-   NICE-SLAM
-   NeRF
-   Gaussian Splatting

------------------------------------------------------------------------

# 12. Research Challenges

-   Dynamic environments
-   Scale consistency
-   Long-term mapping
-   Loop closure robustness
-   Real-time processing
-   Large-scale scenes
-   Memory efficiency
-   Semantic consistency
-   Embedded deployment

------------------------------------------------------------------------

# 13. Future Directions

Emerging topics

-   Neural Radiance Fields (NeRF)
-   3D Gaussian Splatting
-   Semantic 3D Mapping
-   Dynamic Scene Reconstruction
-   Foundation Models for 3D Vision
-   Vision-Language Mapping
-   Event Camera Mapping
-   Edge AI Mapping

------------------------------------------------------------------------

# 14. Useful Resources

## Libraries

-   Open3D
-   COLMAP
-   OpenMVS
-   GTSAM
-   Ceres Solver
-   Pangolin
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
2.  Visual Odometry
3.  Visual-Inertial Odometry
4.  Depth Estimation
5.  Structure from Motion
6.  Multi-View Stereo
7.  3D Mapping
8.  SLAM
9.  Semantic 3D Mapping

------------------------------------------------------------------------

# Notes

Modern 3D Mapping systems increasingly integrate Visual Odometry, Depth
Estimation, Semantic Segmentation, and Neural Scene Representations to
produce accurate, scalable, and semantically meaningful maps suitable
for autonomous systems and robotics.
