# Installing Docker On Linux
## Original Guide
[Original Docker Documentaion](https://docs.docker.com/engine/install/ubuntu/)

### What it seems to be doing
Tell 'apt-get' about docker repo, and verify it.
Then download docker from docker repo.

### Last Updated
2021/1/6 2:26

## Steps
### Uninstall old versions
`$ sudo apt-get remove docker docker-engine docker.io containerd runc`

# Installation methods
## Install using the repository
### SET UP THE REPOSITORY
Update the apt package index and install packages to allow apt to use a repository over HTTPS
```
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

### Add Docker’s official GPG key:
Add the GPG key.
* `$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`

### Verify fingerprint
* `$ sudo apt-key fingerprint 0EBFCD88`
* 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88

### Set up stable repository
```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

### Install Docker Engine
Update the apt package index, and install the latest version of Docker Engine and containerd, or go to the next step to install a specific version:
* `$ sudo apt-get update`
* `$ sudo apt-get install docker-ce docker-ce-cli containerd.io`

### Verify Docker Works
* `$ sudo docker run hello-world`

## Future Updates
Docker will be updated.
`sudo apt-get update`
`sudo apt-get upgrade`

# Post install, manage docker as non-root user.
Have not done this to alienware laptop, will stick with sudo for now: TODO. \
[Link to documentation](https://docs.docker.com/engine/install/linux-postinstall/)