FROM gerac83/baxtersim
MAINTAINER Gerardo Aragon-Camarasa "Gerardo.AragonCamarasa@glasgow.ac.uk"

USER root

RUN rm -rf /usr/share/doc/* && rm -rf /usr/share/info/* && rm -rf /tmp/* && rm -rf /var/tmp/*

RUN /bin/bash -c "mkdir -p /home/rflab/notebooks"
COPY notebooks.tar.gz /home/rflab/notebooks.tar.gz
RUN /bin/bash -c "tar -xvf notebooks.tar.gz && rm notebooks.tar.gz"
RUN /bin/bash -c "chown ${uid}:${gid} -R /home/rflab/notebooks"

USER rflab
ENV HOME /home/rflab
WORKDIR /home/rflab

RUN rosdep update && cd /home/rflab/ros_ws/src && git clone https://github.com/ros-planning/moveit_robots.git
RUN cd /home/rflab/ros_ws && /bin/bash -c "source /opt/ros/kinetic/setup.bash && catkin_make && catkin_make install" && rm -rf /usr/share/doc/* && rm -rf /usr/share/info/* && rm -rf /tmp/* && rm -rf /var/tmp/*
CMD ["bash"]
