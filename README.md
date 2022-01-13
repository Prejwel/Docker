# Docker-basics
Matrix from Hell - compatibility matrix issue 

With Docker we can run each component ( webserver , DB, messaging, Orchestration ) in a seperate container with its own dependencies and its own Libraries, all on the same VM & OS but within seperate Enviornments / Containers

Containers -completely isolated eviornments
They can have their own Processes, Services, Network Interfaces, Mounts etc but all sharing the same OS Kernal.
Docker uses LXC containers

Main purpose of Docker  - To package and containerize applications and to ship them & to run them anytime anywhere as many times as we want.

In case of Docker we have The HardwareInfracture -> over which we have the OS -> over that we have Docker installed -> Docker then manages the containers that run with Lib and dependencies alone.
Docker containers are light weight & usally in MB in size , so the boot up is faster.

DOCKER HUB
Containerized versions of applications are readily available in Docker Hub

CONTAINERS vs IMAGE
Docker Image is a package or template , 
It can be used to create one or more containers
Containers are running instances of images that are isolated and have their own set of processes

If we cant find an image , we can create one of our own and push it to docker hub repository

