

# Install Rancher UI

Reference:
https://docs.rke2.io/install/quickstart

## Install Helm

```
curl -L https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

## Add Rancher Helm repository

- Latest version with newest features

```
helm repo add rancher-latest https://releases.rancher.com/server-charts/latest
```


## Install Rancher via Helm

```
helm upgrade -i rancher rancher-latest/rancher --set global.cattle.psp.enabled=false --create-namespace --namespace cattle-system --set replicas=1 --set ingress.tls.source=secret --set hostname=$(hostname -f) --set bootstrapPassword=dnuglab50
```

## Wait for deployment

```
kubectl -n cattle-system rollout status deploy/rancher
```


## Add TLS secret

```
kubectl -n cattle-system create secret tls tls-rancher-ingress --cert=cert.pem --key=key.pem
```

## Delete TLS secret to provide a new one

```
kubectl -n cattle-system delete secret tls-rancher-ingress
```

