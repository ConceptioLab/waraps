![MainBranchNOLRS2](https://github.com/CentroEspacialITA/waraps/actions/workflows/docker-image-nolrs2.yml/badge.svg?branch=main)
![MainBranchDeepracer](https://github.com/CentroEspacialITA/waraps/actions/workflows/docker-image-deepracer.yml/badge.svg?branch=main)
[![Docker Image CI (REMOTEID)](https://github.com/CentroEspacialITA/waraps/actions/workflows/docker-image-remoteid.yml/badge.svg?branch=main)]

# LRS2
LRS2 fork as a docker image.

![image](https://github.com/CentroEspacialITA/waraps/blob/main/doc/readme_img/container.svg)

# 1. Introduction

This repository should be used for all CONCEPTIO agents willing to test and connect to the WARA-PS/LRS2 arena[^1]. 

Presently there is no docker image for LRS2, so the Dockerfile provided here uses osrf:ros-humble-desktop as a base image, copies all directories from "lrs2" (which are submodules) to the image, sources the ROS 2 installation and compiles all LRS2 packages. 

[^1]: Actually, the LRS2 repository is not exactly the WARA-PS arena, which seems to be using ROS1 repositories... we must confirm this with the swedish side. 

## Docker 101
A docker container is like a virtual machine running an Operating System with preinstalled software. It is used to quickly run applications that rely on specific libraries without spending time configuring the environment. That way, new agents can be added to the arena as quickly as possible. If your ROS2 node/package uses a specific library, you can also add it to the docker image. 

You can either build the image yourself or download the image and create a new Docker container to run it:

# 2. Building the image (Windows WSL2/Raspberry Pi)

1. Download [Docker](https://www.docker.com/) (Raspbian/Debian instructions [here](https://docs.docker.com/engine/install/debian/)).
2. Clone this repository using [GitHub Desktop](https://desktop.github.com/) or [git](https://git-scm.com/), by running the ```git clone https://github.com/CentroEspacialITA/waraps.git``` command. If you are on Raspberry Pi, control it via SSH and follow the instructions [here](https://stackoverflow.com/questions/2505096/clone-a-private-repository-github) to generate a token for GitHub.
3. To fetch LRS2 packages, open the root cloned folder and run ```git submodule init``` followed by ```git submodule update --remote```. This will get the most up-to-date packages from the swedish side.
4. Run ```docker build -f docker/nolrs2.dockerfile . -t mvccogo/conceptio:nolrs2``` or ```docker build -f docker/deepracer.dockerfile . -t mvccogo/conceptio:deepracer``` to start building the image for your architecture (ARM64 for RPI, AMD64 for x86_64). Don't forget the ```.```!


# 3. Downloading the image (Recommended for RPI)
Building the linux/arm64 image takes a looooooong time, so it is advisable to simply download the Docker image from the Conceptio Docker Hub repository. 
1. Download [Docker](https://www.docker.com/). (Raspbian/Debian instructions [here](https://docs.docker.com/engine/install/debian/)).
2. Run ```sudo docker pull mvccogo/conceptio:deepracer``` or ```sudo docker pull mvccogo/conceptio:nolrs2```.
   
Note: use ```sudo``` only in RPI.

# 4. Using the arena
On the root cloned folder, start the container with ```sudo docker run -ti --network host mvccogo/conceptio:nolrs2``` or ```sudo docker run -ti --network host mvccogo/conceptio:deepracer```

To run another terminal in the same container, execute ```sudo docker exec -ti <container_name> bash```.

You can check the list of containers running using ```sudo docker ps```.

Note: use ```sudo``` only in RPI.

Check [lrs_doc](https://gitlab.liu.se/lrs2/lrs_doc) section 2.2 for more info.

By default, LRS2 workspace is at the /opt/lrs2 folder and CONCEPTIO workspace is at /opt/conceptio. ROS2 is installed in /opt/ros. 

# 5. Contributing to the image
To contribute to the image, simply follow the [Dockerfile documentation](https://docs.docker.com/engine/reference/builder/). 

Upon commiting to this repo, a workflow will start that will automatically push the newest image to Docker Hub.




# Roadmap for september
- [X] Run arena locally.
- [ ] Create topics for UTM. (Ongoing with [br-utm](https://github.com/CentroEspacialITA/br-utm))
- [ ] See arena agents in VR-Forces.
- [ ] Add an agent to the arena.
- [ ] Control a real (live) agent and see the behavior in Gazebo/Rviz/VR-Forces

