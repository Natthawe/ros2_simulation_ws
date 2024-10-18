# Dependencies
 - sudo apt install ros-$ROS_DISTRO-joint-state-publisher-gui
 - sudo apt install ros-$ROS_DISTRO-xacro
 - sudo apt install ros-$ROS_DISTRO-gazebo-ros-pkgs
 - sudo apt install ros-$ROS_DISTRO-robot-localization
 - sudo apt install ros-$ROS_DISTRO-rqt-robot-steering
 - 

# Add the Path of the Model to the Bashrc File
 - source /opt/ros/humble/setup.bash
 - export ROS_DOMAIN_ID=99
 - export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
 - export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/home/natthawe/ros2_simulation_ws/src/basic_mobile_robot/models/
 - export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/home/natthawe/ros2_simulation_ws/src/basic_mobile_robot/worlds/basic_mobile_bot_world/

# Gazebo
 - killall gazebo
 - killall gzserver
 - killall gzclient

# Launch file
 - ros2 launch basic_mobile_robot basic_mobile_bot_v1.launch.py (create URDF)
 - ros2 launch basic_mobile_robot basic_mobile_bot_v2.launch.py (spawn model on gazebo)
 - ros2 launch basic_mobile_robot basic_mobile_bot_v3.launch.py (robot_localization[IMU & Encoder wheel])
 - ros2 launch basic_mobile_robot basic_mobile_bot_v4.launch.py (setup LIDAR)
 - ros2 launch basic_mobile_robot basic_mobile_bot_v5.launch.py (slam & navigation)
 - ros2 launch basic_mobile_robot basic_mobile_bot_v5.launch.py -s (show Arguments)

# Command
 - ros2 run rqt_robot_steering rqt_robot_steering --force-discover (move robot)
 - ros2 run tf2_ros tf2_echo odom base_footprint (output transform)
 - ros2 node list
 - ros2 node info /ekf_filter_node
 - rqt_graph
 - ros2 run tf2_tools view_frames.py (save coordinate frames)
 - evince frames.pdf (view coordinate frames)

# Know How
 - Costmap_2d: [Costmap_2d_wiki](http://wiki.ros.org/costmap_2d) and [Costmap_2d_nav2](https://docs.nav2.org/configuration/packages/configuring-costmaps.html)
 - Global costmap: Costmap นี้ใช้ในการสร้างแผนระยะยาวสำหรับสภาพแวดล้อมทั้งหมด เช่น การคำนวณเส้นทางที่สั้นที่สุดจากจุด A ไปยังจุด B บนแผนที่
 - Local costmap: Costmap นี้ใช้เพื่อสร้างแผนระยะสั้นเหนือสภาพแวดล้อม เช่น เพื่อหลีกเลี่ยงอุปสรรค
 - ใช้อัลกอริทึม AMCL (Adaptive Monte Carlo Localization) เพื่อระบุตำแหน่งของหุ่นยนต์ในโลกและเผยแพร่การแปลงพิกัดจากแผนที่ ไปยัง เฟรม Odom
 - AMCL: ระบุตำแหน่งของหุ่นยนต์ในโลกโดยใช้การสแกน LIDAR โดยการจับคู่ข้อมูลการสแกนแบบเรียลไทม์กับแผนที่ที่รู้จัก [amcl_wiki](http://wiki.ros.org/amcl) [amcl_nav2](https://docs.nav2.org/configuration/packages/configuring-amcl.html)
