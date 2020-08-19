# Extended Kalman Filter Project Starter Code
Self-Driving Car Engineer Nanodegree Program

Table of Content
---

In this project a kalman filter has to be built and to start off, the udacity readme provides information on what needs to be accomplished and what information will be provided.

To give a walkthrough of the code structure we will be going through the additions made to the respective files `src/FusionEKF.cpp`, `src/FusionEKF.h`, `kalman_filter.cpp`, `kalman_filter.h`, `tools.cpp`, and `tools.h`.

1. [Udacity Readme](#udacity-readme)
2. [FusionEKF](#fusionekf)
3. [Kalman Filter](#kalman-filter)
4. [Tools](#tools)
5. [Results](#results)

Udacity Readme
---

The following has been provided by Udacity and are also the things to keep in mind when building this project.

Note that the programs that need to be written to accomplish the project are src/FusionEKF.cpp, src/FusionEKF.h, kalman_filter.cpp, kalman_filter.h, tools.cpp, and tools.h

The program main.cpp has already been filled out, but feel free to modify it.

Here is the main protocol that main.cpp uses for uWebSocketIO in communicating with the simulator.


**INPUT**: values provided by the simulator to the c++ program

["sensor_measurement"] => the measurement that the simulator observed (either lidar or radar)


**OUTPUT**: values provided by the c++ program to the simulator

["estimate_x"] <= kalman filter estimated position x

["estimate_y"] <= kalman filter estimated position y

["rmse_x"]

["rmse_y"]

["rmse_vx"]

["rmse_vy"]

---

## Other Important Dependencies

* cmake >= 3.5
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make` 
   * On windows, you may need to run: `cmake .. -G "Unix Makefiles" && make`
4. Run it: `./ExtendedKF `

FusionEKF
---


The file, [src/FusionEKF.cpp](src/FusionEKF.cpp) moslty handles the usage the Kalman Filter.  Firstly, it detected if the filter has been initialized before or not, if it hasnt, it will initialize all the necessary variables depicted in lines 80-112.

Before mentioning the next steps, it should also be noted that upon first initialization, the necessary matrices are also created.  This is shown in lines 41-58.

Next the **Predict** stage from lines 125-149 will be carried out which will then be used to **Update** the *state* and *covariance* matrices.  However, 1 measurement is linear and the other is non linear.  Hence, a handle is created to handle which Filter or calculations are used based on the measurement type.  This is in lines 162-173.

Kalman Filter
---

The [kalmam_filter.cpp](src/kalmam_filter.cpp) file contains all necessary calculations for the **Predict** and **Update** stage.

As previously mentioned in FusionEKF a handler was created to distinguish between RADAR and Laser measurements.  All these can be seen in the code from line 16-90.

Tools
---

[tools.cpp](src/tools.cpp) contains 2 helpful functions, `CalculateRMSE()` and `CalculateJacobian()`.  

Firstly, the jacobian is very straightforward and it follows the derivate calculation used in the Udacity Classroom shown in line 61-89.

Next the `calculateRMSE()` function should be straightforward where we calculate the root mean sqaure error.  However, every single time this function is called, it will have to loop over all of it's previous values and this can be ineffective.  A workaround is to remember the last *mean square error* which will allow for a very efficient calculation shown in lines 13-59.

Results
---
The RMSE for each dataset was the following:

```
Dataset 1:  
RMSE <= [0.0973, 0.0855, 0.4513, 0.4399]
Dataset 2: 
RMSE <= [0.0726, 0.0965, 0.4216, 0.4932]
```
