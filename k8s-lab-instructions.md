# Kubernetes Lab Instructions

Preparation

* Already downloaded already from the Docker part
* Docker is already installed and the base 
* You just need to extract the scripts


```
cd /local/software
tar -xvf k3s.tar
```


## Install k3s

```
curl -sfL https://get.k3s.io | sh -
```


## Check installation

```
k3s kubectl get node
```

## Install kubectrl on your machine

Instructions:

https://kubernetes.io/docs/tasks/tools/install-kubectl/


### Windows Install -- if you have curl ;-)

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.19.0/bin/windows/amd64/kubectl.exe
```

Or just download via browser ..

### Download your kube config from your Linux box to your machine

```
 /etc/rancher/k3s/k3s.yaml
```

For example MobaXterm --> drag & drop to file explorer 


## Export your configuration on Windows

```
set KUBECONFIG=d:\k3s\kubeconfig.yml
```

### Or use the following on Mac/Linux

```

 ~/.kube/config 
 
 or 
 
 export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
```

## Edit the file and change the hostname from 127.0.0.1 to your server name like this:

```
https://master.domino-lab.net:6443

```


## Check configuration and connection

```
kubectl.exe version

kubectl.exe get node
```


## Install Dashboard on Linux Server

This needs a couple of more complex commands

```
cd /local/software/k3s/dashboard
```

Run the script:

```
./install.sh
```

It does the following, which you don't want to type in ;-)

```
GITHUB_URL=https://github.com/kubernetes/dashboard/releases
VERSION_KUBE_DASHBOARD=$(curl -w '%{url_effective}' -I -L -s -S ${GITHUB_URL}/latest -o /dev/null | sed -e 's|.*/||')
k3s kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/${VERSION_KUBE_DASHBOARD}/aio/deploy/recommended.yaml
```


## Run the deploy script

```
./deploy.sh
```

It does the following:

```
k3s kubectl create -f dashboard.admin-user.yml -f dashboard.admin-user-role.ym
```


### Get the authentication token on Windows

```
kubectl -n kubernetes-dashboard describe secret admin-user-token | findstr token
```

### Get the authentication token on Linux/Mac

```
kubectl -n kubernetes-dashboard describe secret admin-user-token |grep token
```

## Connect from your machine to k3s dashboard

The proxy command creates a tunnel between your local machine and your K8s server

```
kubectl proxy
```

## Launch the Dashboard in your local browser

Yes you have to use exactly this URL on your local browser!  

```
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

```

This completes the K3s setup


## Now let's install Domino again

But where to do we get it from?

We have a registry to download images prepared

# Write a new secrect for accessing our Docker registry 

```
kubectl create secret docker-registry regcred --docker-server=https://registry.csi-domino.com --docker-username=admin --docker-password=xxxxx

```


## Edit domino12.yml and have a look

```
Or just run a "cat domino12.yml"
```


### Create your first Pod

```
kubectl apply -f domino12.yml
```

### Delete a Pod

```
kubectl delete -f domino12.yml
```


### Show details of a pod

```
kubectl describe pod/domino12
```

### Run a bash into a pod

```
kubectl exec pod/domino12 -it -- bash
```
