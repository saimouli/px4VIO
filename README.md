# Snapdragon Flight VISLAM-ROS Sample Code
This repository is a fork of the VISLAM from ATLFlight/ros-examples, modified to work with the px4 flight stack. The original README can be found in the [ATLFlight/ros-examples](https://github.com/ATLFlight/ros-examples/blob/master/README.md) repository.

## Preparations
### Mavros
Get the mavros sources into your catkin's source directory by following the instructions from the [mavros git page](https://github.com/mavlink/mavros/tree/master/mavros#source-installation).

This example code is for MV SDK release [mv_1.0.2](https://developer.qualcomm.com/hardware/snapdragon-flight/tools).

**NOTE**: The older release(mv0.9.1) instructions are [here](https://github.com/ATLFlight/ros-examples/tree/master).

**NOTE**: Step 3 should also include `--rosdistro kinetic` flag.

### Other packages
On a freshly flashed snapdragon, I had to install the following packages
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
>>>>>>> Readme update

## Build
`catkin build`

Compiling mavros can easily take 30 minutes on the snapdragon.

<<<<<<< 2121ee3681d9575c9a3f9d06fea03a7e8cca1ec7
## High-Level Block Diagram
![SnapVislamRosNodeBlockDiagram](images/SnapVislamRosNodeBlockDiagram.jpg)

## Setup and build process

**NOTE:** These instructions are for VISLAM version mv_0.9.1_8x74.deb.  For earlier versions refer to [this](https://github.com/ATLFlight/ros-examples) page.


### Summary of changes from previous release

| Item | Previous release - mv0.8 | Current Release - mv0.9.1 | Future Release mv 1.0.2 |
|----|----|----|----|
|MV_SDK environment variable| needed | Not needed.  The new mv installation puts the library files under /usr/lib | Not needed |
|MV License file installation | needed.  Should be placed in the /opt/qualcomm/mv/lib/mv/bin/lin/8x74/ | needed should be placed at /usr/lib | needed should be placed at /opt/qcom-licenses/ |
|MV link library Name| libmv.so | libmv1.so.  Update the respective make files to link against libmv1 instead of libmv.so | same as mv 0.9.1 |

The current build process is supported only on-target (i.e. on the Snapdragon Flight<sup>TM</sup> Board).  Future release(s) will support off-target cross-compilation on a host computer.

The following is an overall workflow for installation, build and execution of the ROS sample apps for Snapdragon Flight<sup>TM</sup>

![Installation and build Work Flow](images/InstallationAndBuildWorkflow.jpg)

### Pre-requisites

#### Platform BSP

These instructions were tested with version **Flight_3.1.3**. The latest version of the software can be downloaded from [here](http://support.intrinsyc.com/projects/snapdragon-flight/files) and  installed by following the instructions found [here](http://support.intrinsyc.com/projects/snapdragon-flight/wiki)

**NOTE**: By default the HOME environment variable is not set.  Set this up doing the following:

```
adb shell
chmod +rw /home/linaro
echo "export HOME=/home/linaro/" >> /home/linaro/.bashrc
```

If you use SSH, the home environment variable should be set correct after the above step.
If you use ADB, do the following for each session:

```
adb shell
source /home/linaro/.bashrc
```


#### Install ROS on Snapdragon Platform.

Refer to the following [page](https://github.com/ATLFlight/ATLFlightDocs/blob/master/SnapdragonROSInstallation.md) for ROS installation on Snapdragon Flight<sup>TM</sup> platform.

#### Install Snapdragon Machine Vision SDK

* Download the latest Snapdragon Machine Vision SDK from [here](https://developer.qualcomm.com/sdflight-tools)
* The package name will be mv\<version\>.deb.  
** Example: *mv1.0.2_8x74.deb*
* push the deb package to the target and install it.

```
adb push mv<version>.deb /home/linaro
adb shell sync
adb shell
dpkg -i /home/linaro/mv<version>.deb
```

*NOTE:* MV release 0.8 and earlier required to set the MV_SDK environment variable.  This is no longer needed.  Make sure to unset this variable if it is set.  Not doing so will give an compilation error that says, "mv.h" file is not found.

#### Machine Vision SDK License Installation

The Machine Vision SDK will need a license file to run.  Obtain a research and development license file from [here](https://developer.qualcomm.com/sdflight-key-req)

The license file needs to be placed in the following folder on target: /opt/qcom-licenses/

Push the license file to the target using the following command:

```
adb push snapdragon-flight-license.bin /opt/qcom-licenses/
adb shell sync
```

*NOTE:* Make sure to create the folder /opt/qcom-licenses/ if it is not present on the target.

### Clone and build sample code

#### Setup ROS workspace on target

```
adb shell
source /home/linaro/.bashrc
mkdir -p /home/linaro/ros_ws/src
cd /home/linaro/ros_ws/src
catkin_init_workspace
cd ../
catkin_make
echo "source /home/linaro/ros_ws/devel/setup.bash" >> /home/linaro/.bashrc
```

This ensures that the ROS workspace is setup correctly.

#### Clone the sample code
* The repo may be cloned from [here]( from https://github.com/ATLFlight/ros-examples.git) directly on the target, or cloned on the host computer and then pushed to the target using ADB. The recommended method is to clone directly on the target.

```
adb shell
source /home/linaro/.bashrc
roscd
cd ../src
git clone -b mv-release-1.0.2 https://github.com/ATLFlight/ros-examples.git snap_ros_examples
```

* Build the code
=======
>>>>>>> Readme update

## Configure
Copy the px4 configuration files from `./px4_configs` to their respective location on the snapdragon. For using the recommended LPE:
```
cd snapdragon_mavros_vislam
adb push ./px4_confs/lpe/mainapp.conf /home/linaro/mainapp.conf
adb push ./px4_confs/lpe/px4.config /usr/share/data/adsp/px4.config
```

and if you want to give EKF2 a try:
```
cd snapdragon_mavros_vislam
adb push ./px4_confs/ekf2/mainapp.conf /home/linaro/mainapp.conf
adb push ./px4_confs/ekf2/px4.config /usr/share/data/adsp/px4.config
```

The configurations are intended to provide a working starting point. Adjust parameters to your likings.

## Run
Get a roscore up and running
```
adb shell
roscore
```

In another terminal, launch mavros and vislam
```
adb shell
roslaunch snapdragon_mavros_vislam mavros_vislam.launch
```

Start the px4 flight stack
```
adb shell
cd $HOME
./px4 mainapp.config
```
