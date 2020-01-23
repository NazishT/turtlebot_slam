# turtlebot_slam

<b> SLAM MAP BUILDING WITH TURTLEBOT </b>

# Robot setup: 
Hokuyo URG-04LX-UG01 Scanning Laser Rangefinder
Joystick xbox36 and 
Kinect Camera 
Turtlebot2. 

# Operating System: 
Ubuntu 16.04
ROS Kinetic


# SLAM : Fast SLAM through gmapping


# 1. SSH into the Turtlebot 
Find out the Turtlebot's ip on Turtlebot's Netbook. 
```
if config
```
Find out the ip of the Turtlebot and use it to ```ssh``` into the Netbook  

On your workstation,type the following . Type the password if password protected. 

```
$ ssh username@192.168.x.y

```
# 2. Bringup the Turtlebot 
After the connection is established, bring up the Turtlebot.

```
$ roslaunch turtlebot_bringup minimal.launch
```
In another terminal window of Netbook, initate SLAM through gmapping. 

```
$ roslaunch turtlebot_navigation gmapping_demo.launch
```
# 3. Use the gamepad for teleoperation 
To use the joystick, initate joy node

```
$ rosrun joy joy_node
```
in another terminal window

```
$ roslaunch turtlebot_teleop xbox360_teleop.launch
```
# 4. Start the 3D LaserRange Finder
Now to bringup the LaserRange Finder, use the ```hokuyo_node``` instead of ```urg_node```. To set up URG-04LX-UG01 on Kinectic for the first time, read *this*. 

```
$ rosrun hokuyo_node hokuyo_node
```
In another terminal: 

```
$ rosrun tf static_transform_publisher 0 0 0 0 0 0 /plate_middle_link /laser 1000
```

# 5. Connect Kinect 
For using Kinect Camera, do the followig: 

```
echo $TURTLEBOT_3D_SENSOR 

```
It produces the following output: >>asus_xtion_pro. In order to add Kinect to the bashrc:

```
echo "export TURTLEBOT_3D_SENSOR = Kinect" >> .bashrc
```
Now launch the ```openni```

```
roslaunch openni_launch openni.launch
```

# 6. Visualization on Rviz 

For visualization, launch ```Rviz```

```
roslaunch turtlebot_rviz_launchers view_navigation.launch

```

On ```Rviz```  on the *Global Options* change the Fixed Frame to ```/laser```. In case it is not mentioned in the menu, type it manually. To see the scan lines, go to ```Add``` button , select ```LaserScan``` and change the topic to ```scan```.

