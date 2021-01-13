# Poly Kid Guide to Containers and Docker
DISCLAIMER:
* This will be an overly simpliflied explanation
* Refer to documentation and references for a full understanding
* This is basically a guide i would write for the struggling poly kid i was 4 mth ago.

### Excelent Resources / other guides.
* 

## Containers
[Containers](https://en.wikipedia.org/wiki/OS-level_virtualization) allows for OS-level virtualisation.  
Basically its a Virtual Machine that virtualises processes and not the whole computer, which makes it much more efficient.  
Containers were initially made for Linux, therefore most containers will be linux based.

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

### WSL2
Windows Subsystem for Linux, basically aims to have windows be able to run Linux "natively".  
As of WSL2, they had decided on using a lightweight VM.  

I would reccomend you use this to run containers, good choice if you do not have a spare laptop with linux to use.  

Resources:
* [Official Windows Guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
* [Another Guide](https://www.sitepoint.com/wsl2/)
## Building + Running docker containers 
People have made many guides, heres some of them, find other favourites
* [Learning docker by making web app](https://youtu.be/gAkwW2tuIqE)
* [Docker page official guide](https://docs.docker.com/get-started/)
* Pull and run the basic docker container [hello-world](https://hub.docker.com/_/hello-world?tab=tags&page=1&ordering=last_updated)

When in doubt, ask the reference:
* https://docs.docker.com/engine/reference/run/

### Building Docker Image
How Image Layers work:
* After each dockerfile command, a new read-only layer is created 
* Final top layer is a modifiable layer
* Idea: different images can share lower level layers.

Best Practices:
* Reduce number of dockerfile commands, put more commands into same dockerfile command.
* If unsure, Test commands using `docker exec / run`, write down all commands used.
* Then, implement commands in dockerfile.
### Typical Docker Commands
List of all common docker commands:
[Reference](https://docs.docker.com/engine/reference/run/)

docker run:
* Run a container
* `$ docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]`  
[Reference](https://docs.docker.com/engine/reference/run/)

docker stop:
* Stop a running container
* `docker stop [OPTIONS] CONTAINER`  
[Reference](https://docs.docker.com/engine/reference/commandline/stop/)

docker exec:
* runs a new command in a running container
* `docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`  
[Reference](https://docs.docker.com/engine/reference/commandline/exec/)

docker build:
* Build an image from dockerfile
* `docker build [OPTIONS] PATH | URL | -`  
[Reference](https://docs.docker.com/engine/reference/commandline/build/)

docker pull:
* Pull an image or a repository from a registry
* `docker pull [OPTIONS] NAME[:TAG|@DIGEST]`  
[Reference](https://docs.docker.com/engine/reference/commandline/pull/)

docker push:
* Push an image or a repository to a registry
* `docker push [OPTIONS] NAME[:TAG]`  
[Reference](https://docs.docker.com/engine/reference/commandline/push/)

**Container and Image management**

docker ps:
* List containers
* `docker ps [OPTIONS]`  
[Reference](https://docs.docker.com/engine/reference/commandline/ps/)

docker images:
* List images
* `docker images [OPTIONS] [REPOSITORY[:TAG]]`  
[Reference](https://docs.docker.com/engine/reference/commandline/images/)

docker image:
* Manage images
* `docker image COMMAND`  
[Reference](https://docs.docker.com/engine/reference/commandline/image/)

docker image rm:
* Remove one or more images
* `docker image rm [OPTIONS] IMAGE [IMAGE...]`  
[Reference](https://docs.docker.com/engine/reference/commandline/image_rm/)

**Save and Load image from .tar file**

docker save:
* Save one or more images to a tar archive (streamed to STDOUT by default)
* `docker save [OPTIONS] IMAGE [IMAGE...]`  
[Reference](https://docs.docker.com/engine/reference/commandline/save/)

docker load:
* Load an image from a tar archive or STDIN
* `docker load [OPTIONS]`  
[Reference](https://docs.docker.com/engine/reference/commandline/load/)

**Advanced**

docker buildx:
* Build with BuildKit, X-perimental builder. Typically used for cross compilation
* Complex, but good to use for x-compilation. Double check containers are proper architecture.
* `docker buildx COMMAND`  
[Reference](https://docs.docker.com/engine/reference/commandline/buildx/)

docker commit:
* Create a new image from a container’s changes, aka save a running container as a new image.
* Not Reccomended, its reccomended that changes to containers be done in a dockerfile for consistency.
* `docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]`  
[Reference](https://docs.docker.com/engine/reference/commandline/commit/)

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


## Buildx
Experimental builder tool, can be used to cross compile and put multiple images into same tag on dockerhub.  
Has other uses as well.

Some Guides to get started:
* [Docker official guide](https://docs.docker.com/docker-for-mac/multi-arch/)
* [Guide i personally started learning from](https://www.padok.fr/en/blog/multi-architectures-docker-iot)
* [Guy who explains multi-arch](https://medium.com/icetek/understanding-how-docker-multi-arch-images-work-9a7e035e2868)



## GPU Support
Windows 10:  
As of writing(13/1/2021), stable version of WSL2 with docker does not support GPU Usage(GPU Passthrough).  
There is a preview / insider build for windows that does allow GPU usage.  
Hopefully by the time you read this, the preview build will have been pushed to live.  

Ubuntu/Mac:
Possible, refer to `dockerOnUbuntu.md` and `dockerWithGPUOnUbuntu.md` for more details.
# TODO STUFF TO WRITE
DockerHub -> Done  
Building + Running Docker containers -> Simple one done
docker and WSL2 
typical docker commands: -> done
image management commands: -> done
how docker takes up space on your computer in windows -> referenced guide
docker layers -> done
.dockerignore -> mentioned somewhere
docker buildx -> done
diff arch -> Mentioned
GPU support in containers. -> done