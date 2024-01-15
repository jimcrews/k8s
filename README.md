k3d commands

```
k3d cluster create my-cluster --servers 3 --agents 3
k3d cluster list
k3d cluster delete my-cluster
```

k3d demo
```
k3d cluster create my-cluster -p "8081:80@loadbalancer"  --servers 1 --agents 2
k create deployment nginx-dep --image=nginx --dry-run=client -o yaml > nginx-dep.yaml
k apply -f nginx-dep.yaml
k create service clusterip nginx --tcp=80:80 --dry-run=client -o yaml > nginx-service.yaml
k apply -f nginx-service.yaml
k apply -f my_ingress.yaml
```

k3d cleanup
```
k delete -f my_ingress.yaml
k delete service nginx-service -n test
k delete deployment nginx-deploy -n test
k3d cluster delete my-cluster
```

```
k create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
k expose deployment hello-node --type=LoadBalancer --port=8080
```


### Create an NGINX Pod

Using the `kubectl run` command can help in generating a YAML template.

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
k label node node01 color=blue
```

## Taints and Tolerations
Taints and Tolerations are only meant to restrict nodes from accepting certain pods. it does not tell the pod to go to a particular node.
 - Taints are set on Nodes
 - Tolerations are set on Pods

```
kubectl taint nodes node01 spray=mortein:NoSchedule
```
or to remove taint (add '-' to the end)
```
kubectl taint nodes node01 spray=mortein:NoSchedule-
kubectl taint nodes controlplane node-role.kubernetes.io/control-plane:NoSchedule-
```
Tolerations are added to the pod spec file.

Q: Do any Taints exist on node01

```
k describe node node01 | grep -i taint
```

## Node Selectors
Add 'nodeSelector' to the pod definition file. The key value pair in nodeSelector selects the node (such as size=Large). 
You must have first labeled your nodes before creating this pod - `k label nodes node01 size=Large`

## Node Affinity
Ensure pods are hosted on specific nodes using more advanced expressions than Node Selectors. Such are using selectors using 'Or' or 'Not'.
types of node affinity: 
 - `requiredDuringSchedulingIgnoredDuringExecution`
 - `preferredDuringSchedulingIgnoredDuringExecution`

 'During Scheduling' is the state where a pod does not exist and is created for the first time. 'Required' = the scheduler will mandate the pod be placed on the correct node, otherwise the pod wont be scheduled. 'Preferred' is best effort. The pod will be place anywhere if no labael is found.

 'During Execution' is the state where the pod has been running and a change has been made that effects node affinity. 'Ignored' = no changes will be made.
