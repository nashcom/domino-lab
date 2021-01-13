# Install a SSH Client

## On Windows use Putty or better MobaXterm

Connect to the server using the private key .ppk specified in the SSH Advanced key settings

## On Linux or OSX use ssh

* Ensure the file is only readable by the user  
* specify root@ to ssh doesn't assume your local user
* specify the private key


```
chmod 400 id_escsa.pem
ssh root@master.domino-lab.net -i id_escsa.pem
```

## Prepare the local environment 

## Create your work directory

```
mkdir -p /local/software
cd /local/software
```

# Install Docker 20.10

This command takes a time and installs the current Docker 20.10 with all dependencies.  
Don't PANIC! No output is generated for a while

```
curl -fsSL https://get.docker.com -o get-docker.sh
chmod 755 get-docker.sh
./get-docker.sh

```

## Enable and start Docker

```
systemctl enable --now docker
```

* Install Git
* Clone Domino Docker repository

```
yum install -y git

mkdir -p /local/github
cd /local/github
git clone https://github.com/IBM/domino-docker.git

cd domino-docker
git checkout develop

```


## Check Docker Version and installation

* Check version
* Run the hello-world image in your first container

```
docker version

docker run hello-world

```

## Run the CentOS Base image

```
docker run --rm -it centos:latest bash
```


## Install Docker-Compose

```
curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose

```

## Check Docker Compose version

```
 docker-compose version
 ```


## Create a normal user and group ( notes:notes )

* Creates the user with ID 1000 (first free user)
* Sets the password for notes user with prompt

```

adduser notes -U
passwd notes

```

## Copy Domino Docker image and import it into Docker host

* All software is located on the master server
* One time copy for the whole workshop


```
scp notes@master.domino-lab.net:/local/software/* /local/software

Password for notes user: xxxx
```

## Upload the Domino image to docker host

The image comes as a compressed tar and needs to be uploaded

```
docker load --input Domino_1101FP2_DockerImage.tgz
```

Reference: https://help.hcltechsw.com/domino/earlyaccess/inst_dock_load_tar_archive.html


Congrats!  
This completes your Docker environment preparation.


# Docker-Compose Examples

The following files are Docker compose examples to run containers with different settings from the YML files provided.

```
cd /local/github/domino-docker/examples/docker-compose
```

Take look into the example

```
vi docker-compose.yml
```

Oops maybe you want an easier editor?  
Tip: Install midnight commander and use mcedit

```
yum install -y mc

mcedit docker-compose.yml

```

```
## Start the container: (-d starts the container in back-ground)

docker compose-up
```
