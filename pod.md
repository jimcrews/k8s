### Create Pod without yaml
new pod called nginx, using image from Dockerhub 'nginx'

``` shell
k run nginx --image=nginx
k run redis --image=redis -n=finance
```

### Which node are the pods running
you can "describe" all pods one by one, or,
`k get pods -o wide`

### Create Pod using yaml

either create the yaml from scratch, or, use "dry-run"

```
k run redis --image=redis --dry-run=client -o yaml > redis.yaml
```

``` yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
    tier: frontend
spec:
  containers:
  - name: nginx
    image: nginx

```

commands to use pod yaml:

```
k apply -f pod.yaml
k get pods
k describe pods nginx
k delete pod nginx

k replace --force -f pod.yaml

# extract the pod definition to YAML

kubectl get pod webapp -o yaml > my-new-pod.yaml
```


``` yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: static-busybox
  name: static-busybox
spec:
  containers:
  - image: busybox
    name: static-busybox
    command: ['sleep']
    args: ['1000']
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```