FROM nvidia/cuda:12.2.2-base-ubuntu22.04
SHELL ["/bin/bash", "-c"]

ENV CMAKE_BUILD_TYPE=Release

# Install necessary packages including lsb-release beforehand
RUN apt update && DEBIAN_FRONTEND=noninteractive apt install -y \
    curl \
    gnupg \
    lsb-release \
    build-essential  # Ensure build tools are available

# Verify lsb_release output manually or set it explicitly
RUN echo $(lsb_release -sc)

# Add the ROS repository and install ROS Noetic
RUN echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list && \
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add - && \
    apt update && \
    DEBIAN_FRONTEND=noninteractive apt install -y ros-noetic-ros-base

# Install additional ROS and development tools
RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    python3-catkin-tools \
    python3-rosdep && \
    rosdep init && \
    rosdep update

CMD ["bash"]