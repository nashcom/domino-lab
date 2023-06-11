## Install K3s

In order to install the Rancher management interface install the latest support K8s version.

```
curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION=v1.25.10+k3s1 sh -
```

## Check where kubectl is installed

```
which kubectl
```

## Export configuration K3s


### One time

```
alias k=kubectl
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
```

### Permanently add config variable and alias

```
echo 'export KUBECONFIG=/etc/rancher/k3s/k3s.yaml' >> ~/.bashrc
echo 'alias k=kubectl' >> ~/.bashrc

```

## Check if Kubernetes is running

```
kubectl get node -o wide
```
