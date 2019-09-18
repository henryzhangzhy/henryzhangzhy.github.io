---
author: Henry
topic: Robotics
comments: true
---

A few modules for learning multi sensor fusion with kalman filter.

---

## PyKFFusion

[project link](https://github.com/ZHYHenryZhang/pykffusion)

[drawing link](https://docs.google.com/drawings/d/1BHVoEV2kz0GJIh1zaZzxKpuBi689tOnlxy04gQNYBGw/edit?usp=sharing)

---


## Kalman Filter
We have two motion models, a point model and a box model.

The point model is a constant acceleration model in 2D, with the state $x = \[x, y, v_x, v_y, a_x, a_y\]^T$. 

Initially, I implemented the Kalman Filter in this way.
```python
self.x_pre += dt * (self.mtx_transition @ self.x_post + np.dot(self.mtx_control, u))
self.P_pre += (dt**2) * (self.mtx_transition @ self.P_post @ self.mtx_transition.T + self.noise_process)
```
Which I though would take the time into consideration. But it turns out that there is a second order term of dt in mtx_transition.

With the method mentioned in [multi sensor fusion](https://zhyhenryzhang.github.io/2019/08/18/multi-sensor-data-fusion-hugh-durrant-Whyte.html).

First, we define the continuous model as 
\begin{equation}
  \dot{\mathbf{x}}(t) = \begin{bmatrix} 
                     0 & 0 & 1 & 0 & 0 & 0 \\\\ 
                     0 & 0 & 0 & 1 & 0 & 0 \\\\ 
                     0 & 0 & 0 & 0 & 1 & 0 \\\\ 
                     0 & 0 & 0 & 0 & 0 & 1 \\\\ 
                     0 & 0 & 0 & 0 & 0 & 0 \\\\ 
                     0 & 0 & 0 & 0 & 0 & 0
                     \end{bmatrix} \mathbf{x}(t).
\end{equation}

Then, we discretize the model $ \Delta{t} = t_{k}-t_{k-1}$ and get
\begin{equation}
  \mathbf{x}(t_{k}) = \begin{bmatrix}
                      1 & 0 & \Delta{t} & 0 & \Delta{t}^2/2 & 0 \\\\ 
                      0 & 1 & 0 & \Delta{t} & 0 & \Delta{t}^2/2 \\\\ 
                      0 & 0 & 1 & 0 & \Delta{t} & 0 \\\\ 
                      0 & 0 & 0 & 1 & 0 & \Delta{t} \\\\ 
                      0 & 0 & 0 & 0 & 1 & 0 \\\\ 
                      0 & 0 & 0 & 0 & 0 & 1
                      \end{bmatrix} \mathbf{x}(t_{k-1})
\end{equation}
Thus we need to prepare the F first before we doing prediction. 

Very nice result of error and innovation is obtained.
With the correlation coefficient as below.
```
[[1.         0.30643922]
 [0.30643922 1.        ]]
```
![Single Tracking]({{ site.url }}/assets/images/single_object_tracking_1.png)

Single Object Tracking, below is the error and innovation.
The error is defined as the position difference of the ground truth and the estimation.
The innovation is defined as the length of the innovation in position of the Kalman Filter.

![error and innovation]({{ site.url }}/assets/images/single_object_error_innovation_1.png)

Interesting result about multi sensor fusion was found, that simply by adding more sensor wouldn't help improve the result. If the covariance of observation is too small, new observation in sequential fusion will just behave similar to overwrite the previous observation. A larger observation variance will fuse the multiple sensors better.
Note that we then need to balance the prediction and observation noise together as well.
check multi_sensor_tracking_error_innovation_5.png for reference.

So now we have two balances.

- The balance of prediction noise and observation noise.
- The balance of observation coming from different sensors.

Further parameter tunning shown that there is a conflict between the two balance, we can not get the best out of the data for a fixed covariance.

In sequential filtering, the two balances are coupled. Because we treat them sequentially, the information of our previous update will be in the prediction. Let say if we trust our observation more. Then the later observation will simply overwrite the previous observation, even though they come at the same time. This is where order matters happens. And if we lower the confidence of our observation, then it takes longer to get initial filtering right.

Another perspective comes from the data itself. For example, if the radar observation noise is proportional to the distance to that object. Then for two sensors that both observe the same object, but one is close to that object, the other is further, we should assign higher weights to the observation from the closer observation. But a sequential filtering system with fixed observation noise cannot handle this properly. (Think about order matters)

This is also true for group fusion method, where we cannot just stack the same observation noise matrix diagonally to form the observation noise matrix. We should adjust them based on the confidence of the observation.

__The the question becomes, how can we adjust the noise for single observation?__

---

## Multi modal sensor fusion

After adding the centered radar as the first sensor, I continued to add lidar to make a multi modal system.

Adding lidar as a sensor, it would be natural to think about generating lidar point cloud and process the point cloud to estimate. But it turns out to be much more complicated than these two.

The question becomes, what do we need to do to add a new sensor (modal)?
1. generate sensor data from Object
2. generate proposals from sensor data

as the proposal is in fact a model, what if the sensor brings a new model to this system? In this case, we use point model for radar but lidar is more suitable to a box model.

There are some problems in handling with multi models.
1. generate tracker from proposals
2. associate tracker with proposals
3. update tracker using matched proposals

And more detailed problems that are harder to notice.
4. Do we convert multi models? When? How?
5. Should we merge multi models? When? How?
6. Do we associate trackers with all models to proposals from all sensors?

And a problem specific for lidar.How to handle multiple proposals from detection of a single object? For example, when we get a set of points of a line, it can be any of the edges of a car, thus multiple proposals can be proposed from it. By how to handle it, we really means 
7. Do we initialize a tracker for each proposal? Yes, when no more information.
8. Do we treat them as separate observation or related? Related if from single detection, we only associate the most matched pair.
9. How do we reduce the number of trackers when new information is available?

Writing these down really helped organizing them :p

---

## Experiments

1. Testing the relation of tracking performance and innovation.
   - meansure the distance of the estimation and the ground truth.
   - meansure the innovation.
   - plot them as a function of time.
2. Testing multi-sensing kalman filter and the performance gain.
   - measure error when using one radar and two radar and more.
   - change the position of the radar.
   - using bearing sensor.
3. Testing sequential method and group method, performance, time.
4. Testing information filter
5. Testing multi object data association methods.
6. Testing asynchronous, delayed, asequent data.

---

Contents below will be kept unchanged, as a live mistake show on project design. I thought too much about reuse and extensibility before I get the program work. Details goes in the post [programming philosophy](https://zhyhenryzhang.github.io/2019/08/25/programming-philosophy-yinwang-reading-notes.html).

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
  - asequent
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

1. How to handle relation of sensor and the world? How to let sensors get observation?
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
6. Meta questions
   - How to I generate a tracker from a proposal?<br/>
     create a model depend on the proposal type
   - What type of information does a proposal need to provide to a tracker?<br/>
     - sensor type
     - sensor data (no, but I need abstract away the sensor information)
   - What is a proposal?
     - It provides a possible object, along with a probability.
   - Should proposal be defined as a type?
   - should the pos defined as .x, .y, .z or pos(x, y, z)
   - should the box include 3D?
   - we want to generate the filter from point model, should we generate it inside the point class or outside?
   - Fusion.py is tightly coupled with the way that sensors provide data. See class SensorData in sensor.py
   - Kalman Filter that is competible with different time.
   - prediction and association, how to coorperate?
   - It becomes very hard to have testings.
   - How to handle similar proposals, do we fuse proposal first or merge trackers? Merge close once.
   - For each lidar detection, we can generate multiple proposal with different orientation. How to handle this?
     - For each detection, If none of its proposals are matched, we initialize for all of them.
     - If some matched, we pick the one with best fit, and remove all other matches.
     - How to handle only match one when there are multiple association?
       - pre-associate
       - if no match, return None
       - If more than one match, find best match and associate.

---


## Future work.

I would like to extend this work to ROS implementation, as a practice of ROS, and make it easier to migrate to Autoware.
