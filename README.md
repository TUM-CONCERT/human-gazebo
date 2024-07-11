# human-gazebo
Gazebo Plugin to send out the human animations as ros messages. Also contains motion capture capabilities. 

## Dependencies:
- CONCERT: [concert_msgs](https://github.com/ADVRHumanoids/concert_msgs) : Defines a ros message for Humans, using keypoints 
- Other: gazebo_ros

## Description
- `animations` contain Collada(`.dae`) files for different human animations.
- `models` contain a the description(`.config` and `.sdf`) for two humans in a simulation, `human_work` and `human_work2`. The latter is a copy of the first with only the actor name changed. This enables it two spawn two humans in the same gazebo simulation.
- `world` contains different gazebo simulation environments. `test_human_work.world` contains only the human and a ground plane, while `concert_with_human.sdf` and `concert_with_two_human.sdf` provide the base environment for the CONCERT project with one or two humans, respectively. They can be used with `.launch` files, as described below
- `launch` contains a dummy `.launch` file to launch gazebo with a specified `.world` file

The dependency graph is as follow, where A -> B means that B is used/included in A.

    launch -> world -> models -> animations
    
In addition to the above described files, this Repository also contains code for a gazebo plugin, which publishes the positions of the human(s) as a `concert_msgs/Humans` message. The code for that is in `source/motion_capture.cpp`, `source/motion_capture.h`,`source/skeleton_node.h` and `CMakeLists.txt`. 

## Installation
Install this project just like any other ros packages
1. Clone it into `catkin_ws/src` using `https://github.com/TUM-CONCERT/human-gazebo.git`
2. Build the environment using `catkin build`
3. Source the environment using `source devel/setup.bash`

## Usage
This package is not intended to be used solely.
For debugging, `roslaunch human-gazebo test_human_work.launch` can start gazebo with the human in the world. The result will look like below:
![image](https://github.com/TUM-CONCERT/human-gazebo/assets/120781514/c73014c0-a37a-44a1-97b3-2cf6a38d47ca)
