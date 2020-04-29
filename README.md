# outr-simulation

## Purpose
This repository is a complete Catkin Workspace. This workspace has three packages, that simulate the OUTR. With the help of this package, we can develope all software components of the OUTR that require the Robot to exist. Since Gazebo and ROS are used, one can access all properties of the Robot in the simulation, as if it were to the real robot.
The packages are doing the following:

* **outr_description** specifies the entire robot structure as links and joints and can launch the model in rviz.
* **outr_gazebo** launches the model in the gazebo environment.
* **outr_control** launches the model in the gazebo environment where the robot motion can be commanded by the keyboard.

The model is described as URDF under outr_simulation/src/outr_description/urdf, where the outr.xacro file includes the other files.

## Dependencies

- ROS
    - rospy
    - roscpp
    - geometry_msgs
- Gazebo
- This software is tested with:
    - Ubuntu 18.04, ROS Melodic, Gazebo 9
## Install
Assumed, you already installed ROS with Gazebo:

1. Clone this repository to your home directory
```
cd
git clone this repo outr_simulation
cd outr_simulation
```
2. Delete everything within outr_simulation/build/
```
cd build
sudo rm -r *
```
3. Build the workspace with catkin
```
cd ~/outr_simulation
catkin_make
```
4. Don't forget to source your environment
```
source ~/outr_simulation/devel/setup.bash
```

You should now be able to see these packages as ros nodes.

## Usage
Launch the Gazebo simulator and rviz in separate terminals using the following commands:
```
roslaunch outr_gazebo outr.launch
roslaunch outr_description outr_rviz.launch
```
RViz is optional.

### Use `rostopic pub`
After launching the model, in a new terminal use the following command to publish a desired velocity to the `cmd_vel` topic (change values accordingly):
```
rostopic pub /cmd_vel geometry_msgs/Twist "linear:
  x: 0.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 0.0"
```

### Circle Mode:
After launching the model, in a new terminal use the following command to drive the robot in a circle:
```
rosrun outr_gazebo circle_mode.py
```

### Square Mode:
After launching the model, in a new terminal use the following command to drive the robot in a 0.4m square:
```
rosrun outr_gazebo square_mode.py
```
This method is not very accurate.

### Keyboard teleop Mode:
You can use the standard teleop node from the turtlebot. The`keyboard_teleop.launch` file simply remaps the `/turtlebot_teleop_keyboard/cmd_vel` message to `/cmd_vel`.

Launch the gazebo simulator with complete simulation settings using the following command:
```
roslaunch outr_gazebo outr_gazebo_full.launch
```

Start the teleop node:
```
roslaunch outr_control keyboard_teleop.launch
```

Start RViz to visualize the robot state:
```
rosrun rviz rviz
```
