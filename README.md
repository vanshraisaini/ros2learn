# ROS2Learn with Docker

This repository contains ROS 2 enabled Artificial Intelligence (AI)
and Reinforcement Learning (RL) [algorithms](algorithms/) that run in selected [environments](environments/). The repo was forked from the AcutronicRoboitcs/ros2learn and I highly encourage everyone to checkout the parent repo to learn more, especially if you want to learn how to use the repo without docker containers.

The repository contains the following:
- [algorithms](algorithms/): techniques used for training and teaching robots.
- [environments](environments/): pre-built environments of interest to train selected robots.
- [experiments](experiments/): experiments and examples of the different utilities that this repository provides.

## Pull container from docker hub
Pull the docker container containing the repo from the docker hub.

```shell
docker pull vanshrai/ros2learn
```

## Build the container
Alternatively, instead of pulling the docker image from docker hub, you can build it locally.
Please note that the building can take up to 30 minutes.
```shell
cd ~ && git clone -b staging https://github.com/vanshraisaini/ros2learn.git
cd ~/ros2learn/docker
docker build -t vanshrai/ros2learn .
```

## Setup
Create a folder where the simulation and training data will be stored.

```shell
cd ~/. && mkdir ros2_learn
```

# Start a new container

Before starting the container, move to the directory where all the data should be stored.

```shell
cd ~/ros2_learn/
```
### Run a new r2l container

```shell
docker rm r2l || true && docker run -it --name=r2l -h ros2learn -v `pwd`:/tmp/ros2learn vanshrai/ros2learn
```

### Development/Research mode
You can install new software such as file editors (e.g. `apt install nano`), which would be useful if you are trying to find the optimal parameters for a network for instance.

```shell
# Inside Docker
apt update
apt install nano
```

Make sure you save the state of your docker container before exiting it by opening a new terminal and executing:

```shell
# Get the CONTAINER ID from the IMAGE called r2l.
docker ps
# Commit changes to the r2l container.
docker commit XXXXXXX r2l
```

Example:
```shell
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
b0d8de35f133        r2l                 "bash"              2 minutes ago       Up 2 minutes        11597/tcp           wizardly_lamarr

$ docker commit b0d8de35f133 r2l
```

Next time you want to run the container you will need to launch the existing one:

```shell
docker run -it r2l
```

## Run a training script

```shell
# inside the docker container
cd ~/ros2learn/experiments/examples/MARA
python3 train_ppo2_mlp.py
```

#### Launch gzclient (GUI)

Make sure you have gazebo already installed in your main Ubuntu system and you are in the same path from which you executed the `docker run` command, that is, ~/ros2_learn folder. If you are already running the simulation in the default port, you can access the visual interface the following way opening a new terminal:
```shell
# Do not use -g --gzclient flag
cd ~/ros2_learn && git clone -b staging https://github.com/vanshraisaini/ros2learn.git
cp ~/ros2_learn/ros2learn/docker/gzclient.sh ./gzclient.sh
sh gzclient.sh
```

#### Visualize tensorboard

From your main OS, launch tensorboard pointing it to the files shared from the docker container. You can use the absolute path to any specific file or folder available in that directory.

```shell
cd ~ && git clone -b dashing https://github.com/AcutronicRobotics/ros2learn
cd ~/ros2learn/docker
sudo tensorboard --logdir=`pwd`
```
