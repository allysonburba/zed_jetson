FROM nvidia/cuda:12.2.2-base-ubuntu20.04

SHELL ["/bin/bash", "-c"]

RUN rm -Rf /etc/apt/sources.list.d/cuda.list

RUN apt-get update -y && apt-get install -y \
    git \
    vim \
    curl \
    wget \
    zstd \
    python3-pip

####################################################################################################
########################################### ROS NOETIC #############################################
####################################################################################################

RUN echo "deb http://packages.ros.org/ros/ubuntu focal main" > /etc/apt/sources.list.d/ros-latest.list && \
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add - && \
    apt-get update -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y ros-noetic-desktop

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    python3-rosdep \
    python3-rosinstall \
    python3-rosinstall-generator \
    python3-wstool \
    python3-catkin-tools \
    ros-noetic-catkin \
    build-essential &&\
    rosdep init && \
    rosdep update

RUN python3 -m pip install --upgrade pip

CMD ["bash"]