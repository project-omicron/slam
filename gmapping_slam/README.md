# About

The gmapping package provides laser-based SLAM (Simultaneous Localization and Mapping), as a ROS node called slam_gmapping. Using slam_gmapping, you can create a 2-D occupancy grid map (like a building floorplan) from laser and pose data collected by a mobile robot - this stage is called Mapping. On the localization stage mobile robot uses real-time laser scanning results and a map to define its location on the map.
Configuration below works fine on the bag-file downloaded by provided link, but did not work with our arena bag-file.

# Dependecies

```
sudo apt install ros-melodic-slam-gmapping
sudo apt install ros-melodic-map-server
```

# How to run

## Mapping (map generation)

Download the Rosbag from <a href="https://drive.google.com/uc?export=download&confirm=wwQS&id=0B46akLGdg-uaa1dDSlUwWUsyTzQ">here</a>.

Install the package and start ROS.

```
mkdir -p catkin_ws/src
cd catkin_ws/src
git clone https://github.com/project-omicron/slam.git
cd ..
catkin_make
source devel/setup.bash
roscore
```

Go to the directory you unpacked the rosbag and play the bag.

```
rosbag play --clock map1.bag
```

In another terminal start the gmapping-SLAM, the script will generate the map.

```
roslaunch gmapping_slam gmapping_without_loc.launch
```

Once the bag finished to play, use map_server to save the map published in topic map as created_map.pgm:
```
rosrun map_server map_saver -f created_map
```

## Localization

To perform localization the package amcl must be installed:
```
sudo apt install ros-melodic-amcl
```

Perform the command:
```
roslaunch gmapping_slam localization.launch yaml_path:=<path to yaml file of created map> bag_file_path:=<path to bag file>
```

Default paths are:
```
yaml_path:=/home/user/catkin_ws/bagfiles/created_map.yaml
bag_file_path:=/home/user/catkin_ws/bagfiles/map1.bag
```

Localization works fine, if initial pose is correctly specified. Otherwise, robot cannot localize itself.

