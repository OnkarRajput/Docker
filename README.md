# Docker Basic to Advance 


## create a container in background, stop,start,detach container

Usage:	docker container COMMAND

docker container list

docker image ls

docker container ls    

docker container ls -a

docker container rm 8e76cf05adee

docker container rm $(docker container ls -aq)

docker container run -d -it ubuntu /bin/bash  

docker container run -it ubuntu /bin/bash

docker container stop 8e76cf05adee 

docker container start 8e76cf05adee                     :: start stopped container

detach container Ctrl+p+q

 # what's going on inside container
 docker container top 8e76cf05adee                         :: Display the running processes of a container
 
 docker container stats                                    :: Display a live stream of container(s) resource usage statistics
 
 docker container inspact 8e76cf05adee                     :: Display detailed information on one or more containers

docker container logs 8e76cf05adee                         :: Fetch the logs of a container
      
# Docker port mapping, rename container, restart container, exec container
 
 docker container run -d -p 80:8081 --name test_nginx nginx       :: run nginx container with port 80 to 8081 name  test_nginx
 
 docker container exec -it 8e76cf05adee /bin/bash                 ::  login in existinf running instance 
 
 docker container rename  8e76cf05adee newtest_nginx       :: rename your existing container name test_nginx to newtest_nginx
 
 docker container restart  8e76cf05adee                    :: restart existing container
 
# Attach to running container, kill, wait, pause, unpause, prune, port
  
docker container attach 8e76cf05adee              :: attach container inside the env.
  
docker container kill 8e76cf05adee                :: kill container immediately
 
docker container wait 8e76cf05adee                 :: waiting  to container stop 
 
docker container stop 8e76cf05adee                  :: stop container wiith soft way
 
docker container pause 8e76cf05adee                 :: Pause resources for your container
 
docker container unpause 8e76cf05adee                :: unpause your container resources 
 
docker container prune                               :: delete your all stopped containers
 
docker container port container_id/container_name      :: check the bind port with your host machine 
 
 # create docker container, diff docker container and copy file into container
 
docker container diff 8e76cf05adee         :: It'll show you modify files system inside container files/directories (A : add, C: create, D: delete)

watch 'docker container diff 8e76cf05adee'  :: watch modify files in container 

docker container cp /tmp/abc.txt 8e76cf05adee:/tmp/    :: copy file into container

docker container attach 8e76cf05adee           :: check copied files inside container

# Export/Import docker container

docker container export 8e76cf05adee > export_image.tar     :: Export your container images with .tar file

docker container export 8e76cf05adee -o  export_image.tar   :: Export your container images with .tar file

docker image import export_image.tar new_export_image        :: import .tar file imange as conatiner 

docker image  ls | grep new_export_image 

docker container run  -it new_export_image /bin/bash        :: to run the new_export_image 


# how to create docker image from running container (docker commit)

docker container commit --author "Ajay Rajput" -m "this is new test image" 8e76cf05adee new_commit_images  :: commit image

docker container run -it new_commit_images /bin/bash


# How to push image on docker hub, image tag, image pull, docker login

docker pull ubuntu:18.04             :: pull image from docker hub with sepific tag like :18.04

docker image tag ubuntu:18.04 onkardevops/ubuntu:18.04_latest :: tag exist ubuntu:18.04 image

docker login

docker push onkardevops/ubuntu:18.04_latest         :: push on github account

docker pull onkardevops/ubuntu:18.04_latest          :: download in your system


# How to inspect remove,inspect, list and history for the docker image
docker images ls --format '{{.ID}} , {{.Repository}}  -{{.Tag}}'    :: view image by id, repo & Tag

docker image history ubuntu                                          :: check history on ubuntu image

docker image rm ubuntu:18.04

docker image inspect ubuntu | less 

docker image prune


# Docker save / docker load. Diff between export and save & load &import

docker image save kibana > kibana.tar  :: svae as standred  output (save all parent layer, save tag, name version, repos, all info etc..)

docker image load  < kibana.tar         :: ipmort as standrrad input (import all parent layer, save tag, name version, repos, all info etc..)) 

docker image import     :: single layer without all parent layer, save tag, name version, repos, all info etc..

docker container expot :: save only one layer without taking volume backup 

## Dockerfile

 
# Dockerfile (add, copy, user) difference between copy and add in docker file





















 
 



