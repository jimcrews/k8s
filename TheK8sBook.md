Use k3d for demos.

```
k3d cluster create tkb -p "8081:80@loadbalancer" \
  --servers 1 \
  --agents 3 \
  --image rancher/k3s:latest
```

cleanup
```
k3d cluster list
k3d cluster delete tkb
```

The kubectl configuration file is called config and lives in a hidden directory called .kube in your home directory
You can view your kubeconfig using the ```kubectl config view``` command
You can use ```kubectl config current-context``` to see your current context


## kubectl exec: running commands in Pods

kubectl exec <pod-name> -- <command>
```
kubectl exec hello-pod -- ps
```

usekubectl exec to get shell access to a container running in a Pod. Install curl and check url. get hostname too..

```
kubectl exec -it hello-pod -- sh

apk add curl
curl localhost:8080
env | grep HOSTNAME
```

The -it flags on the kubectl exec command make the session interactive and connect STDIN and STDOUT on your terminal to STDIN and STDOUT inside the first container in the Pod.
If you’re running multi-container Pods, you’ll need to pass the --container flag and give it the name of the container you want to create the exec session with.


## Configuring kubectl to use a specific Namespace

The following command configures kubectl to run all future commands against the shield Namespace.
```
kubectl config set-context --current --namespace shield

kubectl config set-context --current --namespace default
```
