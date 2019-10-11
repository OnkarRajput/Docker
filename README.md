# Docker Basic to Advance 

# Below is the list with a short description of some of the most used Dockerfile instructions:

# ARG 
- This instruction allows you to define variables that can be passed at build-time. You can also set a default value.

# FROM 
- The base image for building a new image. This instruction must be the first non-comment instruction in the Dockerfile. The only exception from this rule is when you want to use a variable in the FROM argument. In this case, FROM can be preceded by one or more ARG instructions.

# LABEL 
- Used to add metadata to an image, such as description, version, author ..etc. You can specify more than one LABEL, and each LABEL instruction is a key-value pair.

# RUN 
- The commands specified in this instruction will be executed during the build process. Each RUN instruction creates a new layer on top of the current image.

# ADD 
 - Used to copy files and directories from the specified source to the specified destination on the docker image. The source can be local files or directories or an URL. If the source is a local tar archive, then it is automatically unpacked into the Docker image.

# COPY 
- Similar to ADD but the source can be only a local file or directory.

# ENV 
- This instruction allows you to define an environment variable.

# CMD 
- Used to specify a command that will be executed when you run a container. You can use only one CMD instruction in your Dockerfile.

# ENTRYPOINT 
- Similar to CMD, this instruction defines what command will be executed when running a container.

# WORKDIR 
- This directive sets the current working directory for the RUN, CMD, ENTRYPOINT, COPY, and ADD instructions.

# USER 
- Set the username or UID to use when running any following RUN, CMD, ENTRYPOINT, COPY, and ADD instructions.

# VOLUME 
- Enables you to mount a host machine directory to the container.

# EXPOSE 
- Used to specify the port on which the container listens at runtime.

To, exclude files and directories from being added to the image, create a .dockerignore file in the context directory. The syntax of the .dockerignore is similar to the one of the Git’s .gitignore file.

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

## How to create Dockerfile 

 
# Dockerfile (add, copy, user) difference between copy and add in docker file

FROM ubuntu:18.04

LABEL name : "Ajay Rajput"

LABEL email : "onkar.devops@gmail.com"

ENV NAME ajay

ENV PASS password@123

RUN pwd >/tmp/test.txt

RUN cd /tmp

RUN pwd >/tmp/test1.txt

WORKDIR /tmp                   :: Define working directory

RUN pwd >/tmp/test2.txt

RUN apt-get update && apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN useradd -d /home/ajay -g root -G sudo -m -p $(echo "$pass" | openssl passwd -l -stdin) $NAME  :: add uesr and switch user

RUN whoiam > /tmp/test3.txt

USER $NAME                                               :: switch in ajay user

RUN whoami  > /tmp/test3.txt

COPY test.tar /tmp                         :: COPY only copy test.tar file to /tmp

ADD test1.tar /tmp                         :: ADD extract test1.tar to  /tmp  

CMD ["/bin/bash"]                       :: Define default command.

# Dockerfile ( Expose and create a SSH container using dockerfile )

FROM ubuntu:18.04

LABEL name : "Ajay Rajput"

LABEL email : "onkar.devops@gmail.com"

ENV NAME ajay 

ENV PASS password@123

RUN apt-get update && apt-get install -y openssh-server 

RUN useradd -d /home/ajay -g root -G sudo -m -p $(echo "$pass" | openssl passwd -l -stdin) $NAME  :: add uesr and switch user

EXPOSE 22 443 80                   :: open ports
 
 CMD ["/usr/sbin/sshd",  "-D"]                         :: Define default command.

docker image build -t ubuntu:18.04_latest .

docker container run -itd ubuntu:18.04_latest

docker container ls

# Dockerfile (Entrypoint)

FROM ubuntu:18.04

LABEL name : "Ajay Rajput"

LABEL email : "onkar.devops@gmail.com"

ENV NAME ajay 

ENV PASS password@123

RUN mkdir -p /var/run/sshd

RUN apt-get update && apt-get install -y python tee

COPY test.sh /tmp/

ENTRYPOINT ["/tmp/tesh.sh"]


# Docker Volume ( Docker Storage), mysql data persist in docker container

docker container run --name mysql_instance -e MYSQL_ALLOW_EMPTY_PASSWORD=true mysql

docker volume ls 

docker volume create abc

docker volume inspect abc

docker container run -itd -v abc:/var/lib/mysql --name mysql_instance -e MYSQL_ALLOW_EMPTY_PASSWORD=true mysql 

# Docker Volume (Remove, Prune)

docker volume rm abc

docker volume prune    :: remove unused volumes 

# Docker Bind mount

 docker container run -itd -v /home/ajay/bind/test:/temp/test --name mysql_instance  mysql 

 docker container run -itd -v $(pwd):/temp/test --name mysql_instance  mysql   :: bind your current working directory folder 

 or 

docker container run -it --mount type=bind,source= $(pwd),target=/temp/test  mysql bash

# Docker Networking (Bridge Network Overview)

docker network ls

docker network inspect bridge 

docker network create test 

docker container run -it --network=test ubuntu:18.04 bash 

#  Docker Networking (DNS Enable)

docker container run -it --network=test ubuntu:18.04 bash

hostname  

docker container run -it --network=test ubuntu:18.04 bash 
ping hostname                   :: By default domain name come with custome network already enable with custome network.

# Docker Networking (Host Network)

docker network ls

f2efa836f00e        host                host                local

docker container run -it --network=host ubuntu:18.04 bash

ifconfig   :: it will show you base host ip address range 192.168.21.1 

docker container run -itd --network=host nginx  :: http://hostip to check nginx, this type of networking all processes and pid's seprated with host network. you cann't create multipal host network.

# Docker Networking (Null Network, None Network)
this network not use for any other network. if you not mention any network name it will assign to bridge network.

docker container run -it --network=null ubuntu:18.04 bash

ifconfig  :: it would be loop back  ip address : 127.0.0.1

#  Docker Networking (Connect, Disconnect)
how to assign a multipul network name to a single container?

docker container run -it network bridge ubuntu:18.04 bash

ifconfig  :: it will show you one eth0

docker network  connect  test 2683sjbjsdw  :: it will add eth1 in '2683sjbjsdw' container

docker network  connect  test 2683sjbjsdw   :: it will remove eth1 in '2683sjbjsdw' container

# Docker Networking (Remove, Proun)

docker network rm test  :: remove test network

docker network prune :: remove unused network

# Docker Registry/Repository (Insecure)

 



































 
 



