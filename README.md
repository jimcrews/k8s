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

## Replace a pod using config
```
kubectl replace --force -f /tmp/kubectl-edit-19233122.yaml
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
Ensure pods are hosted on specific nodes by what labels exist on the nodes.
types of node affinity: 
 - `requiredDuringSchedulingIgnoredDuringExecution`
 - `preferredDuringSchedulingIgnoredDuringExecution`


## Secrets
```
kubectl create secret generic db-secret --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123
kubectl create secret generic app-secret --from-file=app_secret.properties
```


## Cluster maintenance
You can purposefully drain the node of all the workloads so that the workloads are moved to other nodes.
The node is also cordoned or marked as unschedulable.

```
k drain node-1
```

When the node is back online after a maintenance, it is still unschedulable. You then need to uncordon it.
```
k uncordon node-1
```

There is also another command called cordon. Cordon simply marks a node unschedulable. Unlike drain it does not terminate or move the pods on an existing node.

```
k drain node-1
k cordon node-2
k uncordon node-1
```

## Upgrade Cluster process

upgrade 1 version at a time
get the current node versions
```
k get nodes
```

open docs (https://kubernetes.io/search/?q=upgrade) and click the upgrade link from current version to next version.

what distro:
```
cat /etc/*release*
```

 - get the latest patch release in that minor version (eg 1.25.x-00 where x is the latest)
 - upgrade kubeadm (kubeadm version)
 - kubeadm upgrade plan
 - ```kubeadm upgrade apply v1.25.10```
 - ```kubectl get node```
 - upgrade kubelet if required. drain the node. ```kubectl drain <node> --ignore-daemonsets```
 - upgrade kubelet
 - restart the service, and uncordon the node

 - ssh to worker node 
 - upgrade kubeadm
 - ```kubeadm upgrade node```
 - upgrade kubelet. drain the node. (run command on control plane)
 - upgrade kubelet
 - restart the service, and uncordon



## ETCD

To make use of etcdctl for tasks such as back up and restore, make sure that you set the ETCDCTL_API to 3.

 

You can do this by exporting the variable ETCDCTL_API prior to using the etcdctl client. This can be done as follows:

export ETCDCTL_API=3


## config

```kubectl config view```: Lists all clusters for which kubeconfig entries have been generated. This is helpful in verifying or troubleshooting your settings

switch context to specific cluster name - ```kubectl config use-context cluster1```


```
student-node ~ ➜  kubectl config use-context cluster1
Switched to context "cluster1".

student-node ~ ➜  k get nodes
NAME                    STATUS   ROLES           AGE   VERSION
cluster1-controlplane   Ready    control-plane   51m   v1.24.0
cluster1-node01         Ready    <none>          50m   v1.24.0

student-node ~ ➜  kubectl config use-context cluster2
Switched to context "cluster2".

student-node ~ ➜  k get nodes
NAME                    STATUS   ROLES           AGE   VERSION
cluster2-controlplane   Ready    control-plane   51m   v1.24.0
cluster2-node01         Ready    <none>          51m   v1.24.0

student-node ~ ➜  
```


# NodePort Service
The range of valid ports is 30000-32767