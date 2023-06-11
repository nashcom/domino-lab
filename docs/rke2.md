
# RKE2 Install

## Reference:

https://ranchermanager.docs.rancher.com/v2.5/pages-for-subheaders/install-upgrade-on-a-kubernetes-cluster

## System requirements

https://docs.rke2.io/install/requirements


## Run RKE2 install script

```
curl -sfL https://get.rke2.io | sh -
```

```
systemctl enable --now rke2-server.service
```

## Check YAML

```
cat /etc/rancher/rke2/rke2.yaml
```


# Install kubectl

## Download and install

```
curl -L "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" -o /usr/bin/kubectl
chmod +x /usr/bin/kubectl
```

## Export configuration RKE2

### One time

```
export KUBECONFIG=/etc/rancher/rke2/rke2.yaml
```

### Permanently add config variable and alias

```
echo 'export KUBECONFIG=/etc/rancher/rke2/rke2.yaml' >> ~/.bashrc
echo 'alias k=kubectl' >> ~/.bashrc

```


## Check if Kubernetes is running

```
kubectl get node -o wide
```
