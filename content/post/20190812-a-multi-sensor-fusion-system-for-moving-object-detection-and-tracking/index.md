---
title: A Multi Sensor Fusion System for Object Detection and Tracking
date: 2019-08-12
description: A multi Sensor Fusion System for Object Detection and Tracking in Urban Driving Environments.
author: Henry
categories:
    - Autonomous Vehicles
tags:
    - Sensor Fusion
comments: true
---

A paper on sensor fusion system using EKF to fuse LIDARs, raders and cameras.

This paper presents a two-layer fusion system. A sensor layer processes the raw sensor data and generates features and then generates proposals based on the features, partly across multiple sensors. The fusion layer fuses the sensor measurements using an Extended Kalman Fileter (EKF). Where measurements from all sensors are processed sequentially and asynchronously. Measurements are associated with the tracked objects based on their type. Each type of measuremnt has its own measurement model for update the associated object.

---

## Sensor Setup

The platform introduced in this work use 6 LIDAR and radar pairs and three cameras for perception.

LIDARs are 4-layer LIDAR with range up to 200m.
Radar1 has a max range of 250m and radar2 can be configured to 60m or 175m.
Two cameras, one in the front, one in the back have a resolution of 640*480.
The third camera is a thermal camera.

Any object within 200 meters will be projected onto sensor converge and within 60 meters will be seen by at least two different types of sensors.

---

## Sensor Layer

The sensor layer is made of sensor-specific modules. Each module takes the raw data and uses sensor-specific algorithms to generate high level features. And object proposals will be generated from these features.

For radars, we can get 2D position and direct measuremnt of the speed of the target. The measurement at time $k$ would be represented as 

$z^R(k) = {r_1, r_2, ..., r_p},$

where $r_i = [x, y, dx, dy]^\top, i = 1, 2, ..., p.$

All six LIDARs are treated as one homogeneous sensor. Analyzing their measurements using built-in segmentation and extract features line segments or junctions of lines ("L") shape [2]. we can get pose in 3D and size (partially)

$z^L(k) = {l_1, l_2, ..., l_q},$

where $l_i = [x, y, \theta, dx, dy, w, l]^\top, i = 1, 2, ..., q.$

For cameras, we can get the bounding box in the image frame and a class label.

$z^C(k) = {c_1, c_2, ..., c_r},$

where $c_i = [x_1, y_1, x_2, y_2, class]^\top, i = 1, 2, ..., r$.

---

## Fusion Layer

The fusion of multiple sensor measurements employ the sequential-sensor method. Which treats observations from individual sensors idnependently and sequentially feeds them to the EKF's estimation process.

### Tracking Models

#### Motion Models

A point model and a 3D box model is used for motion prediction. A point model is effective in localizing objects that are far away and we don't care about its shape and orientation. A 3D model is effective for objects that are near the vehicle and provides oritentaion and shape estimation.

Here the point model is a constant acceleration model in 2D:

$x(k) = [x, y ,v_x ,v_y, a_x, a_y]^\top$.

and the box model is represented by:

$x(k) = [x, y, \theta, v, \omega, a, w, l, h]^\top$.

where $\theta$ is yaw angle, $\omega$ is yaw rate, $w$ is width, $l$ is length, $h$ is height.

For more on motion model, [4] is a previous work on this.

#### Observation Models

Observations from sensors will be associated with corresponding objects, then observation model is applied to update the state estimation. Data association will be introduced in the next section. If an observation is not associated with any esisting object, object instantiation should happen.

We have observations from three sensors, they provide different information about the model. And we have both point model and box model. If we have corresponding update for all possibilities, we will have six observation models.

But notice that radar cannot update the box target, it only update the point target.

LIDAR measurements are primarily used for update the box target, it also can bu used to update the point target.

Camera measurements cannot be used for position estimation due to poor depth estimation. Thus it is only applied to the box model for update the width and height.

Details about the update step are not list in this post currently.

### Data Association

Measurement data is sequentially sent to the EKF, thus the association process will handle one measurement to all objects. My interpretation is that a prediction step for all objects should happen before association. The association of prediction and measurement is sensor dependent.

For LIDAR meansurements, association of point model is based on distance of prediction and measurment. For box models, possible interpretations of the edge target is generated and interpretations with max overlap with predicted object is selected. This in pratice occasionally fails thus vision target is utilized here. When vision target give higher reponse on a particular view of a vehicle (eg. back view), we can filter interpretations of other views (eg. side view).

Association of camera measurements is achieved by projecting the prediction of the point model or box model into the pinhole camera model and compute the distance to the midpoint of the bottom line of the detected bounding box. The object whose point is the nearest neighbbor is associated.

For association of radar measurements, a set of possible point targets are generated from predected model. Specifically, several points along the contour is generated for a box model and one point for a point model. The enhancement for a box model using multiple points is due to poor lateral position estimation from radar. Association is made by the nearest-neighbor approach.

### Movement Classifications

Movement Classification is hard for LIDAR detection cause shape changes when the car is driving and the center is hard to estimate. I had a headache with this when I was doing shape estimation. This method is definitely worth trying.

Two flags are set for movement classification same as [4].

- the __movement history flag__ is raised when the tracking system determines that the position of a tracked object has significantly changed. The distance traveled is computed from the last time stamp that the object has been classified as not observed moving. Emprically determined thresholds for pedestrians, vehicles and cyclists are used to compare with the distance. 
- the __movement state flag__ is raised when the tracking system determines that the object is moving. Radars provide the directly estimation of moving state while LIDAR can estimate the speed over time.

### Comments

Result shown 93.7% by human inspection with 5.7 false positives per minute. Not sure what this exactly means.

I think this is a very clear paper about sensor fusion. I like the proposed system.

### Reference
[1]  Cho, Hyunggi, et al. A multi-sensor fusion system for moving object detection and tracking in urban driving environments. _Robotics and Automation (ICRA), 2014 IEEE International Conference on. IEEE_, 2014.

[2] C. Mertz et al. Moving Object Detection with Laser Scanners. _Journal of Field Robotics_, 30(1):17-43, 2013.

[3] H. Durrant-Whyte. _Multi Sensor Data Fusion_. Lecture Notes, 2006.

[4] M. S. Darms, P. Rybski, C. Baker, and C. Urmson. Obstacle detection and tracking for the urban challenge. _IEEE Transaction on Intelligent Transportation Systems_, 10(3), 2009.