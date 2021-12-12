# Read Me Template

![Project Image](https://user-images.githubusercontent.com/43727159/145706210-607af6d7-92bc-446d-8a46-23e7bfc8c91c.png)

> I.	Project Description:
On our industrial project we are entrusted to discover the new Ros2 Foxy  using the robot tutelbot3. The Robot Operating System (ROS) is a set of software libraries and tools for creating robotic applications. From pilots to state-of-the-art algorithms, and with powerful development tools, ROS has what you need for your next robotics project. And everything is open source.
Since the launch of ROS in 2007, a lot has changed in the robotics and ROS community. The aim of the ROS 2 project is to adapt to these changes, taking advantage of the benefits of ROS 1 and improving what is not.


---

### Table of Contents
You're sections headers will be used to reference location of destination.

- [WHY ROS2](#WHY-ROS2)
- [The basic command in ROS2](##the-basic-commands-ros2-short-"tutorial":)
- [The Project: TurtleBot 3](#Project:-TurtleBot-3)
- [Control the robot with the keyboard](#To-Control-the-robot-with-thekeyboard)
- [Run The SLAM](#Run-the-SLAM-node:)
- [Launch the camera](#To-launch-the-camera:)
- [Author Info](#author-info)
- [Special THANKS](#special-THANKS:)

---

## WHY ROS2

### 1.	The question is answered by Going back: what is ROS?
Robot Operating System (ROS) is a set of open source software libraries and tools that help you build robotic applications. From pilots to state-of-the-art algorithms to powerful development tools, ROS to what you need for your next robotics project.
The ROS environment was developed by Willow Garage for its PR2 robot, a humanoid robot capable of autonomously navigating a known environment.
At that time, its creators knew that PR2 would not be the only robot on the market. Rather than developing a specific program for PR2, they deviated from implementing generalist and adaptable software so that they could improve or modify it later. So they worked on a middleware, ROS, by defining levels of abstraction that could be used on other robots.
They based this on some of the characteristics of the PR2 robot:
 •	One robot
•	No real-time requirements
•	Excellent network connectivity
•	Maximum flexibility (works on mobile bases as well as on humanoids for example)

Today, ROS is used not only on PR2 robots and similar robots, but also on mobile robots of all sizes, humanoids, industrial arms, outdoor ground vehicles and aerial vehicles.



#### 2.	Changements between ROS 1 and ROS 2
#### 1)	Foreword:
Each change is described as briefly as possible, but giving sufficient context and justification for a reader familiar with ROS 1. If other external information is available (e.g. other articles), it must be linked.
Platforms and dependencies
#### 2)	Platforms:
ROS 1 is only tested by CI on Ubuntu. It is actively supported by the community on other versions of Linux as well as on OS X.
ROS 2 is currently tested by CI and supported on Ubuntu Xenial, OS X El Capitan as well as Windows 10
#### 3)	Languages
#####	C++ Standard
The core of ROS 1 targets C++03 and does not use the features of C++11 in its API. ROS 2 uses C++11 extensively and uses parts of C++14. In the future, ROS 2 could start using C++17 as long as it is supported on all major platforms.

#####	Python
ROS 1 targets Python 2. ROS 2 requires at least Python version 3.5.

#### 3.	Reuse existing middle ware
ROS 1 uses a custom serialization format, a custom transport protocol, and a custom central discovery mechanism. ROS 2 has an abstract middleware interface, through which serialization, transport, and discovery are provided. Currently, all implementations of this interface are based on the DDS standard. This allows ROS 2 to provide various quality of service policies that improve communication across different networks.

## Setting up your ROS 2 environment
#### 1.	Source installation files
You will need to run this command on each new shell you open to access ROS 2 commands, like this:
```bash
$ source /opt/ros/foxy/setup.bash
```

Add sourcing to your shell startup script
If you don't want to have to search for the installation file every time you open a new shell (by skipping task 1), you can add the command to your shell startup script:
```bash
$ echo "source /opt/ros/foxy/setup.bash" >> ~/.bashrc
```
#### 2.	Check environment variables
Provisioning the ROS 2 installation files will define several environment variables necessary for ROS 2 to work. If you have problems finding or using your ROS 2 packages, make sure that your environment is configured correctly by using the following command:
```bash
$ printenv | grep -i ROS
You must have seen this:
ROS_VERSION=2
ROS_PYTHON_VERSION=3
ROS_DISTRO=foxy
```
#### 3.	The notion of nodes:
##### The ROS 2 graph
The ROS graph is a network of ROS 2 elements processing data together at the same time. It encompasses all executables and the connections between them if you had to map and visualize them all.
##### Nodes in ROS 2
Each node in ROS must be responsible for a single module objective (for example, a node to control wheel motors, a node to control a laser rangefinder, etc.). Each node can send and receive data to other nodes through topics, services, actions, or settings. Here is an image that explains the nodes well:

![Nodes-TopicandService](https://user-images.githubusercontent.com/43727159/145708317-5e4684bb-5a8c-4d79-a87b-1a3d35fd9582.gif)

A complete robotic system is made up of many nodes working together. In ROS 2, the same executable (C++ program, Python program, etc.) can contain one or more nodes.
[Back To The Top](#read-me-template)

---

## 	The basic  commands ROS2 short "Tutorial":

#### 1)	Ros2 run


The commande launches an executable from a "ros2 run" package
```` bash
$ ros2 run<package_name><executable_name>
```` 
Example:
```` bash
$ ros2 run turtlesim turtlesim_node
````
Once the turtlesim is launched in can see the nodes activated by the command:
```` bash
$ ros2 node  list
````
You see:
```` bash
/turtlesim
````
#### 2)	Node informationros2  
Now that you know the names of your nodes, you can access more information about them with:
```` bash
$ ros2 node info<node_name>
````
Example:
```` bash
$ ros2 node info  /my_turtle
````
You had to see:
```` bash
/my_turtle
  Subscribers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /turtle1/cmd_vel: geometry_msgs/msg/Twist
  Publishers:
    /parameter_events: rcl_interfaces/msg/ParameterEvent
    /rosout: rcl_interfaces/msg/Log
    /turtle1/color_sensor: turtlesim/msg/Color
    /turtle1/pose: turtlesim/msg/Pose
  Services:
    /clear: std_srvs/srv/Empty
    /kill: turtlesim/srv/Kill
    /reset: std_srvs/srv/Empty
    /spawn: turtlesim/srv/Spawn
    /turtle1/set_pen: turtlesim/srv/SetPen
    /turtle1/teleport_absolute: turtlesim/srv/TeleportAbsolute
    /turtle1/teleport_relative: turtlesim/srv/TeleportRelative
    /my_turtle/describe_parameters: rcl_interfaces/srv/DescribeParameters
    /my_turtle/get_parameter_types: rcl_interfaces/srv/GetParameterTypes
    /my_turtle/get_parameters: rcl_interfaces/srv/GetParameters
    /my_turtle/list_parameters: rcl_interfaces/srv/ListParameters
    /my_turtle/set_parameters: rcl_interfaces/srv/SetParameters
    /my_turtle/set_parameters_atomically: rcl_interfaces/srv/SetParametersAtomically
  Action Servers:
    /turtle1/rotate_absolute: turtlesim/action/RotateAbsolute
Customer Action:
````
#### 3)	Ros2 Subject Echo
To see published data on a topic, use:
```` bash
$ ros2  topic echo<topic_name>
````
Example:
```` bash
$ ros2 topic echo /turtle1/cmd_vel
````
You must have seen this:
```` bash
linear:
  x: 2.0
  y: 0.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 0.0
  ---
````

#### 4)	Creatinga  workspace
First, source your installation: 
```` bash
$ source /opt/ros/foxy/setup.bash
````
Let's use the workspace you created in the previous tutorial, for example by wanting to create our  workspace  under the  name  "dev_ws",  for yournew package. 
```` bash
$ubuntu@ubuntu:~$ mkdir dev_ws
$ubuntu@ubuntu:~$  cd  dev_ws/
$ubuntu@ubuntu:~/dev_ws$  mkdir  src
$ubuntu@ubuntu:~$  colcon  build
$ ubuntu@ubuntu:~$ ls
````
Normally you had to find 3 folders:
- Devel/ Build/ Src/		

#### 5)	Creating a package
Make sure that you are in the src folder before you run the package creation command:
```` bash
$ cd ~/dev_ws/src
````
The syntax of the command to create a new package in ROS 2 is:
```` bash
$ ros2 pkg create --build-type ament_cmake<package_name>
````
You will use the optional --node-name argument that creates a simple executable of type Hello World in the package. Enter the following command in your terminal:
```` bash
$ ros2 pkg create --build-type ament_cmake --node-name my_node my_package
````
You will now have a new folder in your workspace directory my_package. To compile your  package  back to  your  workspace.
```` bash
$ cd ~/dev_ws/
$ colcon build
````
You can use this command to compile that the package select:
```` bash
$ colcon build --packages-select my_package
````
After source after each installation:
```` bash
$ source /opt/ros/foxy/setup.bash
````
You can usethe same to download a package from GitHub.
```` bash
$ cd ~/dev_ws/src/
````
```` bash
$sudo git clone  https://github.com/votre-package/
````
Becareful,  sometimes  you want to install a package in another branch  different from that of master, for this you have to add the branch name !!!
```` bash
$ sudo git clone  -b  foxy  https://github.com/votre-package/
````
If for example the branch is foxy😉

[Back To The Top](#read-me-template)

---
#	Project: TurtleBot 3
### 1) Workstation:
At first we installed Ubuntu 20.04 LTS Desktop image (64-bit) on our tower station the download link: https://releases.ubuntu.com/20.04/
```` bash
esirem as user
napelturbot as password 
The IP address is  192.168.0.100
````
##### Installing ros2 foxy:
After we installed ubuntu 20.04 LTS on our Desktop (Tower), now we will install Ros2 packages on tour, we put:
```` bash
$ wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros2_foxy.sh
$ sudo chmod 755 ./install_ros2_foxy.sh
$ bash ./install_ros2_foxy.sh
````
##### Install Dependent ROS 2 Packages:

We install simulation packages like gazebo11 and map  navigation2
To install Gazebo11 on the terminal of the tower we type:
```` bash
 $ sudo apt-get install ros-foxy-gazebo-*
````
To install Cartographer,on the terminal of the tower we type:
```` bash
 $ sudo apt install ros-foxy-cartographer
 $ sudo apt install ros-foxy-cartographer-ros
````
To install Navigation2, on the terminal of the tower we type:
```` bash
 $ sudo apt install ros-foxy-navigation2
 $ sudo apt install ros-foxy-nav2-bringup
````
Finally we install TurleBot3 via Debian packages:
```` bash
$ source ~/.bashrc
$ sudo apt install ros-foxy-dynamixel-sdk
$ sudo apt install ros-foxy-turtlebot3-msgs
$ sudo apt install ros-foxy-turtlebot3
````
At the end we add everything we have installed to the ros environment variables for the PC (TOWER)
```` bash
 $ echo 'export ROS_DOMAIN_ID=30 #TURTLEBOT3' >> ~/.bashrc
$ source ~/.bashrc
````
#### Note well!!
If you installed TurtleBot  via Debian packages by  apt  install  command, you can ignore the warning message:
```` bash
 bash: /home/{$YOUR_ACCOUNT}/turtlebot3_ws/install/setup.bash: No such file or directory
 ````
### 2) Preparation of the Raspberry Pi of the Turtlebot3:

To install the Ros2 on the raspberry  pi:  Prepare a  microSD card and insert it into the computer.
Download first: Ros2 foxy  image:  https://www.robotis.com/service/download.php?no=2064  if  Raspberry pi 4B
Or https://www.robotis.com/service/download.php?no=2058  if Raspberry pi 3B+
Then download Raspberry Pi  imager:  https://www.raspberrypi.org/software/ this software allows you to flash the sd  card  with  foxy that we have  installed.
![rpi_imager](https://user-images.githubusercontent.com/43727159/145709307-746c21fc-80fe-48e4-b6dd-50c4bea49fe4.gif)

Then look for the "Disk" and launch the application:
•	Search for "Disks" and select the microSD card in the left panel.
•	Select the "Restore Disk Image" option.
•	Open the . img  from the local disk.
•	Click Start Restoring... > Restore button. Launch the app
After resize the partition according to your preference.

After installing the Ros2 packages on the  Raspberry Pi, we put :
````bash
ubuntu as user
Turtlebot ace Password
The IP address is  192.168.0. 200
````
Configure WiFi network settings:
This part is very important because we will  configurerla card with thenetwork,  for this  "we have configured a  TP-Link router with the  university network  to be easier  to connect".
Open a terminal and access this directory:
````bash
cd /media/$USER/writable/etc/netplan
sudo nano 50-cloud-init.yaml
````
##### Pay attention to the spaces and Tabs !!!
![network_setup](https://user-images.githubusercontent.com/43727159/145709427-38a40055-bccd-4a78-8937-19c25da311bf.gif)

##### Check our file "50-cloud-init.yaml" in github files 
##### Careful:
"Dhcp-identifier:  mac": The built-in network configuration of Ubuntu 18.04 and above no longer uses the Mac address of the network adapter as the default identifier for DHCP requests.
In ROS2 DDS communication, ROS_DOMAIN_ID must match between the remote PC and TurtleBot3 for communication in the same network environment.
The default ROS domain ID for TurtleBot3 is set to 30 in the file. bashrc.
On the terminal type:
````bash
$ubuntu@ubuntu:~$ sudo nano .bashrc
$ROS_DOMAIN_ID=30 #TURTLEBOT3
````
Please change the ID to avoid conflicts when there are identical IDs in the same network.


#### 3) Configuration OpenCR
OpenCR1.0 is developed for ROS embedded systems to provide fully open source hardware and software.
All about the board of directors; Schematics, Gerber PCBs, BOMs and firmware source code for TurtleBot3 and OP3 are free to distribute under open source licenses for users and the ROS community.
The STM32F7 series chip inside the OpenCR1.0 board is based on a very powerful ARM Cortex-M7 with a floating-point unit.
The development environment for OpenCR1.0 is wide open from the Arduino ide and Scratch for young students to traditional firmware development for the expert.
![image](https://user-images.githubusercontent.com/43727159/145709582-d3300d61-c548-4288-aa6b-f522d628206b.png)
The difference between a firmware and an OS:
To make it simpler:
The Operating System (OS) is a set of programs  that directs the use of the capabilities of a computing device by application software. Contains the kernel, a graphical user interface (GUI), or at least a command line interface (CLI) that uses hardware for file management.
The Kernel ispart of the operating system software, the doorman and translator between the operating system and the hardware.

In other words (on Wikipedia), the main function of the kernel is to facilitate access to computer resources:
•	CPU
•	RAM
•	I/O
The Firmware par  definition,is  a firmware is any instruction stored in the ROM.
Firmware is a play on words between software and hardware, referring to the spectrum for "ease of modification".
The firmware is independent of the operating system _ {an exception that blurs the lines} _ when the entire operating system is stored in the ROM memory, therefore, by definition, considered firmware
Firmware is the minimum instruction for orchestrating multiple general-purpose hardware components.
Once we understand the difference  between these two so we start by connectez OpenCR to Rasbperry Pi using the micro USB cable,andinstaller the packages required on the Raspberry Pi to download the OpenCR firmware.
On the terminal:
````bash
$ sudo  dpkg  --add-architecture  armhf
$ sudo  apt update
$ sudo  apt  install  libc6:armhf
````
Depending on the platform, use either "burger" or "waffle" for the name OPENCR_MODEL in our case it is burger :
````bash
$ export  OPENCR_PORT=/dev/ttyACM0
$ export  OPENCR_MODEL=burger
$ rm  -rf  ./opencr_update.tar.bz2
And tdownload the firmware and charger and then extract the file.
$ wget https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS2/latest/opencr_update.tar.bz2
$ tar  -xjf  ./opencr_update.tar.bz2
````
Then wedownload the firmware on the OpenCR.
````bash
$ cd  ~/opencr_update
$./update.sh  $OPENCR_PORT $OPENCR_MODEL.opencr
````
A successful firmware download for TurtleBot3 Burger will look like below
![shell01](https://user-images.githubusercontent.com/43727159/145709638-b009888a-91e1-419f-874a-031c9c7adc65.png)

If the firmware downloadfails, try downloading with the recovery mode. The sequence below enables OpenCR recovery mode. In recovery mode, the OpenCR STATUS LED  will flash periodically:  
 •	Hold down the PUSH SW2 button.
 •	Press the Reset button.
•	Release the Reset button.
•	Release the PUSH SW2 button.
![image](https://user-images.githubusercontent.com/43727159/145709713-7a12adb3-553c-4be8-9a28-7e5fc9a6e4ea.png)
#### Hardwar assembly:
![image](https://user-images.githubusercontent.com/43727159/145709735-659cdc9b-e55b-4c2f-b02a-af092858e19a.png)

Here's a tutorial: https://www.youtube.com/watch?v=rvm-m2ogrLA&ab_channel=ROBOTISOpenSourceTeam

[Back To The Top](#read-me-template)
### Now Let TURN ON OUR ROBOT !! 😊 
Operate the Turtelbot3:
Open a terminal in the pc "workstation" and try to connect to the turtlebot  by an  ssh:
ssh ubuntu@{IP_ADDRESS_OF_RASPBERRY_PI}
````bash
$esirem@esirem-Precision-3630-Tower:~$ ssh  ubuntu@192.168.0.200  -p22
````
By default the robot's passeword is:  turtlebot
Then to affile the basicpackages  and start the TurtleBot3 applications.
````bash
$ export  TURTLEBOT3_MODEL=burger
$ ros2 launch turtlebot3_bringup robot.launch.py
````
Normally you should have something like  this: 
````bash
[INFO] [launch]: All log files can be found below /home/ubuntu/.ros/log/2019-08-19-01-24-19-009803-ubuntu-15310
[INFO] [launch]: Default logging verbosity is  set  to INFO
urdf_file_name: turtlebot3_burger.urdf
[INFO] [robot_state_publisher-1]: process started with pid  [15320]
[INFO] [hlds_laser_publisher-2]: process started with pid  [15321]
[INFO] [turtlebot3_ros-3]: process started with pid  [15322]
[robot_state_publisher-1] Initialize urdf model from file: /home/ubuntu/turtlebot_ws/install/turtlebot3_description/share/turtlebot3_description/urdf/turtlebot3_burger.urdf
[robot_state_publisher-1] Parsing robot urdf xml string.
[robot_state_publisher-1] Link base_link had 5 children
[robot_state_publisher-1] Link caster_back_link had 0 children
[robot_state_publisher-1] Link imu_link had 0 children
[robot_state_publisher-1] Link base_scan had 0 children
[robot_state_publisher-1] Link wheel_left_link had 0 children
[robot_state_publisher-1] Link wheel_right_link had 0 children
[robot_state_publisher-1] got segment base_footprint
[robot_state_publisher-1] got segment base_link
[robot_state_publisher-1] got segment base_scan
[robot_state_publisher-1] got segment caster_back_link
[robot_state_publisher-1] got segment imu_link
[robot_state_publisher-1] got segment wheel_left_link
[robot_state_publisher-1] got segment wheel_right_link
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Init TurtleBot3 Node Main
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Init DynamixelSDKWrapper
[turtlebot3_ros-3] [INFO]  [DynamixelSDKWrapper]: Succeeded to open the port(/dev/ttyACM0)!
[turtlebot3_ros-3] [INFO]  [DynamixelSDKWrapper]: Succeeded to change the baudrate!
[robot_state_publisher-1] Adding fixed segment from base_footprint to base_link
[robot_state_publisher-1] Adding fixed segment from base_link to caster_back_link
[robot_state_publisher-1] Adding fixed segment from base_link to imu_link
[robot_state_publisher-1] Adding fixed segment from base_link to base_scan
[robot_state_publisher-1] Adding moving segment from base_link to wheel_left_link
[robot_state_publisher-1] Adding moving segment from base_link to wheel_right_link
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Start Calibration of Gyro
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Calibration End
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Add Motors
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Add Wheels
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Add Sensors
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Succeeded to create battery state publisher
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Succeeded to create imu publisher
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Succeeded to create sensor state publisher
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Succeeded to create joint state publisher
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Add Devices
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Succeeded to create motor power server
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Succeeded to create reset server
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Succeeded to create sound server
[turtlebot3_ros-3] [INFO]  [turtlebot3_node]: Run!
[turtlebot3_ros-3] [INFO]  [diff_drive_controller]: Init Odometry
[turtlebot3_ros-3] [INFO]  [diff_drive_controller]: Run!
````
Open another terminal: without making the connection  with the  sshagain, topics and services can be listed with the commands below.
````bash
$ ros2 topic list
/battery_state
/cmd_vel
/imu
/joint_states
/magnetic_field
/odom
/parameter_events
/robot_description
/rosout
/scan
/sensor_state
/tf
````
#### List of services:

````bash
$ ros2 service list
/diff_drive_controller/describe_parameters
/diff_drive_controller/get_parameter_types
/diff_drive_controller/get_parameters
/diff_drive_controller/list_parameters
/diff_drive_controller/set_parameters
/diff_drive_controller/set_parameters_atomically
/hlds_laser_publisher/describe_parameters
/hlds_laser_publisher/get_parameter_types
/hlds_laser_publisher/get_parameters
/hlds_laser_publisher/list_parameters
/hlds_laser_publisher/set_parameters
/hlds_laser_publisher/set_parameters_atomically
/launch_ros/describe_parameters
/launch_ros/get_parameter_types
/launch_ros/get_parameters
/launch_ros/list_parameters
/launch_ros/set_parameters
/launch_ros/set_parameters_atomically
/motor_power
/reset
/sound
/turtlebot3_node/describe_parameters
/turtlebot3_node/get_parameter_types
/turtlebot3_node/get_parameters
/turtlebot3_node/list_parameters
/turtlebot3_node/set_parameters
/turtlebot3_node/set_parameters_atomically
````
#### To Control the robot with thekeyboard

1-	Open a terminal in the pc then tryto connect to the robot with the  ssh  and launch turtlebot3_bringup robot.launch.py without forgetting the export  = burger
````bash
$ ssh ubuntu@192.168.0.200
$ export  TURTLEBOT3_MODEL=burger
$ ros2 launch turtlebot3_bringup robot.launch.py
````
2-	Open another terminal in the pc but this time stay in the pc and type:
````bash
$ export  TURTLEBOT3_MODEL=burger
$ ros2 run turtlebot3_teleop teleop_keyboard
````
If the node is successfully  launched, the following statement will appear in the terminal window.
````bash
Control Your Turtlebot3
Moving around
     w
 a   s    d
     x
w/x : increase/decrease linear velocity (Burger : ~ 0.22, Waffle and Waffle Pi : ~ 0.26)
a/d: increase/decrease angular velocity (Burger: ~ 2.84, Waffle and Waffle Pi : ~ 1.82)
space key, s: force stop
CTRL-C to quit
````
#### Run the SLAM node:
Open another terminal in  the pc then try to connect to the robot with the  ssh and launch:
````bash
$ ssh ubuntu@192.168.0.200
$ export  TURTLEBOT3_MODEL=burger
$ ros2 launch turtlebot3_bringup robot.launch.py
````
Open another terminal and stay on the tower:
````bash
$ export  TURTLEBOT3_MODEL=burger
$ ros2 launch turtlebot3_cartographer cartographer.launch.py
````
Once the SLAM node is successfully operational, TurtleBot3 will explore an unknown area of the map using teleoperation. It is important to avoid vigorous movements such as too rapid change in linear and angular velocity. When creating a map using the TurtleBot3, it is recom-mended to scan every corner of the map.

Open a new terminal and run the remote operation node from the tower:
````bash
$ export  TURTLEBOT3_MODEL=burger
$ ros2 run turtlebot3_teleop teleop_keyboard
````
````bash
Control Your TurtleBot3!
---------------------------
Moving around:
       w
   a   s   d
       x

w/x: increase/decrease linear velocity
a/d: increase/decrease angular velocity
space key, s: force stop

CTRL-C to quit
````
 Normally RVIZ2 will launch, and start exploring and drawing your map.
 
 ![image](https://user-images.githubusercontent.com/43727159/145710236-89b322ce-9029-4c9f-a8e4-f3caea94117d.png)
Once you have finished the mapping you can save your  map by the command:
````bash
$ ros2 run nav2_map_server map_saver_cli  -f  ~/map
````
Launch the map_saver_cli node in the nav2_map_server package to create map files.
The map file is saved in the directory where the map_saver_cli node is launched.
Unless a specific file name is provided, map will be used as the default file name and create map.pgm and map.yaml.
Thee "-f"   option specifies a folder location and file name where the files should be saved.  
With the above command, map.pgm and map.yaml will be saved in the home folder ~/(/home/esirem)

### To launch the camera:
All of abord it is necessary to check if it is activated,  andto check  this:  
````bash
$ ssh  ubuntu@192.168.0.200
$ubuntu@ubuntu:~$  sudo nano /etc/firmware/boot:config.txt
````
You should see something like  this,if the values are  different you have to change them: 
````bash
## Add the following lines to the end of /boot/firmware/config.txt file 
# RS - Activate Camera
start_x=1
# RS – Set GPU memory to 128 MB
gpu_mem=128
disable_camera_led=1
````


Now we will try to take a capture  to make sure that our camera works well:
````bash
$ubuntu@ubuntu:~$  sudo raspistill -o image.jpg
$ubuntu@ubuntu:~$  ls
````
Normalement you deviez find your image.jpg in the /home,  if you do not find it know that the camera of your robot is poorly  connected.
Now we will send the image on the tower to be able to display it:
````bash
$ubuntu@ubuntu:~$  scp . /image.jpeg esirem@192.168.0.100:~/
````
If you enter your workspace  (home/) you will  find  the image of your screenshot.

Since we are assured that our camera works well, now installs the packages of our cam to be able to launch it under ros2 permanently in order to visualize the path of our robot.
#### if you install my Project normally you don't need this following command!!!
On the terminal of our tour: 
````bash
$esirem@esirem-Precision-3630-Tower:~$ cd turtlebot_ws/src
$esirem@esirem-Precision-3630-Tower:~/turtlebot_ws/src$git  clone  https://gitlab.com/boldhearts/ros2_v4l2_camera
$esirem@esirem-Precision-3630-Tower:~/turtlebot_ws/src$cd..  
$esirem@esirem-Precision-3630-Tower:~/turtlebot_ws$colcon  build --symlink-install
$esirem@esirem-Precision-3630-Tower:~/turtlebot_ws$ source devel/setup.bash
$esirem@esirem-Precision-3630-Tower:~/turtlebot_ws$ cd src
$esirem@esirem-Precision-3630-Tower:~/turtlebot_ws/src$ git clone  https://github.com/ros2-gbp/rqt_image_view-release.git
$esirem@esirem-Precision-3630-Tower:~/turtlebot_ws/src$ cd ..
$esirem@esirem-Precision-3630-Tower:~/turtlebot_ws$colcon  build --symlink-install
$esirem@esirem-Precision-3630-Tower:~/turtlebot_ws$ source devel/setup.bash
````
We installed the packages of our camera as well as the software rqt_image_view which facilitates the display of the camera.
To launch the robot with the camera:  Open another terminal fromthetower,  then try to  connect to  the robot with the  ssh  and launch:
````bash
$esirem@esirem-Precision-3630-Tower:~$  ssh ubuntu@192.168.0.200
$ubuntu@ubuntu:~$  export  TURTLEBOT3_MODEL=burger
$ubuntu@ubuntu:~$  ros2 launch turtlebot3_bringup robot.launch.py
````

Launch a terminal in the tower:
````bash
$esirem@esirem-Precision-3630-Tower:~$  ros2 run v4l2_camera v4l2_camera_node
$esirem@esirem-Precision-3630-Tower:~$  ros2 run rqt_image_view rqt_image_view
````
---
## Files to download:

[Back To The Top](#read-me-template)

---

## Author Info
- Mail: Mehdi_Hahou@etu.u-bourgogne.fr
- Twitter - [@Mehdi_Hahou](https://twitter.com/zaara_gaara)
- LinkedIN - [@Mehd HAHOU](https://www.linkedin.com/in/mehdi-hahou-170b161a3/)


---
## Special THANKS:

It is my pleasure to announce that we have successfully completed the Turtlebot3 project in Ros2.
Special thanks go out to:
- Robotis 
- Mr Joaquin Jorge Rodriguez
- Mr Ralph Seulin
- Mr Raphael Duverne
- Mr Renato Martins
---
[Back To The Top](#read-me-template)
