# vegebot
Repository for all Vegebot code
by Simon Birrell

Includes the following packages:
vegebot - The metapackage
vegebot_commander - Overall executive for Vegebot
vegebot_msgs - Definition of vegebot-specific messages for ROS topics.
vegebot_run - Startup scripts and robot URDFs
vegebot_webserver - Drives the Vegebot HTML UI.
lettuce_test - Various test scripts that simulate lettuces.

(c) Bio-inspired Robotics Laboratory, Cambridge University. 2017. All Rights Reserved.

INSTALLATION
============

1. Install ROS Kinetic
2. Create Catkin Workspace http://wiki.ros.org/catkin/Tutorials/create_a_workspace
3. Install vegebot software
```
cd ~/catkin_ws/src
git clone https://github.com/manacoa/vegebot
cd ~/catkin_ws
```
6. Install other packages
```
sudo apt-get install ros-kinetic-web-video-server ros-kinetic-ur10-moveit-config ros-kinetic-ur-gazebo ros-kinetic-rosbridge-server ros-kinetic-usb-cam ros-kinetic-tf2-web-republisher ros-kinetic-moveit ros-kinetic-universal-robot
``` 
7. Install ur_modern_driver for Universal Robots
```
cd ~/catkin_ws/src
git clone https://github.com/iron-ox/ur_modern_driver
cd ur_modern_driver
git checkout iron-kinetic-devel
```
8. catkin_make
```
cd ~/catkin_ws
catkin_make
```
9. Add commands to BASH shell
```
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
10. Set UR10 IP
- Set Up Robot > Set up Network
- IP 192.168.2.5
- Netmask 255.255.255.0
- Gateway 192.168.2.1
11. Set PC Ethernet IP to 192.168.2.10
- Check you can ping the robot
```
ping 192.168.2.5
```

12. Set up DeepLettuceDetctor (by Julia Cai)
- Generate libdarknet.so. You will need CUDA and CUDNN installed (good luck!).
````
roscd lettuce_detect
cd deep_lettuce_detector 
make
````
- Edit vegebot/lettuce_detect/deep_lettuce_detector/darknet.py to include path to libdarknet.so
- Download 6 files (2 x .weights, .data and .cfg) into lettuce_cfg
- For demo to check it-s working:
````
python2 deep_lettuce_detector.py
````
This should show you a video capture window and detected bounding boxes. Press any key to exit.

DEMO
====

REAL ROBOT

1. Connect to UR-10 via ethernet and check you can ping UR-10 at 192.168.2.5
2. On UR-10 touch screen, go to Program Robot > Move > Home and press Auto until robot in upright position
3. Leave the Home screen (important!)
4. In first terminal window do roslaunch vegebot_run run.launch
5. In second window do rosrun vegebot?commander vegebot_commander
6. Open browser to http://localhost:8000 Model should load.
7. Click Detect for fixed lettuces
8. Click Pick on any lettuce
9. Click Camera Image to read an image off disk and extract lettuces
10. Can use rosrun image_view image_view image:=/vegebot/lettuce_hypotheses/annotated_images to monitor image

SIMULATION

1. In first terminal window do roslaunch vegebot_run sim.launch
2. In second window do rosrun vegebot?commander vegebot_commander
3. Open browser to http://localhost:8000 Model should load.
4. Click Detect for fixed lettuces
5. Click Pick on any lettuce
6. Click Camera Image to read an image off disk and extract lettuces
7. Can use rosrun image_view image_view image:=/vegebot/lettuce_hypotheses/annotated_images to monitor image

