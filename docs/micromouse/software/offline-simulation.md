---
title: MicroMouse Offline Simulation Software
---

# Offline Simulation with ROS2

Testing every feature on your physical MicroMouse can be difficult and tedious, especially during the early stages of development when there are lots of bugs in your code. For this reason, we've experimented with running MicroMouse robot code natively on desktop and simulating the MicroMouse in a 3D engine. This speeds up the development process greatly since you can set breakpoints while the robot is driving and watch variables in real time – things not possible when running on a physical robot.

To make this happen, you will need to abstract away all your code controlling the robot's hardware. You must configure your build system to have an option to build for robot or desktop. If robot, your build system must enable code controlling your robot's hardware. If desktop, it must enable code controlling the simulation.

Your robot program needs a way to communicate with whatever 3D simulation application you plan to use. We've found that [ROS2](https://docs.ros.org) is awesome for this, even though it sometimes can be painful to install. With ROS2, you can publish variables to "topics" that can be subscribed to by other processes. Some topics your robot program may want to publish would be `drive/linear_velocity` and `drive/angular_velocity`, and some topics your robot program may want to subscribe to would be `vision/ir_sensor_readings` and `buttons/1`. Your simulator program would then subscribe/publish to the topics used by your robot program.

For your 3D simulator, you have many options. In the field of robotics research, [Gazebo](https://gazebosim.org/) is often used for this kind of thing because it integrates with ROS2 well. However, Gazebo is not very well documented and can be very difficult to use. Instead, Game engines are easier to learn and can work just as well. We recommend using one that has native C++ support, since it will make your life easier integrating ROS2. For our recent PCB mouse, we used the [Godot Engine](https://godotengine.org/) with its GDExtension feature to use our C++ code. In your simulator, you should add a way to easily create mazes and save/load them from files. If you would like to see our Godot-based simulator, check it out [here](https://github.com/petelilley/micromouse/tree/main/simulation).

