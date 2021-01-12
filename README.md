# Poly Kid Guide to Containers and Docker
DISCLAIMER:
* This will be an overly simpliflied explanation
* Refer to documentation and references for a full understanding
* This is basically a guide i would write for the struggling poly kid i was 4 mth ago.

### Excelent Resources / other guides.
* 

## Containers
[Containers](https://en.wikipedia.org/wiki/OS-level_virtualization) allows for OS-level virtualisation. <br>
Basically its a Virtual Machine that virtualises processes and not the whole computer, which makes it much more efficient.

## Benefit + Use case of containers
Main benefits:
* Run an application with libraries, dependacies all pre-loaded.
* Ensure application consistency. 
IE, if it runs on my system A, it **should** run on system B. (with some caveats)

### Comparison to Virtual Machines(VMs)
Virtual Machines:
* Emulate entire system
* Very resource intensive

Containers:
* "Emulate" processes (Are native processes that emulate other OS)
* Very little resource overhead

### How to think about containers.
A method to ensure whatever runs on system A, will run on system B.   \
Achieved by having system "run" an OS as a native process. Be able to interact with the OS as if its a different computer.   \
You take an OS, tell docker how to build + modify it, untill you get a usuable program.


The main benefit of containers is isolation,  \
allowing us to **package an application with all of its dependencies into a standardized unit.**   \
In essence, we can put our setup into the container (such as installing dependacies), and it will work 'anywhere'.  


### Popular Container Software
The most popular containerisation software is [Docker](https://en.wikipedia.org/wiki/Docker_(software)).  \
However for High Performance Computing(HPC) in scientific context, [Singularity](https://en.wikipedia.org/wiki/Singularity_(software)) is a popular option.   

### Docker nomenclature
* dockerfile -> List of instructions on how to build an image
* Image -> Image built using dockerfile
* Container -> Image that is running
* Docker Daemon -> Docker "program/runtime". Must be installed + running to dun docker.
* DockerHub -> Online Repository for docker images. Think github but for docker.
* .dockerignore -> Docker version of .gitignore, choose what dockerfile should ignore.

### How docker is used, usually.
1. Define your `dockerfile`, define how you want your image to be built.
2. Build your image, usually takes awhile.
3. Obtain completed docker image.
4. Run the docker image locally.
5. Push docker image to DockerHub.
6. Pull docker image on machine 2.
7. Run the docker image on machine 2.

## Building + Running docker containers 
People have made many guides, heres some of them, find other favourites
* [Learning docker by making web app](https://youtu.be/gAkwW2tuIqE)
* [Docker page official guide](https://docs.docker.com/get-started/)
* Pull and run the basic docker container [hello-world](https://hub.docker.com/_/hello-world?tab=tags&page=1&ordering=last_updated)

When in doubt, ask the reference:
* https://docs.docker.com/engine/reference/run/

### Building Docker Image
TODO: Best pratices
TODO: how image layers work.

### Typical Docker Commands
TODO: all the commands

List of all docker commands:
[Reference](https://docs.docker.com/engine/reference/run/)

docker run:
* Run a container

docker stop:
* Stop a running container

docker exec:
* runs a new command in a running container

docker build:

docker pull:

docker push:


docker ps:

docker images:

docker image:

docker image rm:


docker save:    

docker load:


docker buildx:

docker commit:



## Why can docker work / how docker works internally.
Instruction Set Architecture:
* Ensures CPU with the same architecture will be able to run the same software.
[Wiki](https://en.wikipedia.org/wiki/Instruction_set_architecture)  

How the magic works:
* Programs are compiled to only run on 1 Specific OS and 1 Specific Architecture.
* Docker daemon abstracts away the Operating System -> OS-level virtualisation.
* Therefore, **as long architecture is the same, docker image can run.**
### WHAT YOU NEED TO KNOW
As long architecture is the same, Machine will be able to run the docker image.
If not, have to use a VM or emulation technique.

Proper References for Deeper Reading:
* [Short Youtube series digging around docker](https://www.youtube.com/watch?v=-YnMr1lj4Z8)

## Using DockerHub
Use dockerhub to upload containers for future use and easy access.
### References
Official Guide: [Docker Hub guide](https://docs.docker.com/docker-hub/)

### DockerHub naming scheme
Docker has an official naming scheme, you use this push and pull docker images.   \
* `<docker_ID>/<repo_name>:<desired_tag>`

### Pull from repo:
* `docker pull <docker_ID>/<repo_name>:<desired_tag>`
* `docker pull hello-world`

Pull an official repo, only referencing repo name:
* `docker pull python`

Pull a normal repo, specify docker_ID and repo name:
* `docker pull continuumio/anaconda3` [Auto pulls :latest]

Pull a specific tag, specify tag:
* `docker pull continuumio/anaconda3:latest`

Pull a specific image, specify image hash:
* `docker pull continuumio/anaconda3:2020.11@sha256:0b2047cdc438807b87d53272c3d5b10c8238fe65a2fedf9bd72de0b7ba360cb1` 
[Always pull specific image]

### Push to repo:
Build your image:
* `docker build -t <your_docker_ID>/<your_repo_name>:<desired_tag> .`
* `docker build -t 16fb/deepheadpose:ZX .`  
Ensure your docker image follows DockerHub format, if not retag your image.

Push to DockerHub:
* `docker push <your_docker_ID>/<your_repo_name>:<desired_tag>`
* `docker push 16fb/deepheadpose:ZX`

## Moving docker images install location on Windows 10 using WSL2
Follow this [StackOverflow Guide](https://stackoverflow.com/a/63752264/11652692).   
Very usefull and helpful when you C: drive is out of space.
# TODO STUFF TO WRITE
DockerHub -> Done  
Building + Running Docker containers
docker and WSL2 
typical docker commands:
image management commands:
how docker takes up space on your computer in windows -> referenced guide
docker layers
.dockerignore
docker buildx
diff arch -> Mentioned
GPU support in containers.