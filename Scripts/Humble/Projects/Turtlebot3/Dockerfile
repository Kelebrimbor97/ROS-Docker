FROM modelling_ros_humble AS base

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


# Install turtlebot3
RUN mkdir ~/turtlebot3_ws && \
    cd ~/turtlebot3_ws && \
    mkdir src && \
    wget https://raw.githubusercontent.com/ROBOTIS-GIT/turtlebot3/ros2/turtlebot3.repos && \
    vcs import src<turtlebot3.repos && \
    rosdep update && \
    rosdep install --from-paths src --ignore-src -y && \
    colcon build
    
# Source ROS2 everytime a new terminal is opened into the Docker container
RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> ~/.bashrc && \
    echo ". /usr/share/gazebo/setup.sh" >> ~/.bashrc && \
    echo "source ~/turtlebot3_ws/install/setup.bash" >> ~/.bashrc && \
    echo "export TURTLEBOT3_MODEL=burger"  >> ~/.bashrc && \
    echo "export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:`ros2 pkg prefix turtlebot3_gazebo`/share/turtlebot3_gazebo/models/"