# RTab_mapping-and-localization

Deployement of Real time appearance based mapping using ROS package RTAB-Map to map 2 simulated environnements in GAZEBO. The localization is done using adaptive Monte Carlo Localization through the AMCL package.  
An analyzis of the results and the performance is given in the report file. 

# Installation
The environnement in which the project was created had at least : 
    - ROS kinetic 
    - ROS RTAB-map package
    - ROS AMCL packqage 
An appropriate integration has to be conducted if the environnement is different. You can use rosdep to resolve dependecies and install required packages. 
# Configuration
First choose the world. The mapping was done in 2 of 4 existing worlds. 
  - The kitchen dining room : 
[![The kitchen dining room](/pics/Kitchen_dining_room.png)]
  - My_world : 
[![My_world](/pics/Custom_world.png)]

To choose wich world replace the name of the world file in the the world.launch document 

```
<arg name="world_name" value="$(find slam_project)/worlds/My_world.world"/>
```
Then choose the robot's model by replacing the name of the wanted mode xarco file in the robot_description.launch file :
```
<param name="robot_description" command="$(find xacro)/xacro --inorder '$(find slam_project)/urdf/My_bot.xacro'" />
```
The model used is called My_bot and you can find it's urdf files in the urdf folder. Add your own urdf files to use your own customized model. 

[![My_bot](/pics/Custum_robot.png)]

# Usage 

Launch the world.launch to spawn the robot in the chosen world : 
```
roslaunch slam_project world.launch
```
Launch the visualisation on rviz using the robot_slam.rviz configuration : 
```
roslaunch slam_project rviz.launch
```
Launch the AMCL localization : 
```
roslaunch slam_project amcl.launch
```
Launch the RTAB-mapping :
```
roslaunch slam_project mapping.launch
```
To teleoperate the robot using the keyboard launch: 
```
roslaunch slam_project teleop.launch
```
The grid map and 3D map can be found in by visualizating the rtabmp output : 
```
rtabmap-databaseViewer ~/.ros/rtabmap.db
