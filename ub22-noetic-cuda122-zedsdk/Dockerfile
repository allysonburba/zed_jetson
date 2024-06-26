FROM nvidia/cuda:12.2.2-base-ubuntu20.04

SHELL ["/bin/bash", "-c"]

RUN apt-get update -y && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    wget \
    zstd \
    python3-pip

RUN python3 -m pip install --upgrade pip

####################################################################################################
########################################### ZED SDK 4.0 ############################################
####################################################################################################

WORKDIR /zed

COPY .nv_tegra_release /etc/nv_tegra_release

RUN wget -q -O ZED_SDK_Jetson_40.run https://download.stereolabs.com/zedsdk/4.0/l4t35.4/jetsons
RUN chmod +x ZED_SDK_Jetson_40.run && \
    DEBIAN_FRONTEND=noninteractive ./ZED_SDK_Jetson_40.run --silent && \
    rm ZED_SDK_Jetson_40.run

RUN python3 -m pip install cython numpy opencv-python pyopengl
RUN apt-get update -y && apt-get install --no-install-recommends python3-pip -y && \
    wget download.stereolabs.com/zedsdk/pyzed -O /usr/local/zed/get_python_api.py &&  \
    python3 /usr/local/zed/get_python_api.py && \
    python3 -m pip install numpy opencv-python *.whl && \
    rm *.whl

WORKDIR /root/ros_ws


RUN mkdir -p /root/ros_ws/src/ && source /opt/ros/noetic/setup.bash && catkin init && catkin build

RUN cd src && git clone --recurse-submodules -j8 https://github.com/stereolabs/zed-ros-wrapper.git
RUN apt update && source devel/setup.bash && DEBIAN_FRONTEND=noninteractive rosdep install --from-paths src --ignore-src -r -y 
RUN python3 -m pip install -U pip && python3 -m pip install opencv-contrib-python

RUN git clone https://github.com/stereolabs/zed-ros-examples.git
RUN apt update && DEBIAN_FRONTEND=noninteractive rosdep install --from-paths . --ignore-src -r -y
RUN catkin build -DCMAKE_BUILD_TYPE=Release


RUN source devel/setup.bash && \
    catkin config --cmake-args -DCMAKE_CXX_FLAGS="-Wl,--allow-shlib-undefined" && \
    catkin build zed_wrapper


CMD bash