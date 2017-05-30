# Snapdragon Flight VISLAM-ROS Sample Code
This repository is a copy of the VISLAM from ATLFlight/ros-examples, modified to work with the px4 flight stack.

## Preparations
Get the mavros sources into your catkin's source directory by following the instructions from the [mavros git page](https://github.com/mavlink/mavros/tree/master/mavros#source-installation).

Note: Step 3 should also include `--rosdistro kinetic` flag.

Note2: On a freshly flashed snapdragon, I had to install the following things
* python pip
* python future (`pip install future`)
* `sudo apt-get install ros-indigo-diagnostic-updater`
* `sudo apt-get install ros-indigo-angles`
* `sudo apt-get install ros-indigo-eigen-conversions`
* `sudo apt-get install ros-indigo-urdf`
* `sudo apt-get install ros-indigo-tf`
* `sudo apt-get install ros-indigo-control-toolbox`
  If `control-toolbox` cannot be installed due to unmet dependencies, you might have to install the missing dependency yourself. In my case overwriting an existing file was necessary for the package `fontconfig-config`. That can be done with
  `sudo apt-get -o Dpkg::Options::="--force-overwrite" install fontconfig-config`


## Build
`catkin build`

This can easily take 30 minutes on the snapdragon.


## Run
Get a roscore running
`roscore`

Start the px4 flight stack
```
cd $HOME
./px4 mainapp.config
```

Launch rpg_qualcomm_vislam
`roslaunch rpg_qualcomm_vislam mavros_vislam.launch`
