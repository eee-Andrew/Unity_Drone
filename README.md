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
8. [Lighting](#Lighting)
9. [New Input System for Physics](#New-Input-System-for-Physics)
10. [Create Script for Input System](#Create-Script-for-Input-System-for-Physics)
11. [Camera Setup](#Camera-Setup)
12. [Post Effects Setup](#Post-Effects-Setup)
13. [Creating the Physics](#Creating-the-Physics)


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
-Go to [Drone Package](https://www.dropbox.com/scl/fi/bidjmh6zcce2o7sgjj1z8/IP_Drone01_Assets_04262020.zip?rlkey=3reihkfydxb6o2srelstvhbo2&e=1&dl=0) and download it , you will see one folder : Textures ,one image.png and a .unity package
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
- Go to Level_GRP -> right click -> 3d object -> Plane -> rename it to ground 
- Go to Transform -> scale -> x=10,y=10,z=10
- Go to Art -> right click  -> show in Explore -> go to Art , open the download file from previous steps and copy paste the texture folder in the art folder
- Go back to Unity -> Project tab -> Art -> click Gray_Grid_MAT and you will see that a new Inspector opens , in the same folder textures : you will see a gray-grid with black icon, drag it and place it to the Inspector tab Under the *MAIN MAPS in the White icon (Albedo)
- Go back to Project -> Gray_Grid_MAt and drag it to the main Scene inside the "animated environment"
- We can change the Tiling in the Ispector to be 100 x 100
- click on the animated Scene (ground) , we have to se the reflection probe to static (top right corner) click the box
  
## Lighting
- Window -> Rendering -> Lighting Settings
- At this point turn of the Realtime Lighting
- change the Indirect samples and the enviroment samples to 128 from 500
- change the lightmap Resolution to 10 from 40 
- Let unticked the Ambient Occlusion box
- Lightmap Parameters set them to Default-LowResolution
- Hit Generate Lighting (will take a minute)
- You will see a mirror ball above the drone means everything is working if you dont see just click the Reflection Probe from Hierarchy
- 
- 


## New Input System for Physics
- In this section we will set up the Input Mapping
- Go to Assets -> Drone -> Controller -> Input -> click the Drone_Input -> go to right and click edit asset
- Delete our previous AD folder which includes Negative and Positive and the Move Folder, we will start fresh
- Create new by clicking on **+** button and name it Cyclic(will take care of the Y rotation of the drone, so it will look realistic)
- Delete the Binding above like previous
- Click the Cyclic -> Properties -> Action Type -> change it to Pass through from Button
- Click on Control Type and set it to : Vector 2 from button
- Go to Cyclist label ,there is plus button **+** right from it , press it and Add 2D Vector Composite (its going to give us Up,down,left,right), name the folder that contain those : WASD (are keyboard keys)
- Click the UP : Binding -> path : W [Keyboard]
- Click the Down : Binding -> path : S [Keyboard]
- Click the left : Binding -> path : A [Keyboard]
- Click the Right : Binding -> path : D [Keyboard]
- Add another one by pressing the **+** again , Add 2D Vector Composite
- Name it Lstick , go to Properities -> Binding -> Path -> Gamepad : Xbox controlller (or what ever you have)
- Change the Up / Down / Left /Right like previous and choose yours according to your controller
- Now we need some pedals for the x rotation of the drone (for ex. if you have a camera on it you can rotate it while you are moving foward so it can take images from its back
- Go to Actions , Press **+** right from Actions and name is Pedals, delete the binding
- Click on Pedals go to Action Type and set it to Pass Through and the Control Type set it to Axis
- Go back to Pedals press **+** add 1D Axis Composite
- Name it Arrows instead of 1D Axis , go to Negative -> path -> write : Left Arrow [keyboard]
- Got to Positive and select the Right Arrow [keyboard]
- Now we have to set the Drone to go up and Down
- Go to Inputs ,add new Action ,name it Throttle,delete the binding
- click on throttle set the Action Type from Button to Value
- Go to Control Type and from Button set it to Axis
- Go back to Throttle press **+** and ADD 1D Axis Composite,name it Arrows
- will give us negative and positive for Axis
- On Negative go to path : Down Arrow
- On Positive go to path : Up Arrow
- For XBOX start....
- On throttle press **+** and add another 1D AXis Composite call it Rstick
- set negative and positive , go to path : Gamepad -> Xbox controller , Negative->Right Stick/Down and Positive -> Right Stick/Up
-Go to Pedals , press **+** AdD 1D Axis Composite, call it Rstick
- set negative and positive to Left and right
- -end for xbox
- 
## Create Script for Input System
- In the Assets -> code -> create -> Folder name : Editor
- In the Assets -> code -> create -> Folder name : Scripts
- In the Scripts -> create -> C# Script ,name it : IP_Drone_Inputs , double click this , will open C# IDE Visual studeio 

```bash
 using UnityEngine.InputSystem; // top section, write it down from Using UnityEngine;
 namespace myworkspace    // to secure the code will run smoothly place all the functions inside  namespace
  {
    [RequireComponent(typeof(PlayerInput))] // will search automatically if there is assigned a key component for player input,if not
     //will going to make one for us
    public class IP_Drone_Inputs : MonoBehaviour
    {   //those viarables are private means we cant share them to other scripts so we have to make C# properties
        //to do this , highlight the cyclic, right click ,choose Quick Actions and Refactorings..
        //press the Encapsulate field 'cyclic'(and use property) 
        #region Variables
        private Vector2 cyclic;
        private float pedals;
        private float throttle;

        public Vector2 Cyclic { get => cyclic; } //this line generated by the step above
        public float Pedals { get => pedals; } //this line generated by the step above
        public float Throttle { get => throttle; } //this line generated by the step above

        #endregion

        $region Main Methods

       // void Start()
       // {

       // }

        voide Update()
        {

        }
        #endregion

        #region Input Methods

        private void OnCyclic(InputValue value)
        {
          cyclic = value.Get<Vector2>();
        }
        private void OnPedals(InputValue value)
        {
          pedals = value.Get<float>();
        }
        private void OnThrottle(InputValue value)
        {
          throttle = value.Get<float>();
        }

        #endregion

     }

  }

```
- save the script
- Go back to Unity on Scene (main window of animated image with drone)
- Go to Hierarchy -> right click -> Create Empty -> nam it: Drone
- Go to right , the 3 dots on Transform and press Reset
- Drag and drop the Drone_01 to Drone (Hierarchy) its for asthetic
- Go to Assets -> code -> scripts -> IP_Drone_Inputs drag and drop it on the Inspector tab bellow the transform
- Go to Assets -> Input -> Drone_Inputs drag and drop it to player input from last step to "None (Input Action Asset)"
- set Default Map to : Drone
-set Behavior : Send messages
- go to Drone_Inputs (Input Actions) is a window in the top of the screen and press **save Asset*** SOS
- Go to 3 dots in the Inspector Tab and switch from Normal to Debug mode
- Hit Play and you will see the values 


## Camera Setup
- Go to scene
- Press the main camera from Hierarchy
- Press Ctrl Shift F
- This will automatically place the Camera to focus on the Drone
  
## Post Effects Setup
- Right Click on the Level_GPR -> Create Empty name it Post
- Go to Inspector and Add Component : Post-process Volume
- tick the "is Global" which is in the same tab
- hit the "new" on the right side of "None (Post Process Profile), this is automatically saved on Project->Scenes->Drone_Cntroller_DEV_Profiles
- Go toIspector , on the top there is a Layer , Add Layer , User Layer 8 -> name it: post
- Go back and then select the Layer : post
- To see the post effects go to main camera and Add Component : Post-process Layer (there will be a yellow warning)
- Set the layer fromn Nothing to post and set the Anti-aliasing to Temporal Anti-aliasing(TAA)
- set the sharpness to 0.90 (so it will be more reallystic)
- select the Post in the Hierarchy and go to Inspector so you can press Add effect..
- Select Unity -> Ambient Occlusion
- set the Intensity to 1.20
- Add another Component -> Unity -> Bloom , set the intensity to 6.40
- Add another Component -> Unity -> Color Granding , Click the "MODE" box on the Tonemapping and choose the ACES 
- Set the Post-exposure (EV) to 1.3 so it will be brighter the environment
- Go to Lift (Left colourfull circle) and move the middle point a little bit to the top right where the red ping colours are
- Go to Gammas (middle colourfull circle) and move it a little bit down to blue
- go to top select Gizmos and turn off the 3D Icons
- go back to inspector on the Post from Hierarchy and add a new component : Motion Blur 
- Add another one component named : Vignette ->click on Intensity and set it to 0.367
- 
- 

## Creating the Physics
- Creating the Base Rigidbody
- Go to Project -> in the script folder -> create -> C# name it IP_Base_Rigidbody
- Go to Zip Folder we download before from link , take the icon and drag drop it to Editor , is in the Assets in the code folder
- Select the script IP_Base_Rigdbody, go to Inspector press the white C# icon , press the other and search for indie-pixel-icon_32px
- Do the same for the Ip_Drone_Inputs
- Go to 3D Icons in Gizmos and set the bar to 20% (randomly)
- Double click the IP_Base_Rigidbody will launch the C# editor
- 
- 
```bash

using UnityEngine;

namespace myworkspace
{
      [RequireComponent(typeof(Rigidbody))]
    
      public class IP_Base_Rigidbody : MonoBehaviour
    {
      #region Variables
      [header("Rigidbody Properties")] //allow user to assigne the number of punds the weight of the drone
      [SerializedField] private float weightInLbs =1f;
      
      const float lbsToKg = 0.454f;    //Unity works in kilograms not pounds(lbs)
      protected Rigidbody rb;
      protected float startDrag;
      protected float startAngularDrag;
      #endregion


      #region Main Methods
      //start is called before the first fframe update
      void Awake()  //change the start
        {
          rb = GetComponent<Rigidbody>();
          if(rb)
                {
                  rb.mass=weightInLbs * lbsToKg;
                  startDrag = rb.drag;
                  startAngularDrag = rb.angularDrag;
                }
         }

      void FixedUpdate()  //rename the Update function
      {
        if(!rb) //if we dont find the rb , somhow is detached
          {
            return;
          }

          HandlePhysics();
      }
      #endregion
      #region Custom Methods
      protected virtual void HandlePhysics() { }  
      #endregion
 }
}
```
-save the script
- click the drone on Hierarchy and Drag the Input_Base_Rigidbody to inspector of the drone 
- you can see the mass of the drone but we dont need them now , so delete first the IP_Base_Rigidbody (script) then the Rigidbody
- Go to Scripts -> Create -> C# _> name it IP_Drone_Controller (you can change the icon too if you want)


```bash
using UnityEngine;

namespace myworkspace
{
   [RequireComponent(typeof(IP_Drone_Inputs))]
    public class IP_Drone_Controller : IP_Base_Rigidbody
    {
    #region Variables
    [Header("Control Properties")]
    [SerializeField] private float minMaxPitch =30f;
    [SerializeField] private float minMaxRoll =30f;
    [SerializeField] private float yawPower =4f;
    [SerializeField] private IP_Drone_Inputs input;
    #region Main Methods


    #endregion
    voide Start()
      {
         input = GetComponent<IP_Drone_Inputs>();
       }
    
    #endregion
    #region Custom Methods
    protected override void HandlePhysics()
    {
       HandleEngines();
       HandleControls();
    }
     protected virtual void HandleEngines()
     {
        rb.AddForce(Vecotr3.up * (rb.mass * Physics.gravity.magnitude));
     }

     protected vitual void HandleControls()
     {
     }
     #endregion
    }
}
```
- Go to Scripts Folder -> create new folder name it : Interfaces
- In it create a new C# script and name it : IEngine (I =interface)
- you can set the icon as you want
- Double click go to visual studio
  
```bash

using UnityEngine;

namespace myworkspace
{
    public interface IEngine
    {
      void InitEngine();
      void UpdatedEngine();
    }
}
```
- Go back to Scripts -> Create -> C# -> name it IP_Drone_Engine
- double click on it 
```bash

using UnityEngine;

namespace myworkspace
{
    public class IP_Drone_Engine : MonoBehaviour, IEngine // highlight it right click and press Implement interface thats how u solve the red highlighting
    {
      #region Variables
      [Header("Engine Properties")]
      [SerializeField} private float maxPower = 4f;
      #endregion

      #region Interface Methods
      public void InitEngine()
      {
        throw new System.NotImplementedException();
      }
      public void UpdateEngine()
      {
        throw new System.NotImplementedException();
      }
      #endregion
    }
}
```

Unity 2019 - Drone Controller - Section 3 - Video 4
 3 - Video 4





















