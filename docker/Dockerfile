FROM acutronicrobotics/gym-gazebo2

LABEL maintainer="vansh.rai.saini@gmail.com>"

# setup environment
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

ENV ROS2_DISTRO dashing
#Prepare work-space
RUN mkdir -p /root/ros2_mara_ws/src
WORKDIR /root/ros2_mara_ws

RUN \
      #ros2learn
      cd /root && git clone -b dashing https://github.com/AcutronicRobotics/ros2learn \
      && cd /root/ros2learn \
      && git submodule update --init --recursive \
      && git pull --recurse-submodules && git submodule update --recursive --remote \
      && cd /root/ros2learn/algorithms/baselines && pip3 install scikit-build &&pip3 install -e .\
      && cd /root/ros2learn/environments/gym-gazebo2 && pip3 install -e .
      #Load provisioning script
WORKDIR /root/ros2learn/
EXPOSE 11597
ENTRYPOINT ["bash"]
