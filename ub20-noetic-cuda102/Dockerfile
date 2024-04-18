FROM personalroboticsimperial/prl:jetson2004
SHELL ["/bin/bash", "-c"] 

ENV CMAKE_BUILD_TYPE=Release

RUN apt update && DEBIAN_FRONTEND=noninteractive apt install -y \
    curl gpg-agent

RUN echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list && \
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add - &&\
    apt update &&  \
    DEBIAN_FRONTEND=noninteractive apt install -y  ros-noetic-ros-base

RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    python3-catkin-tools python3-rosdep && \
    rosdep init && \
    rosdep update

CMD bash