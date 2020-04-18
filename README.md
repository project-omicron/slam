# SLAM

Repo to compare different slam algorythms.

Paper: <a href="Comparison_of_Various_SLAM_RG.pdf">Comparison of Various SLAM Systems for Mobile Robot in an Indoor
Environment</a>.

# Why GMapping, RTab and Cartographer?

GMapping is one of the most used algorithm in open source comunity. It is a aprt of the default navigation ROS stack.

RTab is one of the best SLAM that does not require LIDAR. Taking into the account the costs of the LIDARs, we want to compare how good we can create map and localize without a map.

Cartographer is best SLAM based on the paper.


# Comparison design

## Input data

We have a ROS bag with all sensor data.

Here is the list of recorder topics:

	/clicked_point
	/clock
	/imu
	/initialpose
	/joint_states
	/move_base_simple/goal
	/odom
	/r200/camera/color/camera_info
	/r200/camera/color/image_raw
	/r200/camera/depth/camera_info
	/r200/camera/depth/image_raw
	/r200/camera/ir/camera_info
	/r200/camera/ir/image_raw
	/r200/camera/ir2/camera_info
	/r200/camera/ir2/image_raw
	/scan
	/tf
	/tf_static


As you can see, we have a RGB-D camera, LIDAR, IMU, and odometry. This data should be enoght to run most of the SLAM algorithms.

## For data recording

	You could start by lower velocity. Our goal is to create a great map with the least 
	amount of passes as possible. Getting 3 loop closures will be sufficient for mapping 
	the entire environment. You can maximize your loop closures by going over similar 
	paths two or three times. This allows for the maximization of feature detection, 
	facilitating faster loop closures!

## Ground truth map data

ToDo: dump the gazebo world image here.
To create the map, we can use a ROS package <a href="https://github.com/hyfan1116/pgm_map_creator">pgm_map_creator</a>

