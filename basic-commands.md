k3d commands

```
k3d cluster create my-cluster --servers 3 --agents 3
k3d cluster list
k3d cluster delete my-cluster
```

k3d demo
```
k3d cluster create --api-port 6550 -p "8081:80@loadbalancer" --agents 2
k create deployment nginx --image=nginx
k create service clusterip nginx --tcp=80:80
k apply -f my_ingress.yaml
```

k3d cleanup
```
k delete -f my_ingres.yaml
k delete service nginx
k delete deployment nginx
k3d cluster delete k3s-default
```

```
k create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
k expose deployment hello-node --type=LoadBalancer --port=8080
```


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

## Edit a pod or export to yaml
```
kubectl edit pod <pod name>

kubectl get pod webapp -o yaml > my-new-pod.yaml
```

### Label a node
```
kubectl label node node01 color=blue
```
