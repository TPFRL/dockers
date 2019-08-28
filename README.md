# dockers
Automatically sets environment I prefer on given docker

### Requirements
Updated : install Docker and nvidia-driver. that's all

### Instructions
```
cd [DOCKER_YOU_WANT]

docker build -t [IMAGE_NAME] .

docker run --ipc=host -p [HOST_PORT_NAME_FOR_DOCKER]:7777 --name=[CONTAINER_NAME] -v [HOST_DATA_PATH]:/data -v [HOST_CODE_PATH]:/workspace  -it [IMAGE_NAME]
```

for example,
```
cd pytorch

docker build -t torch120 .

docker run --ipc=host -p [HOST_PORT_NAME_FOR_DOCKER]:7777 --name=test_torch -v /hdd/data:/data -v /home/user:/workspace -it torch120
```
