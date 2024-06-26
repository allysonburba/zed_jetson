FROM nvcr.io/nvidia/l4t-base:r35.2.1

SHELL ["/bin/bash", "-c"]

RUN apt-get update -y && apt-get install -y \
    git \
    vim \
    curl \
    gnupg2 \
    lsb-release

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
    build-essential &&\
    rosdep init && \
    rosdep update

CMD ["bash"]