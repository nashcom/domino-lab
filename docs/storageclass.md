# Prepare Longhorn storage requirements

iSCSI a requirement for K8s Longhorn storage

## Install iSCSI driver

```
yum -y install -y iscsi-initiator-utils nfs-utils

systemctl enable --now iscsid
```

## Install iSCSI driver Ubuntu

```
apt install nfs-common open-iscsi -y
systemctl enable --now open-iscsi
```

## Check installation requirements for Longhorn

```
curl -sSfL https://raw.githubusercontent.com/longhorn/longhorn/master/scripts/environment_check.sh | bash
```

Longhorn storage is configured on Rancher graphical interface

# Use local storage provider for RKE2

## Install local provisioner

```
kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml
```
