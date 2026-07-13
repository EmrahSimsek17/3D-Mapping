# Visual Odometry (VO)

## Definition

Visual Odometry estimates the 6-DoF motion of a camera using image
sequences.

``` math
T=[R|t]
```

## Pipeline

Image Acquisition → Feature Extraction → Feature Matching → Motion
Estimation → Pose Optimization

## Categories

-   Monocular VO
-   Stereo VO
-   RGB-D VO

## Classical Methods

-   ORB-SLAM
-   LIBVISO
-   DSO
-   LSD-SLAM

## Deep Learning

-   DeepVO
-   TartanVO
-   DroidSLAM

## Metrics

-   ATE
-   RPE
-   Translation Error
-   Rotation Error

## Datasets

-   KITTI Odometry
-   TUM RGB-D
-   EuRoC
-   KITTI-360

## Challenges

-   Scale ambiguity
-   Dynamic objects
-   Illumination changes
-   Motion blur
