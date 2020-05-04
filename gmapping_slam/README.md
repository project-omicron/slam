# About

The gmapping package provides laser-based SLAM (Simultaneous Localization and Mapping), as a ROS node called slam_gmapping. Using slam_gmapping, you can create a 2-D occupancy grid map (like a building floorplan) from laser and pose data collected by a mobile robot.
Configuration below works fine on the bag-file downloaded by provided link, but did not work with our arena bag-file. Writing the map not as pgm-file, but as db-file is a current goal.

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
rosbag play map1.bag
```

In another terminal start the RTab-SLAM, the script will generate the map.

```
roslaunch gmapping_slam gmapping_map1.launch
```

Once the bag finished to play, use map_server to save the map published in topic gmapping_group/map as gmapping_map.pgm:
```
rosrun map_server map_saver -f gmapping_map1 map:=/gmapping_group/map
```
