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

### Summarize Commands

Create
```
k create -f deployment-definition.yaml
```
Get
```
k get deploy
```
Update
```
k apply -f deployent-definition.yaml
k set image deployment/my-app-deployment nginx=nginx:1.9.1
k set image deployment/frontend simple-webapp=kodekloud/webapp-color:v2
```
Status
```
k rollout status deployment/myapp-deployment
k rollout history deployent/myapp-deployment
```
Rollback
```
k rollout undo deployment/myapp-deployment
```