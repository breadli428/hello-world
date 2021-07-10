# Trouble shooting during summer school

> Following exactly the instruction on [Documentation of the SuperMegaBot (SMB) for the ETHZ Robotics Summer School](https://ethz-robotx.github.io/SuperMegaBot/) from installation of ros to preparation of all the tutorials, the following problems might still occur. This documentation hopefully gives you helpful instructions on dealing with these problems. 

## 1. record bag using `record_sensors.sh`

### problem
comment on topics in the middle might cause missing of all topics behind the comment
### solution
change comment line position

## 2. extract pointcloud from recorded bag using Cartographer

### problem
`.bag.pbstream` file missing
### solution
`.bag.pbstream` file only generated after playing of the bag finished

### problem
`.bag file` not found
### solution
`bag_filename` and `pose_graph_filename` must be specified using absolute path

### problem
`jsk-rviz` dependency missing
### solution
run `sudo apt-get install ros-noetic-jsk-rviz-plugins`

## 3. view `.pcd` file using CloudCompare

### problem
open `.pcd` file failed
### solution
change import file type to all or simply drag `.pcd` file to CloudCompare work space

### problem
trim pointcloud failed to undo
### solution
try to trim with "save" selected area instead of "remove" selected area

## 4. localization

### problem
visualization failed on SMB, since commands differ in simulation and on SMB
### solution
on SMB, when running `localization.launch`, set `launch_rviz:=false` and run `roslaunch icp_localization icp_vis.launch` for visualization

## 5. navigation

### problem
environment failed to load in simulation
### solution
make sure `smb_gazebo` is properly launched since local path planer relies on physical environment
run `roslaunch smb_gazebo sim.launch launch_gazebo_gui:=true` to check simulated physical environment in Gazebo 

### problem
`.pgm` map failed to align with point cloud on SMB
### solution
set `global_frame` to `map` (by default) and set `robot_base_frame` to `base_link`

### problem
use existing global maps for planning failed, `map-server` dependency missing
### solution
run `sudo apt-get install ros-noetic-map-server`

### problem
generate `.pcd` map failed, `octomap-server` dependency missing
### solution
run `sudo apt-get install ros-noetic-octomap-server` and `catkin build octomap_server`

### problem
edit `.pgm` file using GIMP
### solution
remove occupancy by overfilling black-colored pixels with ground color, construct occupancy by filling corresponding pixels with black color

### problem
pixels of 2D map when loading `.pgm` in rviz become patchy even with ground color filled when editing 
 
### solution
since the occupancy map distinguish occupied space from free space with a presumably threshold of color, this should work with no problem

## 6. copy file between server and local machine

### problem
target file not found
### solution
default file path on server is already set to be home directory

### problem
files to be copied to SMB for realization of localization and navigation
### solution
`~/catkin_ws/smb_common/smb_slam/maps/map_to_be_used.pcd`
`~/catkin_ws/smb_path_planer/smb_navigation/config/base_local_planner_adapted.yaml`
`~/catkin_ws/smb_path_planer/smb_navigation/data/test/map_to_be_used.pgm`
`~/catkin_ws/smb_path_planer/smb_navigation/data/test/map_to_be_used.yaml`
`~/catkin_ws/smb_path_planer/smb_navigation/launch/navigate2d_ompl_adapted.launch`

## 7. artefact detection

### problem
to be added ...
### solution
to be added ...