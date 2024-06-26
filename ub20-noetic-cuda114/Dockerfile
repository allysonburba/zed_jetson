FROM nvcr.io/nvidia/l4t-tensorrt:r8.4.1.5-devel

SHELL ["/bin/bash", "-c"]

RUN rm -Rf /etc/apt/sources.list.d/cuda.list

RUN apt-get update -y && apt-get install -y git vim

####################################################################################################
########################################### ROS NOETIC #############################################
####################################################################################################

RUN echo "deb http://packages.ros.org/ros/ubuntu focal main" > /etc/apt/sources.list.d/ros-latest.list && \
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add - && \
    sed -i 's=deb https://repo.download.nvidia.com/jetson/common r35.1 main=# deb https://repo.download.nvidia.com/jetson/common r35.1 main=' /etc/apt/sources.list &&\
    apt-get update -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y ros-noetic-desktop

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    python3-rosdep \
    python3-rosinstall \
    python3-rosinstall-generator \
    python3-wstool \
    python3-catkin-tools \
    build-essential &&\
    rosdep init && \
    rosdep update

CMD bash