# Ubuntu preparation

## Update to current version

First of all you have to update your machine to the latest patches.
For Ubuntu it is important to run `apt update` to download the software repository before installing any new package


```
apt update
apt upgrade
reboot
```

## Check current version after boot

```
cat /ets/os-release
```


## Install tools Ubuntu

JQ is the standard tool to format, parse and query JSON data

```
apt install -y jq file
```


# Install Docker


## Install Docker from Ubuntu repository

Install Docker, start the service and make it permanently enabled

```
apt install -y docker.io docker-compose
systemctl --now enable docker
```


## Check if Docker is running

```
docker version
```



## Add standard user

```
useradd -m -U notes
```
