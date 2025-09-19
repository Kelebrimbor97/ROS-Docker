FROM modelling_ros_humble AS base

#Basic updates
RUN apt-get update
RUN apt-get update --fix-missing
RUN apt-get upgrade -y
RUN apt-get dist-upgrade -y

# Base ROS libraries
# RUN apt-get install ghostscript -y
# RUN apt-get install -y \
#         python3-colcon-common-extensions \
#         ros-$ROS_DISTRO-hardware-interface \
#         ros-$ROS_DISTRO-ament-cmake-clang-format \
#         usbutils \
#         fdisk \
#         python3-wstool \
#         python3-rosdep \
#         ninja-build \
#         stow \
#         ros-$ROS_DISTRO-cartographer \
#         ros-$ROS_DISTRO-cartographer-ros \
#         ros-$ROS_DISTRO-navigation2 \
#         ros-$ROS_DISTRO-nav2-bringup \
#         ros-$ROS_DISTRO-joint-state-publisher* \
#         ros-$ROS_DISTRO-robot-localization* && \
#     apt-get clean && \
#     rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y gedit && \
    apt-get install -y \
        python3-colcon-common-extensions \
        ros-$ROS_DISTRO-hardware-interface \
        gcc-arm-none-eabi \
        ros-$ROS_DISTRO-ament-cmake-clang-format \
        usbutils \
        fdisk \
        python3-wstool \
        python3-rosdep \
        ninja-build \
        stow \
        ros-$ROS_DISTRO-gazebo-* \
        ros-$ROS_DISTRO-cartographer \
        ros-$ROS_DISTRO-cartographer-ros \
        ros-$ROS_DISTRO-navigation2 \
        ros-$ROS_DISTRO-nav2-bringup \
        ros-$ROS_DISTRO-joint-state-publisher* \
        ros-$ROS_DISTRO-robot-localization* && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Official instructions
RUN /bin/bash -lc "source /opt/ros/$ROS_DISTRO/setup.bash" && \
    mkdir -p ~/turtlebot3_ws/src && \
    cd ~/turtlebot3_ws/src/ && \
    git clone -b $ROS_DISTRO https://github.com/ROBOTIS-GIT/DynamixelSDK.git && \
    git clone -b $ROS_DISTRO https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git && \
    git clone -b $ROS_DISTRO https://github.com/ROBOTIS-GIT/turtlebot3.git && \
    sudo apt install python3-colcon-common-extensions && \
    cd ~/turtlebot3_ws && \
    colcon build --symlink-install && \
    echo 'source ~/turtlebot3_ws/install/setup.bash' >> ~/.bashrc 
    
    # source ~/.bashrc

# Source ROS2 everytime a new terminal is opened into the Docker container
RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> ~/.bashrc && \
    echo ". /usr/share/gazebo/setup.sh" >> ~/.bashrc && \
    echo "source ~/turtlebot3_ws/install/setup.bash" >> ~/.bashrc && \
    echo "export TURTLEBOT3_MODEL=burger"  >> ~/.bashrc && \
    echo "export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:`ros2 pkg prefix turtlebot3_gazebo`/share/turtlebot3_gazebo/models/"