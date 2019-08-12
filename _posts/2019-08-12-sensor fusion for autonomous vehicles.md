---
Author: Henry
topic: Autonomous Vehicles
---

Explore sensor fusion methods. Index page of findings in this area.

Sensor fusion is to extract the information from heterogeneous sensors that complement each other. For the sensors that are commonly used in Autonomous Vehicles, like LIDARs, radars and cameras, this is obvious.

Cameras are rich in texture and semantic information, like color, material, and signs. But they are poor at depth estimation. LIDARs can provide accurate depth information, using 3d point clouds, but everything is just a point cloud with a 3D position and a reflection rate. You cannnot distinguish a red light and a green light. radars can directly provide speed estimation, which is usually better than estimating using LIDARs[1].

Recent advances in Autonomous Vehicles are highly dependent on sensor fusion. And companies like Waymo, Lyft, Zoox are using multi-sensor settings on their car. While research in single modal perception has a lot of advances, like deep-learning based visual recognition, new representation for point cloud learning, the fusion of them is unclear to me. This area is not much introduced in class and I feel like I need to invest some time on figuring out the big picture in this area by reading literatures.

I would divide the sensor fusion systems into several categories and talk about them. It includes:

- mathematical modeling methods
- deep learning methods

---

## Mathematical Modeling Methods

### [A Multi-Sensor Fusion System for Moving Object Detection and Tracking in Urban Driving Environments]()

A paper on sensor fusion system using EKF to fuse LIDARs, raders and cameras. This paper presents a multi-layer fusion system. Layer one processes the raw sensor data and generate features. Layer two will generate proposals based on the features, partly across multiple sensor. Layer three fuse the sensor measurement using an Extend Kalman Fileter (EKF). Where measurements from all sensors are sequentialized and processed asynchronizedly. measurements are associated with the objects based their type and each type of measuremnt has its own measurement model.

---

## Deep Learning methods


---

### Reference


