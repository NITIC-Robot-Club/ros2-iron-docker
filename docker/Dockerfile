## Ubuntu 22.04 (jammy)
## ROS2 Iron

FROM ubuntu:jammy

SHELL ["/bin/bash", "-c"]

WORKDIR /ros2_ws

ENV TZ=Asia/Tokyo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install ROS2
RUN apt update && \
    apt install -y curl gnupg2 lsb-release git locales ca-certificates gcc g++ make

RUN locale-gen ja_JP ja_JP.UTF-8 && \
    update-locale LC_ALL=ja_JP.UTF-8 LANG=ja_JP.UTF-8 && \
    export LANG=ja_JP.UTF-8 && \
    locale

RUN apt install -y software-properties-common && \
    add-apt-repository universe

RUN curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | tee /etc/apt/sources.list.d/ros2.list > /dev/null

RUN apt update && apt install -y ros-dev-tools ros-iron-desktop

RUN source /opt/ros/iron/setup.bash

RUN sh -c 'echo "deb [arch=$(dpkg --print-architecture)] http://repo.ros2.org/ubuntu/main `lsb_release -cs` main" > /etc/apt/sources.list.d/ros2-latest.list' && \
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add - && \
    apt update && \
    apt install -y python3-colcon-common-extensions python3-pip ~nros-iron-rqt*

RUN echo "source /usr/share/colcon_cd/function/colcon_cd.sh" >> ~/.bashrc && \
    echo "export _colcon_cd_root=~/ros2_install" >> ~/.bashrc && \
    echo "source /opt/ros/iron/setup.bash" >> ~/.bashrc && \
    echo "export ROS_DOMAIN_ID=0" >> ~/.bashrc

    ENTRYPOINT ["/bin/bash"]
