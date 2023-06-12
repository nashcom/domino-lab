# Run Domino on K8s

## Add registry

```
kubectl create secret docker-registry --namespace default regcred --docker-server=$LAB_REGISTRY_HOST --docker-username=$LAB_REGISTRY_USER --docker-password=$LAB_REGISTRY_PASSWORD
```

## Run your first Domino server

```
./autocfg domino12.yml -prompt > domino.yml
kubectl apply -f domino.yml
```

## More advanced way to deploy in one step

```
./autocfg domino12.yml -prompt | kubectl apply -f -
```

## Example get file from remote location

```
./autocfg -p='curl https://domino-lab.net/domino12.yml' -prompt | kubectl apply -f -
```

## Create a TLS secret

```
kubectl create secret tls tls-secret --cert=cert.pem --key=key.pem
```

## Create a PEM file for CertMgr

```
kubectl create secret generic domino-tls --from-file=tls.pem 
```
