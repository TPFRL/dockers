# dockers
Automatically sets environment I prefer on given docker

### Requirements
Must install [nvidia-docker](https://github.com/NVIDIA/nvidia-docker#ubuntu-16041804-debian-jessiestretch) first.

### Instructions
```
cd [DOCKER_YOU_WANT]

docker build -t [IMAGE_NAME] .

docker run --runtime=nvidia --ipc=host --name=[CONTAINER_NAME] -v [HOST_DATA_PATH]:/data -v [HOST_CODE_PATH]:/workspace  -it [IMAGE_NAME]
```
