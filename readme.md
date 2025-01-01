## Requirements

-   Ubuntu 18.04
-   ROS Melodic
-   ethz-adrl / control-toolbox [1]
-   VScode 1.85.2
-   PX4 14.4 (git clone --branch v1.14.4 https://github.com/PX4/PX4-Autopilot.git --recursive)

## Commands

### Compiling the Library

It is assumed that you have a valid catkin-workspace set up, e.g. using catkin tools. Then, execute the following steps. [1]

```
cd ~/your_workspace
catkin build -DCMAKE_BUILD_TYPE=Release
```

1. Build px4_sitl gazebo

```
 make px4_sitl gazebo
```

2. Run MAVROS with

```
source .../devel/setup.bash
roslaunch mavros px4.launch fcu_url:="udp://:14540@127.0.0.1:14557"
```

3.  Runs PX4, VRPN (VICON mocap), and relay pose data.

```
roslaunch lqr_controller mavros_vrpn.launch
```

-   Runs main controller and loads param.yaml file.

```
roslaunch lqr_controller lqr_euler.launch
```

4.  Drone Off-board control

```
commander arm
commander mode offboard
```

## References

-   https://github.com/llanesc/lqr-tracking
-   Foehn, Philipp & Scaramuzza, Davide. (2018). Onboard State Dependent LQR for Agile Quadrotors. [10.1109/ICRA.2018.8460885](https://doi.org/10.1109/ICRA.2018.8460885).
-   [1] ethz-adrl / control-toolbox [Installation](https://github.com/ethz-adrl/control-toolbox/wiki/Quickstart)
