---
Author: Henry
topic: Autonomous Vehicles
---

A paper on sensor fusion system using EKF to fuse LIDARs, raders and cameras.

This paper presents a two-layer fusion system. The sensor layer processes the raw sensor data and generates features and then generates proposals based on the features, partly across multiple sensors. The fusion layer fuses the sensor measurements using an Extend Kalman Fileter (EKF). Where measurements from all sensors are sequentialized and processed asynchronizedly. Measurements are associated with the tracked objects based on their type. Each type of measuremnt has its own measurement model for update the associated object.

---

## Sensor Setup

The platform introduced in this work use 6 LIDAR and radar pairs and three camera for perception.

LIDARs are 4-layer LIDAR with range up to 200m.
radar1 has a max range of 250m and radar2 can be configed to 60m or 175m.
two cameras, one in the front, one in the back have a resolution of 640*480.
The third camera is a thermal camera.

Any object within 200 meters will be projected onto sensor converge and within 60 meters will be seen by at least two different types of sensors.

---

## Sensor Layer

The sensor layer is formed by modules for each sensor. Each module take the raw data and using sensor specific algorithms to generate high level features. And object proposals will be generated from these features.

For radar, we can get 2D position and direct measuremnt of the speed of the target. The measurement would be represented as 

z^R(k) = {r_1, r_2, ... r_p}

where r_i = [x y dx dy]^T, i = 1, 2, ..., p.


---

## Fusion Layer
