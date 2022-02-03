# Docker
* Main purpose of Docker  - To package and containerize applications and to ship them & to run them anytime anywhere as many times as we want.

Docker editions 
* community edition - set of free docker products 
* Enterprise edition - certified & supported container platform that comes with enterprise add ons ( image management, image security )

Matrix from Hell - compatibility matrix issue 

With Docker we can run each component ( webserver , DB, messaging, Orchestration ) in a seperate container with its own dependencies and its own Libraries, all on the same VM & OS but within seperate Enviornments / Containers.

* Containers -completely isolated eviornments
They can have their own Processes, Services, Network Interfaces, Mounts etc but all sharing the same OS Kernal.
Docker uses LXC containers

* Main purpose of Docker  - To package and containerize applications and to ship them & to run them anytime anywhere as many times as we want.

In case of Docker we have The HardwareInfracture -> over which we have the OS -> over that we have Docker installed -> Docker then manages the containers that run with Lib and dependencies alone.
* HW-> OS -> Docker  -> Container
* Docker containers are light weight & usally in MB in size , so the boot up is faster.

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
Practice
* Ctrl+C -> detach
*  --name newname -> to give a name to a container along with docker run command.
* to run a specific version , we can tag that version . ( eg: redis:4.0 )
* -i -> Interactive mode-> used to Enter an input after running the container ( docker run -i imagename)
* -it -> Interactive mode & attached to the terminal
* -p -> Port maping , to be done when Container is in stopped state. ( -p [HostPort]:[ContainerPort] )
* ports exposed to the container can be seen after  ' -> '
* ports published on the host, cen be seen before '-> '
* -v -> Volume Maping
* logs -> to get logs -> docker logs CID/CName
* inspect -> for more info about container. ( docker inspect CID ) , We can find Env variables using INSPECT cmd., Network details etc
* To tag and name during docker run, use ' : ' after imagename . ( docker run imagename:tagname )
* -t -> to tag
* docker history
* -e  -> to change env variables
* --link ->cmd line option to link 2 containers together.
* --name=newname ( docker run -d --name=redis redis )
* -v
* network create ( cmd to create our own private network ). Folowed by  driver & subnet & custom isolated network name.
* docker network ls ( lists all networks )
* -network=Networkname ( to attach to a network )
* --driver
* --subnet
* --gateway
* --restart=always 
* curl -X GET localhost:5000/v2/_catalog  ->list of pulled ,tagged, pushed images  can be found here
* docker image prune -a ( remove dangling images)
* docker image ls  -> lists all images
------------
DOCKER FILE 
* Docker file contain INSTRUCTIONs & ARGUMENT
* From Base OS
* Run -> instructs docker to to run command on base OS
* Copy -> copies file from local system to docker image.
* EntryPoint -> allows to specipy a cmd that will run when the image runs as a container

Layered architecture - if any issue we can start from a particular step instead of starting all over again.
Rebuilding a layer is easy since it will reuse previous steps from cache.
-------------------------
Docker file , Docker build
* docker build -> go to docker file directory , use cmd ( docker build . ), use -t to name it during docker build, use  ' : ' to tag.
* build , name , tag, , use as image, run container
* to see base OS of image-> docker run image cat /etc/*release*
* env field of container can be seen using ( docker exec -it containerName env ), env variabkles can be changed using -e

---------------------------------------
DOCKER COMPOSE

Using docker compose ,we can create a config file in yaml format and put together the different services & options (key) specific for running them. 
Docker-compose up,  will bring up the application stack.

Docker compose file 
1) create a dictionary of container name ( Names- used as key ), (eg : redis)
2) under each container item, specify the image to be used, ( image is the key here) ( image: redis)
2a) if we need to instruct docker compose to run docker build instead of trying to puull an image, then use 'build' .  ( build : ./location )
4) move the ports under the respective containers ( Key :ports ) , ( ports: -5000:80 )
5) move the links (links : -redis -db )
Once done 
* docker-compose up -> to bring up the application stack

Make sure to give the spaces / Tabs properly in docker compose file

--------------
Docker compose
* 3 versions 

* version 1 - no way to specify the order/ dependency in which containers should run.
* version 2 - have the property Services , we need to specify version: 2
here docker compose creates a dedicated bridge network for the applications and attaches all containers to new network.As a result we dont have to use link cmd here.
Depends on Featue-> depends_on: -redis
* version 3 - docker swarm support, specify version 3
Front end & back end networks 
specify using the key networks: ( networks: -front-end, -back-end )
-------------------------------------------------------------------
DOCKER ENGINE
* host with docker installed on it.
* by default Docker engine interacts with docker host
------------------------
* Docker in Windows & Mac
* Docker deamon - background process that manages docker objects ( images, containers )
* Rest API - Docker rest Api server is the api interface that can be used by programs to talk to deamon.
* Docker CLI - cmd line interface used to run ,stop etc ... with containers 
* Docker toolbox
* Docker desktop for windows
* ---------------------

* PID Namespace -> each process can have multiple PIDs associated with id.
* cgroups - Control groups , used by docker to restrict the amt of hardware resource allocated to each container.
* Docker default storage location - /var/lib/docker
* mounting ( -v )
* volume mounting-> mounts a volume from Volume dir
* Bind mount- mounts a dir from any location on docker host
* docker run -v destinatioin:source
* Docker uses storage drivers to enable layered architecture.
---------------------------
Networking
* 3 networks are created automatically when docker is installed. ( Bridge , None , Host )
* Bridge - default network. Private NW 
* to associate the container with other networks we need to specify the network name.

* None - ( --network=none )
* Host - ( --network=host )
* Containers inside docker host can resolve each other using container name.
* --network=Networkname -> (to attach to a network )
* docker network create NWname -> ( to create new network )
* --driver
* --subnet
* --gateway
-----------------------------
DOCKER REGISTRY
* Central repo of all Docker images
* docker.io
* Its possible to make repository as private also 
* to login there  ( docker login private-registry.io ) , Give creds after this
* ( docker image tag my-image localhost:5000/my-image)
* docker push localhost:5000/my-image
* docker pull localhost:5000/my-image ( give IP of docker host instead of localhost if we are accessing from another host)
* --restart=always
* curl -X GET localhost:5000/v2/_catalog  -> list of pulled ,tagged, pushed images  can be found here
*  localhost:5000 -> registry address

----------------------------
CONTAINER orchestration solutions
* Docker swarm
* Kubernetes
* Mesos
---
cluster - set of nodes
