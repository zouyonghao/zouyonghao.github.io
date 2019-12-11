---
title: Run hector-mapping with turtlebot3 in gazebo
layout: post
---

0. env

    `ROS Melodic`

    `ros-melodic-turtlebot3*` installed

1. run `gazebo`

    ```bash
    roslaunch turtlebot3_gazebo turtlebot3_world.launch
    ```

2. run `hector`

    ```bash
    roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=hector
    ```

3. control with `teleop`

    ```bash
    roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
    ```

    Now, use keyboard control the robot. 