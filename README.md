###### yolov8_ros2
https://github.com/mgonzs13/yolov8_ros
https://developer-lionhong.tistory.com/61

jetson@nano:~$ sudo sh -c 'echo 128 > /sys/devices/pwm-fan/target_pwm'
jetson@nano:~$ sudo apt install python3-pip
jetson@nano:~$ sudo -H pip3 install -U jetson-stats
jetson@nano:~$ jetson_release
Software part of jetson-stats 4.2.7 - (c) 2024, Raffaello Bonghi
Model: NVIDIA Jetson Nano Developer Kit - Jetpack 4.6 [L4T 32.6.1]
NV Power Mode[0]: MAXN
Serial Number: [XXX Show with: jetson_release -s XXX]
Hardware:
 - P-Number: p3448-0000
 - Module: NVIDIA Jetson Nano (4 GB ram)
Platform:
 - Distribution: Ubuntu 20.04 focal
 - Release: 4.9.253-tegra
jtop:
 - Version: 4.2.7
 - Service: Inactive
Libraries:
 - CUDA: 10.2.300
 - cuDNN: 8.2.1.32
 - TensorRT: 8.0.1.6
 - VPI: 1.1.15
 - Vulkan: 1.2.141
 - OpenCV: 4.6.0 - with CUDA: YES

jetson@nano:~/Downloads$  git clone -b galactic https://github.com/zeta0707/installROS2.git
Cloning into 'installROS2'...
remote: Enumerating objects: 20, done.
remote: Counting objects: 100% (20/20), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 20 (delta 8), reused 13 (delta 4), pack-reused 0
Unpacking objects: 100% (20/20), 1.62 MiB | 1.49 MiB/s, done.
jetson@nano:~/Downloads$ ls
installPiOLED  installROS2
jetson@nano:~/Downloads$ cd  installROS2
jetson@nano:~/Downloads/installROS2$ 
jetson@nano:~/Downloads/installROS2$ ./install-ros2.sh 
jetson@nano:~$ ls
Desktop    Downloads  Pictures  ros2_ws    Videos
Documents  Music      Public    Templates  yolo_ros


https://github.com/mgonzs13/yolov8_ros

jetson@nano:~$ cd ~/ros2_ws/src
jetson@nano:~/ros2_ws/src$ git clone https://github.com/mgonzs13/yolov8_ros.git
jetson@nano:~/ros2_ws/src$ pip3 install -r yolov8_ros/requirements.txt

original 
User
requirements.txt --->   
opencv-python==4.8.1.78
typing-extensions>=4.4.0
ultralytics==8.1.29 

modify--->
opencv-python==4.8.1.78
typing-extensions==3.7.4
ultralytics==8.1.29
tensorflow==2.4.1
pandas==2.0.3
numpy>=1.20.3  # 업그레이드된 numpy 버전
python-dateutil>=2.8.2

bravo  

result 
dist-packages (from pyasn1-modules>=0.2.1->google-auth<2,>=1.6.3->tensorboard~=2.4->tensorflow==2.4.1->-r yolov8_ros/requirements.txt (line 7)) (0.4.8)
Requirement already satisfied: oauthlib>=3.0.0 in /usr/lib/python3/dist-packages (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard~=2.4->tensorflow==2.4.1->-r yolov8_ros/requirements.txt (line 7)) (3.1.0)




 cd ~/ros2_ws
jetson@nano:~/ros2_ws$ rosdep install --from-paths src --ignore-src -r -y
WARNING: ROS_PYTHON_VERSION is unset. Defaulting to 3
ERROR: the following packages/stacks could not have their rosdep keys resolved
to system dependencies (ROS distro is not set. Make sure `ROS_DISTRO` environment variable is set, or use `--rosdistro` option to specify the distro, e.g. `--rosdistro indigo`):
yolov8_msgs: Cannot locate rosdep definition for [geometry_msgs]
yolov8_ros: Cannot locate rosdep definition for [sensor_msgs]
yolov8_bringup: Cannot locate rosdep definition for [ament_lint_common]
Continuing to install resolvable dependencies...
#All required rosdeps installed successfully

jetson@nano:~/ros2_ws$ ls /opt/ros/
galactic
jetson@nano:~/ros2_ws$ source /opt/ros/galactic/setup.bash

jetson@nano:~/ros2_ws$ colcon build
Starting >>> yolov8_ros
Starting >>> yolov8_msgs
Finished <<< yolov8_ros [7.49s]                                           
Starting >>> yolov8_bringup
Finished <<< yolov8_bringup [3.50s]                                  
[Processing: yolov8_msgs]                             
Finished <<< yolov8_msgs [1min 1s]                             

Summary: 3 packages finished [1min 2s]




ros2 launch yolov8_bringup yolov8.launch.py
jetson@nano:~/ros2_ws$ ros2 launch yolov8_bringup yolov8.launch.py
/opt/ros/galactic/bin/ros2:6: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import load_entry_point
Package 'yolov8_bringup' not found: "package 'yolov8_bringup' not found, searching: ['/opt/ros/galactic']"


jetson@nano:~/ros2_ws$ source ~/ros2_ws/install/setup.bash

jetson@nano:~/ros2_ws$ 
jetson@nano:~/ros2_ws$ ros2 launch yolov8_bringup yolov8.launch.py
/opt/ros/galactic/bin/ros2:6: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import load_entry_point
[INFO] [launch]: All log files can be found below /home/jetson/.ros/log/2024-03-25-10-12-58-175864-nano-32068
[INFO] [launch]: Default logging verbosity is set to INFO
[INFO] [yolov8_node-1]: process started with pid [32072]
[INFO] [tracking_node-2]: process started with pid [32074]
[INFO] [debug_node-3]: process started with pid [32076]


ros2 node list
jetson@nano:~/ros2_ws$ ros2 node list
/opt/ros/galactic/bin/ros2:6: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import load_entry_point
/yolo/debug_node
/yolo/tracking_node
/yolo/yolov8_node
!![Screenshot from 2024-03-25 10-17-37](https://github.com/jetsonmom/yolov8_ros2/assets/92077615/798a247b-f6f5-4926-843a-ca6656860568)
