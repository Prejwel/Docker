# Docker-basics
* Main purpose of Docker  - To package and containerize applications and to ship them & to run them anytime anywhere as many times as we want.
* 
Docker editions 
* community edition - set of free docker products 
* Enterprise edition - certified & supported container platform that comes with enterprise add ons ( image management, image security )

Matrix from Hell - compatibility matrix issue 

With Docker we can run each component ( webserver , DB, messaging, Orchestration ) in a seperate container with its own dependencies and its own Libraries, all on the same VM & OS but within seperate Enviornments / Containers

* Containers -completely isolated eviornments
They can have their own Processes, Services, Network Interfaces, Mounts etc but all sharing the same OS Kernal.
Docker uses LXC containers

* Main purpose of Docker  - To package and containerize applications and to ship them & to run them anytime anywhere as many times as we want.

In case of Docker we have The HardwareInfracture -> over which we have the OS -> over that we have Docker installed -> Docker then manages the containers that run with Lib and dependencies alone.
Docker containers are light weight & usally in MB in size , so the boot up is faster.

DOCKER HUB
Containerized versions of applications are readily available in Docker Hub

* CONTAINERS vs IMAGE

Docker Image is a package or template , It can be used to create one or more containers.
Containers are running instances of images that are isolated and have their own set of processes

If we cant find an image , we can create one of our own and push it to docker hub repository.

DOCKER COMMANDS
---------------
* docker run - used to run a container from an image.
docker run imageName
Eg) docker run nginx
will run an instance of nginx application on the docker host if it already exists.
If the image is not there then it will go out to docker hub & pull the iimage down ( done only the 1st time)

* ps command
will list all running containers and some basic information about them ( CID, Image Name, current status , Cname)

* docker ps -a -> will show all running & exited containers.

* docker stop CID/Cname -> to STOP a running container

* docker rm Cname/CID-> to  remove a stopped or exited container.  We can remove more than 1 container at once using a single 'rm' command.

* docker images -> to see the list of images in our host along with its sizes.

* docker rmi imagename/ImageID - > to remove an image that we no longer want to use ( we must ensure that no containers are running using that image). We must stop and delete all dependent containers if we want to delete an image.

* docker pull imagename -> to only pull the image and keep it so as to use it quickly when ever we want. 

* docker run ubuntu sleep 5 -> execution of a command when we run the container

* docker exec Cname/CID command - >  exec - to executate a command on a running container.
---

* docker run -it imagename bash 
- it imagename bash -> to be logged in to the docker container automatically.

ATTACH & DETACH mode
* in attached mode we can only see the output and cant do anything else.
* pressing Ctlr+C will exit from attach mode & we will go back to prompt
* -d -> to run the container in detached mode, in background.
* docker run -d Cname -> container will run in background, 
* docker attach CID -> to attach back to the container, to work in foreground.
---------------------
Containers are ment to run a specific task
ie: to do some sort of computation.
Once the task is complete , then the container exits.
Container lives only as long as the process inside it is alive.
--------------------
Practicals
* Ctrl+C -> stop a container
*  --name newname -> to give a name to a container along with docker run command.
* to run a specific version , we can tag that version . ( eg: redis:4.0 )
* -i -> Interactive mode-> used to Enter an input after running the container ( docker run -i imagename)
* -it -> Interactive mode & attached to the terminal
* -p -> Port maping , to be done when Container is in stopped state.
* ports exposed to the container can be seen after  ' -> '
* ports published on the host, cen be seen before '-> '
* -v -> Volume Maping
* logs -> to get logs -> docker logs CID/CName
* inspect -> for more info about container. ( docker inspect CID )
* To tag, use ' : ' after imagename . ( docker run imagename:tagname )
