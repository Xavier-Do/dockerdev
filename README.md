DockerDev
---------

A tool to easily build and run runbot docker images locally

Setup
-----

Clone this repository

```bash
git clone https://github.com/Xavier-Do/dockerdev
```

Install required packages 
```bash
    sudo apt-get install docker.io python3-docker
    sudo adduser $USER docker
    su $USER # relog to apply group changes
```

Check that your user can user docker

```bash
    docker ps
```

Building images
---------------

You can then build some runbot images

```bash
    docker_build master
    docker_build 16.0
    docker_build odoo:PureBookworm
```

After the first execution, a file `custom_layers` is created
This file can be customized to your need to add tooling in the docker image. The base version adds ipython, git and pick


Running images
--------------

You can then easily start a docker using the dock script

```bash
    dock 16.0
```

**Warning**: this version of the scripts mounts the postgresql socket inside the docker, but also your **home directory**
This is practical for devlopment if your sources are inside the home directory, and it will also allow you to have the same bashrc inside the docker. But this also means that any operation on your home directory will be applied outside the docker. This also means that your ssh keys are visible inside the docker.

Optional setup
--------------

You can add this folder in your path or create symlink in your bin directory

```bash
ln -s "$(pwd)/dock" /home/$USER/bin/dock
ln -s "$(pwd)/docker_build" /home/$USER/bin/docker_build
```

It is adviced to customize your shell to indicate that you are inside a docker it it doesn't contains the hostname. 

Example:

```bash
hostname=$(hostname)

if [ "$hostname" != "your_hostname" ]; then
    PS1="DOCKER ${DOCKERTAG} -- $PS1"
fi
```

were `your_hostname` is the base name of your machine