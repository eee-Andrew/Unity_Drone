## Unity_Drone
Design from scratch a Drone based controlling system with lighting and physics 
_____________________________________________________________________________________________________________________________________________________________________


# Unity Drone System

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Setup Instructions (1)](#setup-instructions-1)
4. [Setup Instructions (2)](#setup-instructions-2)
5. [Usage](#usage)
6. [Contributing](#contributing)
7. [License](#license)
8. [Contact](#contact)

## Introduction
This project is a Unity-based drone simulation system designed for controlled navigation. Near future will be autonomous with swarm of drones (Master-slave)


## Prerequisites
Before you begin, ensure you have the following installed on your system:
- Unity version **2020.3** [Unity-Releases](https://unity.com/releases/editor/archive) 
- **Python 3** for scripting, we will use it later [Python-downlaod](https://www.python.org/download/releases/3.0/)
- **ROS (Robot Operating System)** **(Isnt necessary now)** [Ros-Kinetic](https://wiki.ros.org/kinetic/Installation/Ubuntu)
- Install C# [C#-guide-w3school](https://www.w3schools.com/cs/cs_getstarted.php)
- 


## Setup Instructions 1
- Open Unity and create a new project 3D
- Go to Edit -> Project Settings -> Player Settings -> Other Settings -> Switch from **Gamma** to **Linear**
- Go to Window -> Package Manager -> "Advanced" tab -> Show preview packages -> search for: **Post Processing** -> hit Install
- Go to Window -> Package Manager -> "Advanced" tab -> Show preview packages -> search for: **Input System** -> hit Install
- Restart the editor 


## Setup Instructions 2
- Go to Assets(down left) -> right click -> Create -> Input Actions -> name it : **Drone_inputs**
- Double left click on Drone_inputs -> hit plus **+** button , name it : **Drone**
- Click on New actions and name it : Move
- Delete the <*No_Binding> with right click 
- Click on: Move -> Action -> from Button change it to **value**
- Go right from Move press **+** button and ADD 1 Axis Composite
- Go to Negative (just created) on Binding -> Path choose your Input like xbox controller, in my case is Keyboard.
- Define the keys you are pressing , go to search bar near Litsen and type : A [keyboard]
- Go to Possitive and do the same by choosing : D [keyboard]
- Press Save Asset
















