# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

# **Project: PID Controller**
[![Udacity - Self-Driving Car Engineer NanoDegree Program](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)


## Overview
This repository contains all the codes and reflection that required for completing project. The goal of this project is to implement the PID controller that make car drive the track of given simulator. To do that we should set hyperparemters for the controller.


## Reflection

In this project, I want to obtaiin steering angle with `cte`(cross track error) which is distance between vehicle and reference trajectory. Explanations of each `P`, `I`, `D` components are followed.

1. `P` : `P` (proportional) controller determine vehicle's steer angle proportionally with distance between vehicle and center line. But, the usage of only `P` component makes the vehicle's trajectory overshooted and oscilated.

1. `I` : When car's alignment is not right, certain amount of steering is needed to compensate mis-alignment. In that situation, steering angle 0 can't minimize `CTE` or can't follow the reference line indefinitely. To avoid that situation, `I`(integral) component which is accumulation of `CTE` over time is used for updating error measurement. `I` indicate if the vehicle spending more time on one side of the trajectory or the other.

1. `D` : `D` controller is used to correct overshoot problem of `P` controller, using dffierential rate of `CTE`. The speed of how the vehicle approaches fast to the target trajectory.


### Final hyperparameters

I set hyperparameters manually instead of using twiddle or other optimization techniques. I think this manual parameter setting is enough to acheive the goal of this project.

I think there is no bias in the simulation, so I choose very small value for `I=0.0001`. To minimize osciliation, I increases the parameter `D` to `8.0`. With many trial and error, I found the optimal value for `P` to `0.2`.

In addition, the throttle value is also important. It is too big, then osciliation occurs very often. So decrease the value of throttle from `0.3` to `0.1`, instead of using another PID controller.

The final parameters are `(P, I, D) = (0.2, 0.0001, 8)`.

## Result

My controller can keep the vehicle going without troubles during two laps. You can see the result at https://youtu.be/O-1aOHl11No.

![GitHub Logo](screenshot.png)