# Snapdragon Flight VISLAM-ROS Sample Code
This repository is a copy of the VISLAM from ATLFlight/ros-examples, modified to work with the px4 flight stack.

## Preparations
Get the mavros sources into your catkin's source directory by following the instructions from the [mavros git page](https://github.com/mavlink/mavros/tree/master/mavros#source-installation).

Note: Step 3 should also include `--rosdistro kinetic` flag.

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
