# ROS - Robot Operating System

+ **Nodes**: A node is an executable that uses ROS to communicate with other nodes. 
+ **Messages**: ROS data type used when subscribing or publishing to a topic. 
+ **Topics**: Nodes can publish messages to a topic as well as subscribe to a topic to receive messages. 

## Build Packages in a catkin Workspace

With [`catkin_make`](http://wiki.ros.org/catkin/commands/catkin_make) called it in the top level of a catkin workspace the workspace is build. The install target is created with: 

``` shell
catkin_make install
```

Note that either the install space or the devel space should be used, but not both at the same time. A new package can be added to a previously compiled workspace with: 

```shell
catkin_make --force-cmake
```

### Configuring Packages

Example: Set a different installation prefix by using the CMake variable `CMAKE_INSTALL_PREFIX` like so: 

```shell
cd ~/tutorial_ws/build
cmake ../src -DCMAKE_INSTALL_PREFIX=../install -DCATKIN_DEVEL_PREFIX=../devel
```

### Cleaning up

Delete the buildspace and install space whenever you want, and re-create them using the steps above.

```shell
cd ~/tutorial_ws
rm build devel install
```

## Workspace setup

Create new workspace:

```shell
mkdir -p catkin_ws/src
cd catkin_ws
catkin_make
```

`catkin_make` sets up the workspace including `devel` folder and `CMakeLists.txt` file. 

Run setup file (useful to add it to `.bashrc`):

```shell
source devel/setup.bash
```

If necessary mark file as executable:

```shell
chmod +x devel/setup.bash
```

Check environment variable:

```shell
echo $ROS_PACKAGE_PATH
```

### Added to `.bashrc`

Load own workspace

```shell
source /opt/ros/kinetic/setup.bash
source /home/zf/ros/lidar_ws/devel/setup.bash
```

### Install ROS Plug-in for Qt Creator

https://ros-qtc-plugin.readthedocs.io/en/latest/_source/How-to-Install-Users.html#installation-procedure-for-ubuntu-16-04

### Run “Hello world” example

Add a new Basic Node to the `src` folder with QT Creator with “File/New File or Project.../ROS/Basic Node/...“ or add a new .cpp file by hand:

```c++
#include <ros/ros.h>

int main(int argc, char **argv)
{
  ros::init(argc, argv, "test");
  ros::NodeHandle nh;

  ROS_INFO("Hello world!");
}
```

Start `roscore` and run `.cpp` file:

```shell
cd ros/tutorial_ws
source devel/setup.bash
catkin_make
roscore 
rosrun trial HelloWorld
```

## Information / Error messages

+ **roscore** is a must have for ROS nodes to communicate (`roslaunch` automatically starts a `roscore` if not already running). `roscore` will start up:
  
  + a ROS Master
  + a ROS Parameter Server 
  + a rosout logging node
  
  `rosrun` does not automatically starts a `roscore`, if no roscore is started the following error appears:
  `[ERROR] [1578639160.606543864]: [registerPublisher] Failed to contact master at [localhost:11311].  Retrying...`