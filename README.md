# Ros 2


## first time setup
```
sudo apt-get install git
```

```
sudo apt install software-properties-common
sudo add-apt-repository universe
```

```
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```


```
sudo apt update
```


```
sudo apt upgrade
```


```
sudo apt install ros-humble-desktop
```


```
sudo apt install ros-humble-ros-base
```


```
sudo apt install ros-dev-tools
```



## Replace ".bash" with your shell if you're not using bash
## Possible values are: setup.bash, setup.sh, setup.zsh

```
source /opt/ros/humble/setup.bash
```



## install gazebo fortress (simulation engine)

```
sudo apt-get update
sudo apt-get install lsb-release gnupg
```


then install ignition fortress
```
sudo curl https://packages.osrfoundation.org/gazebo.gpg --output /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null
sudo apt-get update
sudo apt-get install ignition-fortress
```


Creating ROS2 Gazebo bridge

https://github.com/gazebosim/ros_gz_project_template/tree/fortress
At this link you will have the ros_gz template basiaclly the repo that will setup the link connecting ROS2 into our gazebo simulation.
I'd probably recommend downloading the zip and extracting by hand or just follow these commands:

Install necessary tools:

```
sudo apt install python3-vcstool python3-colcon-common-extensions git wget
```

create workspace:

```
mkdir -p ~/template_ws/src
cd ~/template_ws/src
git clone -b fortress https://github.com/gazebosim/ros_gz_project_template.git
```

Install Dependencies:

```
cd ~/template_ws
source /opt/ros/humble/setup.bash
sudo rosdep init
rosdep update
rosdep install --from-paths src --ignore-src -r -i -y --rosdistro humble
```

Build the project:

```
colcon build --cmake-args -DBUILD_TESTING=ON
```

Source the workspace:

```
. ~/template_ws/install/setup.sh
```

Launch test sim:

```
ros2 launch ros_gz_example_bringup diff_drive.launch.py
```

If that worked GREAT! (if it didnt, try to troubleshoot it by looking up the error, if youre still stuck message me and I can see if i know a fix)

Now heres a little test sim that you can follow all the way through and it'll show you how to visualize lidar data from the gazebo sim in Rviz2
https://docs.ros.org/en/humble/Tutorials/Advanced/Simulators/Gazebo/Gazebo.html#prerequisites
