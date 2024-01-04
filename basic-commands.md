Using the `kubectl run` command can help in generating a YAML template.

### Create an NGINX Pod

```
kubectl run NAME --image=IMAGE

kubectl run NAME --image=IMAGE --dry-run=client -o yaml
```

### Create a deployment
```
kubectl create deployment NAME --image=IMAGE

kubectl create deployment NAME --image=IMAGE --dry-run=client -o yaml
```

Make necessary changes to the file (for example, adding more replicas) and then create the deployment. `kubectl create -f nginx-deployment.yaml`
