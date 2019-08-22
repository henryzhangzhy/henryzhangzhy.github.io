---
author: Henry
topic: Robotics
comments: true
---

A few modules for learning multi sensor fusion with kalman filter.

---

## Major Functions

A simulated road with cars. A few sensors, sensing modules and a fusion model.<br/>
Simulated world should be able to change, but providing the same interface.<br/>
Sensors should be able to extend in types and numbers.<br/>
Fusion model should handle multi-sensor and multi-target tracking.

---

## Requirements

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

## Questions

1. How to handle relation of sensor and the world? How to let sensor get observation?
   - sensor.read()?? where the reference to world is stored in sensor?
   - sensor.read(world)?? where the reference to world is passed?
   - obj = world.get_object()  
     sensor.read(obj)
   - discussions
     - <https://softwareengineering.stackexchange.com/questions/244476/what-is-decoupling-and-what-development-areas-can-it-apply-to>
2. How to handle the relation of the ego car and other car?
   - All the cars run the motion model, only difference is that sensors are associated to the ego car, by that I mean sensors have their position related to the ego car. Otherwies no difference.
3. How to handle the high level driving task?
   - Keep it simple, go straight by now. constant velocity model. or constant acceleration model, all cars are the same. Cars in the same direction are of the same speed.
   - We do not define road, but define center lane. Make it simple.
4. How to handle the overall program excution flow?
   - Set sensor frequency, world starts running, and run generate sensor data every once a while.
   - Sensor data being processed and sent for plot, logging, world running again.
5. How to handle that the simulator will be coupled with the display?
   - objects out of bound should be removed.
   - new objects should be generated at the boundary.
   - boundary needs to be specified by the ego_car or a view.

---

## Future work.

I would like to extend this work to ROS implementation, as a practice of ROS, and make it easier to migrate to Autoware.
