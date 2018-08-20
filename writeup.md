## Questions in Rubric
---

### 1. Describes their model in detail.
The model is characterized by the state vector and the actuator vector. The state vector described how the car is current moving and the actuator vector shows the control commands to the car.

Specifically, the state consists of 6 components: x- and y-coordinates, car's orientation(psi), velocity, cross tracker error, and orientaton error. Actuators include the accelerate a and steering angle delta. The update rule is as following: 
![update](./update.png)

---

### 2. Discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values.
For the choice of N, the larger it is, the longer the MPC will consider the future. However, increasing the N will enlarge the computation complexity.

The dt is the temporal resolution of the MPC. The smaller is the dt, the finer the resolution it will have. 

 Finnally the N = 10 and dt = 0.1. This indicates the MPC take 1 secound updating into consideration.

---
 ### 3.The preprocessing of waypoints, the vehicle state, and/or actuators prior to the MPC procedure. 
 
 The waypoints must be transformed to the cars persperctive. That means, it must be computed into car's coordinate system. The computation is happened in the following code section:
 ```cpp
 car_pers_x(i) = cos(-psi) * (ptsx[i] - px) - sin(-psi) * (ptsy[i] - py); 
car_pers_y(i) = sin(-psi) * (ptsx[i] - px) + cos(-psi) * (ptsy[i] - py); 
```
 ---


### 4.details on how to deal with latency. 

In the MPC there will be a variable defined as delay. 100ms latency means exactly 1 step delay in the N and dt setting. In this manner, the actuator will be used 1 step before (i.e. 100ms earlier) to for the update equation.