In this project, I will use ansible on a host and use centos-based containers as target hosts to automate a simple application deployment, play with different modules, ....

Playbooks and file will be continuesly improved according to best practices. 


__WARNING:__ USE THIS INSTRUCTION WITH CARE! THE BELOW IMAGES ARE TO BE USED FOR TEST PURPOSES ONLY AND SHOULD NOT BE YOUR REFERENCE FOR PRODUCTION ENVIRONMENT!

# Table of Content

- [Table of Content](#table-of-content)
  - [Pre_requirements](#pre_requirements)
    - [Usage:](#usage)
  - [1. web_deployment](#1-web_deployment)
  - [2. play_with_ansible](#2-play_with_ansible)

## Pre_requirements
In order to use containers as target hosts and manipulate services via service module, they need to be reachable via **SSH** and **systemd** should be activated. The corresponding images are stored in my [docker_hub-centos-ssh-enabled](https://hub.docker.com/r/mohammad67/centos-ssh-enabled) and [docker_hub-ubuntu20-ssh-enabled](https://hub.docker.com/r/mohammad67/ubuntu20-ssh-enabled).

The Docker file to create these images are also provided in this repository.

### Usage:
This image has systemctl feature and openssh server feature all setup. All you have to do is

Build the image:
'''
docker build -t IMAGE_NAME:TAG .
'''

Then, create the container with ports 80 and 22 open, privilaged access, and a map of files in the cgroup:
'''
docker run -d --privileged -v /sys/fs/cgroup:/sys/fs/cgroup:ro -p 80:80 -p 2222:22 IMAGE_NAME/TAG 
'''

or, if one wants to open the port for only an IP-Address, should run:
'''
docker run -d --privileged -v /sys/fs/cgroup:/sys/fs/cgroup:ro -p IP_ADDRESS:80:80 -p IP_ADDRESS:2222:22 IMAGE_NAME/TAG 
'''

__NOTE:__ In case of getting an error like: REMOTE HOST IDENTIFICATION HAS CHANGED!, you can solve the issue by deleting the *keys* inside the *.ssh/known_hosts* or simply deleting the whole file.


## 1. web_deployment
     - install required packages
     - configure mysql database and web_app
     - deploy database and application
## 2. play_with_ansible
     - use files module to create a file and directory
     - use service module to start httpd ad firewalld