FROM modelling_ros AS base

#Basic updates
RUN apt-get update
RUN apt-get update --fix-missing
RUN apt-get upgrade -y
RUN apt-get dist-upgrade -y

# Base ROS libraries
RUN apt-get install ghostscript -y
RUN apt-get install -y \
        python3-colcon-common-extensions \
        ros-$ROS_DISTRO-hardware-interface \
        ros-$ROS_DISTRO-ament-cmake-clang-format \
        usbutils \
        fdisk \
        python3-wstool \
        python3-rosdep \
        ninja-build \
        stow \
        ros-$ROS_DISTRO-cartographer \
        ros-$ROS_DISTRO-cartographer-ros \
        ros-$ROS_DISTRO-navigation2 \
        ros-$ROS_DISTRO-nav2-bringup \
        ros-$ROS_DISTRO-joint-state-publisher* \
        ros-$ROS_DISTRO-robot-localization* && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*