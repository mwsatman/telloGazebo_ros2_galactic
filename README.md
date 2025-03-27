# Basic Docker Setup for Tello drones

This repository contains the docker setup with Ubuntu 20.04, ROS2 Galactic, and additional library to execute Tello Gazebo Simulation and real-robot interface for [drone_racing_ros2](https://github.com/TIERS/drone_racing_ros2) github repository.
This implementation is still experimental at this point, and may need additional adjustment in the docker configuration depending on the computer.

So far it has been tested and working on: 
- Ubuntu 24.04 both with 1) only Intel chipset and 2) Intel with Nvidia GPU


## Requirement:
- Have docker installed
- Visual Studio Code with the following extensions: Remote Development, Dev Containers, Docker

Note: 
- this repository setup follows closely to [ArticulatedRobotics Youtube tutorial](https://www.youtube.com/watch?v=dihfA7Ol6Mw&list=PLunhqkrRNRhaqt0UfFxxC_oj7jscss2qe&index=6&ab_channel=ArticulatedRobotics)
- Another good tutorial for the setup and debug is this tutorial [ROS2-Iron + Docker + VSCode](https://docs.ros.org/en/iron/How-To-Guides/Setup-ROS-2-with-VSCode-and-Docker-Container.html)



## Basic steps:
- download or clone repo to your local folder
- open the folder in visual studio code
- clone the repository [drone_racing_ros2](https://github.com/TIERS/drone_racing_ros2) into `drone_racing_ros2_ws/src`
- `Ctrl+P` --> Reopen in Containers
- `colcon build` inside `drone_racing_ros2_ws` -->  Build the packages within the ROS2 workspace

When the container is executed properly (without error), all the required libraries should be installed.
At this point you should be able to run teleop simulation in Gazebo or connect and control the Tello drone.


## Common Issue:

One common issue is the gazebo returning errors or running without display. 
In this case, it is best debug by launching rviz2 and see if it is running well (you can do this by simply calling `rviz2` inside the docker terminal). 
If rviz2 fails to load normally, then most probably you need to adjust some docker configuration or some permission to enable the GUI. 

For newer Ubuntu system (e.g., 24.04), quoting the notes from [ROS2-Iron + Docker + VSCode](https://docs.ros.org/en/iron/How-To-Guides/Setup-ROS-2-with-VSCode-and-Docker-Container.html) (at the bottom)

> Note: There might be a problem with displaying RVIZ. Please make sure to allow the user to access X window system with `xhost +local:<USERNAME>`. If no window still pops up, then check the value of `echo $DISPLAY` - if the output is 1, you can fix this problem with `echo "export DISPLAY=unix:1" >> /etc/bash.bashrc` and then test it again. You can also change the DISPLAY value in the devcontainer.json and rebuild it.


If you plan to use Hardware Acceleration with Docker, then you need to adjust the docker configuration. Several possible ways based on the chipset are listed in this [Wiki ROS](https://wiki.ros.org/docker/Tutorials/Hardware%20Acceleration#Intel) documentation.
