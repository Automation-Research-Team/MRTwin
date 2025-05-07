# MRTwin

---

## Introduction

This repository contains the necessary files needed in order to run the MRTwin framework


## Requisites

- Virtual Reality Meta Quest HeadSet (Reccommended Meta Quest 3)
- Unity 2022.3.41f1
- ROS2 Humble
- Isaac Sim 4.2.0

## Tutorial
- Network

In order for this framework to work, the computer must be connected with the UR5e robot through an ethernet connection, also, the Meta Quest Headset and the computer must be connected to the same Wi-Fi

- Meta Quest Headset

1. [Set up the headset for development mode](https://developers.meta.com/horizon/documentation/unity/unity-env-device-setup/)

2. Open the UR5e Project

3. Go to `Robotics` -> `ROS Settings`

![images/ROSSettings.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/ROSSettings.png)

4. In `ROS IP Address` write the IP Address of the computer you are going to use Isaac Sim, you can view the IP of the computer by writing "hostname -I" in the terminal

![images/ROS IP.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/ROS%20IP.png)

5. Connect the VR Headset to the computer via USB-C

7. Go to `File` -> `Build settings...`

![images/BuildSetting.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/BuildSetting.png)

8. On `Run Device` select the Meta Quest Headset you wish to install the program

![images/RunDevice.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/RunDevice.png)

9. Click on `Build and Run`, save the file and wait for the program to upload on the Meta Quest Headset 

- Isaac Sim

![Video Tutorial Isaac Sim Section](https://github.com/enriquecoronado-art/MRTwin/blob/main/videos/IsaacTutorial.mp4)

1. Download vr_ws and Extension

2. Inside the MRTwin Extension folder go to RmpFlow_Example_python and open scenario.py in the line "path_to_robot_usd write the directory to access the "UR5d.usd" file and save 

![images/USDPath.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/USDPath.png)


3. Open Omniverse Launcher

4. Launch Isaac Sim

5. In the Isaac Sim App Selector click on `Open in Terminal` and source ROS2 and the MRTwin workspace by writing the following commands

![images/OpenTerminal.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/OpenTerminal.png)


```bash

#Source global ROS2
source /opt/ros/humble/setup.bash

#Access the MRTwin workspace
cd vr_ws

#Source the workspace
source install/setup.bash

#Return to Isaac Sim directory
cd /home/aist/.local/share/ov/pkg/isaac-sim-4.2.0

#Initiate Isaac Sim
./isaac-sim.sh


```

6. After launching Isaac Sim, go to `Window` -> `Extensions`

![images/Extensions.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/Extensions.png)

7. Click on the three bars icon and select `Settings`

![images/ExtensionSettings.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/ExtensionSettings.png)

8. In `Extension Search Paths` click on the plus sign to add a new path, after that write the directory where the MRTwin Extension is located

![images/PathExtension.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/PathExtension.png)

9. Click on `THIRD PARTY` -> `User` and enable the extension

![images/ExtensionEnable.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/ExtensionEnable.png)

10. A new option called `RMPFlow Example` will appear on the top menu bar click on it and a new menu will appear. On `World Controls` click on `LOAD`

![images/RMPFlow.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/RMPFlow.png)


11. Once the the scenario loads up, go to `Run Scenario` and click on `RUN`


![images/RUNMRTwin.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/RUNMRTwin.png)

- Ubuntu

1. Run the following commands in the terminals

```bash

#Go to the workspace in each terminal
cd ~/vr_ws

#Source the workspace
source install/setup.bash

#Initiate ROS2 connection with Unity in VR Headset
ros2 run ros_tcp_endpoint default_server_endpoint --ros-args -p ROS_IP:=<IP of computer>

#Open RViz and connect with Real UR5e Robot
ros2 launch ur_robot_driver ur_control.launch.py ur_type:=ur5e robot_ip:=163.220.51.112 launch_rviz:=true

#Enable forward position controller
ros2 control switch_controllers --activate forward_position_controller --deactivate scaled_joint_trajectory_controller

#Run publisher for Real UR5e
ros2 run joint_topic jointPosition

#Activate gripper for UR5e 
ros2 run gripper activate_gripper
```

Once everything else is done, inside the Meta Quest Headset, enable the connection with the Real Robot in the menu inside the application

![images/Menu.png](https://github.com/enriquecoronado-art/MRTwin/blob/main/images/Menu.png)


# TODO:

Solve: PlayerSettings->Active Input Handling is set to Both, this is unsupported on Android and might cause issues with input and application performance. Please choose only one active input handling. Ignore and continue? (This dialog won't appear again in this Editor session if you'll choose Yes)


