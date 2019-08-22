---
author: Henry
topic: Robotics
comments: true
---

A few modules for learning kalman filter.

A simulated world. A few sensors, sensing modules and a fusion model.

Simulated world should be able to change, but providing the same interface.

Sensors should be able to extend in types and numbers.

Fusion model should handle multi-sensor and multi-target tracking.

World model
- Cars as boxes.
- cars with different moving state.
- multi object management.

Ego vehicle
- stationary state or moving state
- adding or removing sensor

Sensor model
- 1d camera bounding box
- 2d lidar scanner
- 2d radar
- timing mode
  - synchronous
  - asynchronous
  - delayed
  - asquent
- range maximum
- probabilistic functioning.

Tracking
- different motion models
- different observation models
- different association methods
- different initialization methods

Visualization:
- 2D
- showing ground truth
- showing estimation
- showing sensor data
- extendable

Logging
estimation and difference to the ground truth

Result
Go deeper with kalman filter, testing innovation, innovation matrix and its relation to error.
Benchmark tracking results with different sensor settings
Benchmark tracking results with different tracking methods

---


