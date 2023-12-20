### Install k3d for macos

``` shell
brew install k3d
```
### Create a cluster with 3 worker nodes
``` shell
k3d cluster create --agents 3
```

``` shell
k create deployment echo --image=g1g1/echo-server:0.1
k expose deployment echo --type=NodePort --port=7070
```

### Checking our services. We need a proxy to access the echo service
``` shell
k get svc echo
```


### Start proxy
``` shell
k proxy &
```

### Test
``` shell
http http://localhost:8001/api/v1/namespaces/default/services/echo:7070/proxy/yeah-it-works
```

### List deployments
``` shell
k get deployments
```

### Delete
``` shell
pkill -9 -f "kubectl proxy"
k delete deployment echo
```
