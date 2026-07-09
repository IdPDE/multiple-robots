# Multiple robots in ROS2
Multipe robots (3 swerve drive and 3 diff drive) in Gazebo and Rviz with Nav2. Every node/topic/controller are linked to a robot by namespace.

![Gazebo environment](figures/Gazebo.png)

Tested in ROS2 Jazzy Jalisco.

## Content
This repository currently includes the following packages:
* differential_drive_controller: contains the controller for the 3 diff-drive robots (robots 4, 5 and 6). The differential controller is a copy of the ROS2 control diff drive controller, adapted so that the namenspace works properly and tf's are disabled (using tf_dummy) in order for ekf filter to publish the tf's.
* ffw_swerve_drive_controller: contains the controller for the 3 4-wheeled-swerve-drive robots (robots 1, 2 and 3). The controller is based on the swerve controller from ROBOTIS AI Worker with the adaptation that the tf are relative and not global (/tf) so that every node/topic is namespace for each robot.
* mulitple_robots: main package containing the robots bringup, configs files, descriptions, meshes, Rivz and Gazebo world files, all namespaced.
* scan_mask_filer: Gazebo Lidar scan fileter to eliminate echoes from the robots own wheels.
* stamped_filter: creates /cmd_vel_stamped as input for the diff drive robots, the swerve drive robots need unstamped.

## Installation instructions & dependencies

To install the packages from inside your workspace:
```console
cd src
git clone https://github.com/IdPDE/multiple-robots
```

Make sure that the following are properly installed in the ROS2 Jazzy Jalisco environment:
* Rviz 
* Nav2
* Robot state publisher
* Joint state broadcaster
* GazeboSim Harmonic

## Execution of the project
### Launch enviroment with multiple robots
This will launch one Gazebo enviroment and for every robot Rviz.
```console
ros2 launch multiple_robots robots.launch.py
```
You can start with goal planning for an individual robot if the Nav2 plugin in Rviz2 shows Navigation and Localization as active. Sometimes due to the large number of nodes to be launched, a single robot fails to launch, try to launch again, most of the time this will help.

## To-do
- [ ] Make the launch a bit more stable, not always all robots will launch properly
- [ ] Make changes to Nav params file to have a better collision detection (correct footprints)
- [ ] Changes some speed setting so robots drive at different speeds
- [ ] Combine some of the config files, not all are really robot specific
- [ ] Make the bt_navigator of the swerve drive robots with a dual controller, general (more diff drive) and last part (more omni drive)
