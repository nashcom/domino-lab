# Build Domino Container Images on Docker


## Clone GitHub repositories

Create a local directory and switch to it

```
mkdir -p /local/github
cd /local/github
```

Clone the HCL Domino container project and the Nash!Com Domino on Linux Startscript project

```
git clone https://github.com/HCL-TECH-SOFTWARE/domino-container.git
git clone https://github.com/nashcom/domino-startscript.git

```


## Build Domino 14.0.0EA1 Image with Nomand Server 1.0.8

Switch to the GitHub repository directory just cloned

```
cd /local/github/domino-container
```

Build Domino 14.0.0EA1

```
./build.sh domino 14.0.0EA1 -nomad=1.0.8-12.0.2 latest
```


Build Traveler 14.0.0EA1 on top of Domino 14.0.0EA1

```
./build.sh traveler 14.0.0EA1 -from=hclcom/domino:14.0.0EA1
```

## Check the available images


```
docker images
```


## Upload image to registry

```
docker login harbor.dnug.eu
docker tag hclcom/domino:latest harbor.dnug.eu/dnug/domino:latest
docker push harbor.dnug.eu/dnug/domino:latest
```

## Install Domino control

```
/local/github/domino-startscript/install_dominoctl
dominoctl about+
```
