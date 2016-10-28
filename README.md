cognifli
=============

Multicopter autopilot system for robust navigation and task execution in closed space human centric environments.

## BRIEF MANUAL:
### IMPORTANT!
1. This manual assumes you have successfully installed the ROS Indigo on Ubuntu (the code was tested on Ubuntu 14.04)
2. Useful ROS HOWTO's: 
  - [ROS Indigo installation](http://wiki.ros.org/indigo/Installation/Ubuntu "Read this to install ROS on your system")
  - [ROS Tutorial](http://wiki.ros.org/ROS/Tutorials "This is a brief ROS tutorial. Helps to understand basic ROS concepts")
  - [Actionlib](http://wiki.ros.org/actionlib "Look into the actionlib tutorials if you want to deal with the code")
  - [Smach](http://wiki.ros.org/smach/Tutorials "The state mashine library that controls the drone's behavior")
3. Download the 'cognifli' code:
```
cd ~/
git clone https://github.com/cognifli/cognifli
```
4. Some additional packages are to be installed to successfully compile the code. I'll maybe write about this one day, but at the moment you have to look at the compiler errors and set everything up yourself ;)
5. To use bash scripts launch *.../cognifli/contrib/INSTALL.py*. It will generate scripts for you and place them to *.../cognifli/contrib/launchers_gen*. It will also add these to your system PATH. Please take into account that your *~/.bashrc* will be modified! If you want to move the *.../cognifli* folder do it, and after that relaunch *.../cognifli/contrib/INSTALL.py*. The paths will (hopefully) be reconfigured automatically. *INSTALL.py --deps* will also try to install some (if not all!) project dependencies. Run *INSTALL.py -h* to get the full list of options.
6. *INSTALL.py* when launched also creates nice desktop shortcuts for your convenience. They are named *cognifli...smth...* and are easily found via Unity search. (Press Dash Home button and type *'cognifli'*) The config files are placed into *~/.local/share/applications* folder.

### To build the project type:
1. Manually. Go to project directory and enter:
  - catkin_make                                          *(To just build the project)*
  - catkin_make --force-cmake -G"Eclipse CDT4 - Unix Makefiles" -DCMAKE_BUILD_TYPE=Debug -DCMAKE_ECLIPSE_MAKE_ARGUMENTS=-j8 *(To build project files for eclipse)*

2. Via bash scripts (need to configure project with contrib/INSTALL.py). Go to *.../cognifli/contrib/launchers* or add the launchers to your system PATH and enter:
  - cognifli-rebuild                                     *(To just build the project)*
  - cognifli-rebuild-eclipse                             *(To build project files for eclipse)*

### To start the demo type:
1. Manually. Type in the terminal:
  - roslaunch cognifli_gazebo cognifli_world.launch      *(To open Rviz and Gazebo for simulation)*
  - Coming soon ...         

2. Via bash scripts (need to configure project with contrib/INSTALL.py). Go to *.../cognifli/contrib/launchers* or add the launchers to your system PATH and enter:
  - cognifli-simulator                                   *(To open Rviz and Gazebo for simulation)*
  - Coming soon ...         

### To change the spawn point in Gazebo:
 1. Go to *.../cognifli/src/cognifli_simulator/cognifli_gazebo/launch/cognifli_world.launch*
 2. Set the coordinates by adjusting `<arg name="x/y/z" value="???"/>`

### To change the default gazebo camera position:
 1. Go to *.../cognifli/src/cognifli_simulator/cognifli_gazebo/worlds/<...>.world*
 2. Find the `<camera name='some_camera_name'>`
 3. Change the <pose> tag 				 *(There will be the `<pose>X Y Z R P Y</pose>` string, put in the correct numbers)*

### To change map:
 1. **DO** it carefully!
 2. If you still decided to add a custom map create a model in [Google Sketch Up](http://www.sketchup.com/) (free to download)
 3. The model should have .dae extension and the altitude of the floor at the robot spawn point should be zero
 4. It is important that it is zero!
 5. Rename the .dae file to "test_chamber0.dae". **Do NOT** rename the generated folder with images! (sometimes there will be no folder generated, do not worry about that) But if you desperately want to rename, edit the .dae file and update the path to the folder.
 6. Put the files in *.../cognifli/src/cognifli_simulator/cognifli_gazebo/worlds/Media/models* folder
 7. If the model jumps on its spawn point than you probably did not set the world floor altitude to zero. You can probably edit the *.../cognifli/src/cognifli_simulator/cognifli_gazebo/worlds/cognifli.world* to fix that.

### To edit the robot model:
 1. Be careful here too)
 2. Go to *.../cognifli/src/cognifli_simulator/cognifli_description/cognifli_drone/urdf*
 3. Edit the *cognifli_drone.urdf.xacro* file to add/modify sensors and tweak other parameters

### For more information on the project read our beloved [wiki](https://github.com/cognifli/cognifli/wiki)!

### Possible issues:
+ If gazebo fails to download models at the startup you'll have to do it manually:
```
cd <somewhere>
hg clone https://bitbucket.org/osrf/gazebo_models
export GAZEBO_MODEL_PATH=${GAZEBO_MODEL_PATH}:$PWD/gazebo_models
```
