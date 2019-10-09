# Docker


## create a container in background, stop,start,detach container

docker container list

docker container ls    

docker container ls -a

docker container rm 8e76cf05adee

docker container rm $(docker container ls -aq)

docker container run -d -it ubuntu /bin/bash  

docker container run -it ubuntu /bin/bash

docker container stop 8e76cf05adee .         

docker container inspact 8e76cf05adee                                :: Display detailed information on one or more containers

docker container inspact 8e76cf05adee                                :: Fetch the logs of a container

 # what's going on inside container
 docker container top 8e76cf05adee                                     :: Display the running processes of a container
 
 docker container stats                                    :: Display a live stream of container(s) resource usage statistics
      
 



