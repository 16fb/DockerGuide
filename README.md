# Poly Kid Guide to Containers and Docker
DISCLAIMER:
* This will be an overly simpliflied explanation
* Refer to documentation and references for a full understanding
* This is basically a guide i would write for the struggling poly kid i was 4 mth ago.

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
* "Emulate" processes
* Very little resource overhead

### How to think about containers.
A method to ensure whatever runs on system A, will run on system B.
Achieved by having system "run" an OS as a native process. Be able to interact with the OS as if its a different computer.
"Builds the entire OS and the dependacies needed"


The main benefit of containers is isolation, <br> 
allowing us to **package an application with all of its dependencies into a standardized unit.** <br>
In essence, we can put our setup into the container (such as installing dependacies), and it will work anywhere.<br>

The most popular containerisation software is [Docker](https://en.wikipedia.org/wiki/Docker_(software)). <br>
However for High Performance Computing(HPC) in scientific context, [Singularity](https://en.wikipedia.org/wiki/Singularity_(software)) is a popular option. <br>



# TODO STUFF TO WRITE
DockerHub
.dockerignore
docker buildx
diff arch
GPU support in containers.