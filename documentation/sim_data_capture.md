# Sim Data Capture Procedure
This document details the procedure involved with capturing simulated Turtlebot3 data in a rosbag and playing it back for offline algorithm development.

## Steps
1.  Launch a simulation environment. For example,
    ```
    roslaunch turtlebot3_gazebo turtlebot3_world.launch
    ```

2.  Launch the teleopkey
    ```
    roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
    ```

3.  Start recording the topic data. See [rosbag/Commandline](http://wiki.ros.org/rosbag/Commandline) for more options
    ```
    rosbag record <topic-names> -o <output-file-prefix> --duration=<duration>
    ```
    Specifically,
    ```
    rosbag record /imu /cmd_vel /odom /joint_states /gazebo/link_states -o sensor_data_1 --duration=10
    ```
4.  Use the teleop key to move the tbot for the duration.
5.  Stop recording the topic data (this should happen automatically if the duration was set).

## Reading Bag Data
Assuming all pip files were installed from the requirements.txt, the necessary packages should be installed.
The following resources may be useful to learn more about manipulating bag data:
-   [rosbag Wiki](http://wiki.ros.org/rosbag)
-   [rosbag/Code API](http://wiki.ros.org/rosbag/Code%20API#Python_API)
-   [rosbag Cookbook](http://wiki.ros.org/rosbag/Cookbook#Get_summary_information_about_a_bag)

## Message Info
### IMU
```
std_msgs/Header header
  uint32 seq
  time stamp
  string frame_id
geometry_msgs/Quaternion orientation
  float64 x
  float64 y
  float64 z
  float64 w
float64[9] orientation_covariance
geometry_msgs/Vector3 angular_velocity
  float64 x
  float64 y
  float64 z
float64[9] angular_velocity_covariance
geometry_msgs/Vector3 linear_acceleration
  float64 x
  float64 y
  float64 z
float64[9] linear_acceleration_covariance
```
Sample output:
```
header: 
  seq: 128
  stamp: 
    secs: 90
    nsecs: 341000000
  frame_id: "base_footprint"
orientation: 
  x: -1.92326368639e-06
  y: 0.00158965015562
  z: 0.000164566763104
  w: 0.999998722962
orientation_covariance: [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]
angular_velocity: 
  x: -4.90031077299e-05
  y: -0.000211230595713
  z: 7.95020430605e-06
angular_velocity_covariance: [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]
linear_acceleration: 
  x: 9.91277317355e-11
  y: 3.08923563409e-10
  z: 8.2810229904e-12
linear_acceleration_covariance: [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]
```

### Odom

```
std_msgs/Header header
  uint32 seq
  time stamp
  string frame_id
string child_frame_id
geometry_msgs/PoseWithCovariance pose
  geometry_msgs/Pose pose
    geometry_msgs/Point position
      float64 x
      float64 y
      float64 z
    geometry_msgs/Quaternion orientation
      float64 x
      float64 y
      float64 z
      float64 w
  float64[36] covariance
geometry_msgs/TwistWithCovariance twist
  geometry_msgs/Twist twist
    geometry_msgs/Vector3 linear
      float64 x
      float64 y
      float64 z
    geometry_msgs/Vector3 angular
      float64 x
      float64 y
      float64 z
  float64[36] covariance
```
Sample output:
```
header: 
  seq: 5665
  stamp: 
    secs: 189
    nsecs:  38000000
  frame_id: "odom"
child_frame_id: "base_footprint"
pose: 
  pose: 
    position: 
      x: -1.9999652019
      y: -0.499889716629
      z: -0.00100739918419
    orientation: 
      x: -2.21113307706e-06
      y: 0.00158964985915
      z: 0.000345721407832
      w: 0.999998676742
  covariance: [1e-05, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1e-05, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1000000000000.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1000000000000.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1000000000000.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.001]
twist: 
  twist: 
    linear: 
      x: 6.57853034128e-07
      y: 1.2331220169e-06
      z: 0.0
    angular: 
      x: 0.0
      y: 0.0
      z: 7.98269956836e-06
  covariance: [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]
```

### Command Velocity
```
geometry_msgs/Vector3 linear
  float64 x
  float64 y
  float64 z
geometry_msgs/Vector3 angular
  float64 x
  float64 y
  float64 z
```
Sample output:
```
linear: 
  x: 0.01
  y: 0.0
  z: 0.0
angular: 
  x: 0.0
  y: 0.0
  z: 0.0
```

### Joint States
```
std_msgs/Header header
  uint32 seq
  time stamp
  string frame_id
string[] name
float64[] position
float64[] velocity
float64[] effort
```
Sample output:
```
header: 
  seq: 15045
  stamp: 
    secs: 501
    nsecs: 705000000
  frame_id: ''
name: [wheel_right_joint, wheel_left_joint]
position: [12.931774845503746, 12.897883498119779]
velocity: []
effort: []
```

### Gazebo Link States
```
string[] name
geometry_msgs/Pose[] pose
  geometry_msgs/Point position
    float64 x
    float64 y
    float64 z
  geometry_msgs/Quaternion orientation
    float64 x
    float64 y
    float64 z
    float64 w
geometry_msgs/Twist[] twist
  geometry_msgs/Vector3 linear
    float64 x
    float64 y
    float64 z
  geometry_msgs/Vector3 angular
    float64 x
    float64 y
    float64 z
```
Sample output:
```
name: ['ground_plane::link', 'ros_symbol::symbol', 'turtlebot3_waffle::base_footprint',
  'turtlebot3_waffle::wheel_left_link', 'turtlebot3_waffle::wheel_right_link']
pose: 
  - 
    position: 
      x: 0.0
      y: 0.0
      z: 0.0
    orientation: 
      x: 0.0
      y: 0.0
      z: 0.0
      w: 1.0
  - 
    position: 
      x: 0.0
      y: 0.0
      z: 0.0
    orientation: 
      x: 0.0
      y: 0.0
      z: 0.0
      w: 1.0
  - 
    position: 
      x: -1.56979293734
      y: -0.498052554154
      z: -0.0010077358079
    orientation: 
      x: -7.5751279242e-06
      y: 0.0015906725702
      z: 0.00364193351871
      w: 0.999992102981
  - 
    position: 
      x: -1.57073753996
      y: -0.354055652347
      z: 0.0319924084177
    orientation: 
      x: -0.673392477388
      y: 0.214821631711
      z: 0.219890934549
      w: 0.672340847226
  - 
    position: 
      x: -1.56863980831
      y: -0.642048020418
      z: 0.0319934240268
    orientation: 
      x: -0.669127606889
      y: 0.227759081109
      z: 0.232807027517
      w: 0.667978244114
twist: 
  - 
    linear: 
      x: 0.0
      y: 0.0
      z: 0.0
    angular: 
      x: 0.0
      y: 0.0
      z: 0.0
  - 
    linear: 
      x: 0.0
      y: 0.0
      z: 0.0
    angular: 
      x: 0.0
      y: 0.0
      z: 0.0
  - 
    linear: 
      x: 0.00023715881247
      y: 2.70948368923e-06
      z: 3.39457299989e-05
    angular: 
      x: 5.63567244756e-06
      y: -0.000166062875413
      z: 1.6688500425e-05
  - 
    linear: 
      x: 0.00023230104822
      y: 1.76385642241e-06
      z: 3.30422317594e-05
    angular: 
      x: -4.34498921364e-05
      y: 0.00619897118403
      z: 3.0017776646e-05
  - 
    linear: 
      x: 0.000236800272014
      y: 1.8056318801e-06
      z: 3.17538729379e-05
    angular: 
      x: -4.44224220866e-05
      y: 0.00629932119113
      z: 2.93492093352e-05
```
