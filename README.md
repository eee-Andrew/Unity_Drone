## Unity_Drone
Design from scratch a Drone based controlling system with lighting and physics 
_____________________________________________________________________________________________________________________________________________________________________


# Unity Drone System

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Setup Instructions (1)](#setup-instructions-1)
4. [Setup Instructions (2)](#setup-instructions-2)
5. [Test Setup](#Test-Setup)
6. [Drone Package](#Drone-Package)
7. [Set Plane](#Set-Plane)
8. [Contact](#contact)

## Introduction
This project is a Unity-based drone simulation system designed for controlled navigation. Near future will be autonomous with swarm of drones (Master-slave)


## Prerequisites
Before you begin, ensure you have the following installed on your system:
- Unity version **2020.3** [Unity-Releases](https://unity.com/releases/editor/archive) 
- **Python 3** for scripting, we will use it later [Python-downlaod](https://www.python.org/download/releases/3.0/)
- **ROS (Robot Operating System)** **(Isnt necessary now)** [Ros-Kinetic](https://wiki.ros.org/kinetic/Installation/Ubuntu)
- Install C# [C#-guide-w3school](https://www.w3schools.com/cs/cs_getstarted.php)
  


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

## Test Setup
- Go to Hierarchy -> right click -> empty -> call it : Test_input
- Go to Assets -> Create -> C# script -> call it : Test_input
- Click om Test_input from Hierarchy -> Go to inspector -> Add Component -> Player input
- Grab and hold the **Drone inputs* from Assets and place them to **Player input* from Inspector 
- Double click the Test_input from Assets , will launch C# editor
- Under the void Update function() {        } , write the following
 ```bash
  using UnityEngine;       // top section
  using UnityEngine.InputSystem; // those must be written in the top section of the program
 
  private void OnMove(InputValue value)
  {
     Debug.Log(value.Get<float>());
  }
```
- save it (ctrl + S) and go back to Unity 
- Go to Assets -> Grab and hold Test_input and release it down from Player Input to inspector tab
- hit Play button ( |> ) is on the middle-top -> press keys A,D on your keyboard and see if you have result on Console down left 

## Drone Package
-Go to [Drone Package](https://www.dropbox.com/scl/fi/bidjmh6zcce2o7sgjj1z8/IP_Drone01_Assets_04262020.zip?rlkey=3reihkfydxb6o2srelstvhbo2&e=1&dl=0) and download it , you will see one folder : Tectures one image.png and a .unity package
- Grab the unity package and release it to unity's project tab
- New window will be appeared , press the import button (wait few secs)
- Go to Assets -> Create -> Folder -> name it : Drone_Controller , inside this new folder create 3 new folders named : Art and Code and Input
- In the Art folder create a new folder named : Prefab
- Go to Quad_Racer -> Art -> Drones -> 01 -> Drone_01 , and you will see the drone model (Yellow one)
- Take the **Drones** folder from the last step and move it to **Art** folder which is a subfolder in the Drone_Controller folder
- Right Click on Quad_Racer and delete it , we will not use it anymore
- Drag and Drop the Drone_inputs folder to the input subfolder from previous step
- delete the Test_input from Project and Hierarchy tabs ( we dont need it anymore)
- In Project tab drag the Scenes folder to Drone_Controller folder, open the folder Scenes
- Go to file -> save us -> Assets -> Drone_Controller -> Scenes -> File name : Drone_Controller_DEV -> save
- Now you can see 2 files in Scenes , delete the SampleScene and keep the Drone_Controller_DEV
- Go to Art folder -> Drones_01 -> Drage the Drone_01 to the Hierarchy tab, now you can see the drone in your scene
- Go to Gizmos top middle-right -> Gizmos -> open the arrow -> Camera Speed -> set min 1 and Max 80
- Lets organize our folders , go to Hierarchy tab -> right click -> Create Empty -> name it : Level_GPR  ,level group that will contain all the assets
- In the Inspector tab -> Transform -> click the 3 dots ->hit reset
- Go to Hierarchy -> Level_GPR , create a new empty with name : Light_GPR and drag the Directional light inside this,
-  in the Light_GPR right click -> Light -> Reflection Probe

## Set Plane









