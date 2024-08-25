## Create Deployment
```
kubectl create deployment nginx --image=nginx
kubectl create deployment nginx --image=nginx --replicas=4

k create deploy webapp --image=kodekloud/webapp-color --replicas=3
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

## Edit

```
k edit deployment nginx
k scale deployment nginx --replicas=5
```