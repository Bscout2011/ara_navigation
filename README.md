# ara_navigation
This code is belong to the hybrid steel bridge inspection robot - ara lab.
This code is used to navigate the robot to run on steel bridge structures

# Install Instructions

*Tested on Ubuntu 18.04 with [ROS Melodic](http://wiki.ros.org/melodic/Installation/Ubuntu).

Create a [ROS catkin workspace](http://wiki.ros.org/catkin/Tutorials/create_a_workspace). First create a folder in your home directory called `catkin_ws` then add a folder beneath it called `src`. Clone the `pahap` directory under `src`. Open a terminal in `catkin_ws` and execute `catkin init`. Finally build the workspace with `catkin build`. (First time build might error because of missing packages. Install the missing packages with the command `sudo apt install ros-melodic-"missing-package-name"`).

# Run Instructions

From `catkin_ws` source the workspace in terminal `source devel/setup.bash`. Run the launch file `roslaunch pahap pahap.launch`.

# Program Overview

### 1. Pointcloud read and preprocessing.

Processed by [pahap.cpp](src/pahap.cpp). Given a pointcloud `.pcd` file, performs pass-through filtering, down sampling, and coordinate transformation from camera to robot frame of reference.

Main function starts node handles, sets parameters

### 2. Segmentation

Given processed pointcloud, [segmentServer.py](scripts/segmentServer.py) finds the boundary edges. Then the total surface is broken into segmented regions.

### 3. Graph Building

With a segmented region, [graphEstimation.py](scripts/graphEstimation.py) creates a graph $G = {V, E}$.

### 4. Shortest Tour

Given a graph, [some file](chinese) find the shortest route that visits all edges.

### 5. Path Planner

Given a waypoint tour, [rrtServer.py](scripts/rrtServer.py) creates a feasbile path between all way points.

### 6. Client

[pcl_pahap_client](src/pcl_pahap_client.cpp) kicks off the navigation algorithm by calling a bunch of ROS services. ****