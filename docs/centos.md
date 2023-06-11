
# CentOS Stream 9

First of all you have to update your machine to the latest patches

```
yum update -y
reboot
```

Check Linux version after update and reboot

```
cat /ets/os-release
```


## Install tools

JQ is the standard tool to format, parse and query JSON data

```
yum install -y jq git
```


## Install Docker from Docker CentOS repository

- Add the official Docker repository
- Install Docker and containerd
- Start the service and enabele it permanently

```
yum config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum -y install docker-ce docker-ce-cli containerd.io docker-compose-plugin
systemctl --now enable docker
```

## Check if Docker is running

```
docker version
```

## Add standard "notes" user

```
useradd -m -U notes
```

