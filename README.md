# Docker


## create a container in background, stop,start,detach container

docker container list

docker container ls    

docker container ls -a

docker container rm containerid

docker container rm $(docker container ls -aq)

docker container run -d -it ubuntu /bin/bash  

docker container run -it ubuntu /bin/bash

docker container stop containerid

docker container inspact containerid 
 
 # what's going on inside container
 docker container top containerid
 
 docker container stats                        :: Display a live stream of container(s) resource usage statistics



