# Run Containers with GPU Support on Ubuntu
Run a GPU enabled container on Ubuntu
[Original Reference](https://towardsdatascience.com/how-to-properly-use-the-gpu-within-a-docker-container-4c699c78c6d1)

## Ensure Base Machine has GPU support
Be able to run drivers:
* `nvidia-smi`

# Expose GPU Driver to Docker
## Use NVIDIA Container Toolkit
Base image that has been preconfigured to detect and expose GPU drivers to Docker.   \
NOTE: does not work for me, refer to NVIDIA Container Runtime.

### Dockerfile example
```
FROM nvidia/cuda:10.2-base  
CMD nvidia-smi
```

### Build Container
* `docker build . -t nvidia-test`

### Run container
Use '--gpus all' to expose GPUs:
* `docker run --gpus all nvidia-test`


## Use NVIDIA Container Runtime
Most of the time, you need different base image, cannot use NVIDIA own base image.  \
[Official Docker Documentation Link](https://docs.docker.com/config/containers/resource_constraints/#gpu)

### Add apt-get to reference proper repo.
[Link to guide.](https://www.pugetsystems.com/labs/hpc/Workstation-Setup-for-Docker-with-the-New-NVIDIA-Container-Toolkit-nvidia-docker2-is-deprecated-1568/)    \
Add apt-get to reference proper repo, then restart docker daemon to commit changes.  

```
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)

curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -

curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

sudo apt-get update

sudo apt-get install nvidia-container-toolkit

sudo systemctl restart docker
```

### Run container
Use '--gpus all' to expose GPUs:
* `docker run --gpus all nvidia-test`