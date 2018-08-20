# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `install-mac.sh` or `install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.

* **Ipopt and CppAD:** Please refer to [this document](https://github.com/udacity/CarND-MPC-Project/blob/master/install_Ipopt_CppAD.md) for installation instructions.
* [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page). This is already part of the repo so you shouldn't have to worry about it.
* Simulator. You can download these from the [releases tab](https://github.com/udacity/self-driving-car-sim/releases).
* Not a dependency but read the [DATA.md](./DATA.md) for a description of the data sent back from the simulator.


## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./mpc`.

## Rubic Points
1. describes their model in detail. This includes the state, actuators and update equations.

The state consists of 6 components: x- and y-coordinates, car's orientation(psi), velocity, cross tracker error, and orientaton error. Actuators include the accelerate a and steering angle delta. The update rule is as following: 
![update](./update.png)

2. discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. 

N = 10 and dt = 0.1. This indicates the MPC take 1 secound updating into consideration. I read this in the slack discussion channel.

3. The preprocessing of waypoints, the vehicle state, and/or actuators prior to the MPC procedure.

The waypoints must be transformed to the cars persperctive. That means, it must be computed into car's coordinate system.

4. details on how to deal with latency.

In the MPC there will be a variable defined as delay. 100ms latency means exactly 1 step delay in the N and dt setting. In this manner, the actuator will be used 1 step before to for the update equation.