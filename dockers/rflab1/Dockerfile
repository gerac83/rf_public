FROM gerac83/baselab
MAINTAINER Gerardo Aragon-Camarasa "Gerardo.AragonCamarasa@glasgow.ac.uk"

USER root

# Install gazebo
RUN sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
RUN wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
RUN apt-get update
RUN apt-get -q -y install gazebo7

RUN rm -rf /usr/share/doc/* && rm -rf /usr/share/info/* && rm -rf /tmp/* && rm -rf /var/tmp/*

RUN /bin/bash -c "mkdir -p /home/rflab/notebooks"
COPY notebooks.tar.gz /home/rflab/notebooks.tar.gz
RUN /bin/bash -c "tar -xvf notebooks.tar.gz && rm notebooks.tar.gz"
RUN /bin/bash -c "chown ${uid}:${gid} -R /home/rflab/notebooks"

USER rflab
ENV HOME /home/rflab
WORKDIR /home/rflab

RUN rosdep update && /bin/bash -c "source /opt/ros/kinetic/setup.bash" 
CMD ["bash"]
