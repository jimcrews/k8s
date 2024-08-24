Create Deployment
```
kubectl create deployment front-end-deploy --image=nginx
```

```
kubectl create deployment front-end-deploy --image=nginx --dry-run=client -o yaml
```

```
kubectl create deployment front-end-deploy --image=nginx --replicas=4 --dry-run=client -o yaml > front-end-deploy.yaml
```

Make necessary changes to the file (for example, adding more replicas) and then create the deployment.

```
kubectl apply -f front-end-deploy.yaml
```