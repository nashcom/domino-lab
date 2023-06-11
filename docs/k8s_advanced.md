

SetupAutoConfigureTemplateDownload=

http://k3s.lab.dnug.eu/.well-known/acme-challenge/test

# Install RKE2


## Specific settings for local IPs

mkdir -p /etc/rancher/rke2
touch /etc/rancher/rke2/config.yaml
chmod 600 /etc/rancher/rke2/config.yaml
vi /etc/rancher/rke2/config.yaml


write-kubeconfig-mode: 600
node-name: "alpha"
node-ip: 10.0.0.6
tls-san:
  - 10.0.0.6
  - alpha


## Install Server


curl -sfL https://get.rke2.io

systemctl enable --now rke2-server.service

## Install Agent on additional Node


Copy the joint token

```
cat /var/lib/rancher/rke2/server/node-token
```

```
export TOKEN=xxx

mkdir -p /etc/rancher/rke2/
echo "server: https://10.0.0.6:9345" >> /etc/rancher/rke2/config.yaml
echo "token: $TOKEN" >> /etc/rancher/rke2/config.yaml
```

```
curl -sfL https://get.rke2.io | INSTALL_RKE2_TYPE="agent" sh -
systemctl enable --now rke2-agent.service
```

```
echo "node-ip: 10.0.0.7" >> /etc/rancher/rke2/config.yaml
```

---


# Install K3s

## Install Server

```
curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION=v1.25.10+k3s1 sh -
```


---

## Install Agent on additional Node


On server node

```
cat /var/lib/rancher/k3s/server/node-token
```


```
export TOKEN=K100c466c3a566040a02d90c9ae992ec8333246fa45260cc28bbb0f654c51d58c44::server:4d97c844277d09ad6f08d8e0554adc7b
curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION=v1.25.10+k3s1 INSTALL_K3S_EXEC="agent" K3S_URL=https://10.0.0.6:6443 K3S_TOKEN=$TOKEN sh -
```

---

```
mkdir -p /etc/rancher/k3s
touch /etc/rancher/k3s/config.yaml
chmod 600 /etc/rancher/k3s/config.yaml
vi /etc/rancher/k3s/config.yaml
echo "node-ip: 10.0.0.7" >> /etc/rancher/k3s/config.yaml
```
