
```
k3d cluster create tkb -p "8082:30080@agent:0" \
  --servers 1 \
  --agents 3 \
  --image rancher/k3s:latest
```


## create deployment
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello-world
  revisionHistoryLimit: 5
  progressDeadlineSeconds: 300
  minReadySeconds: 10
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-pod
        image: nigelpoulton/k8sbook:1.0
        ports:
        - containerPort: 8080
        resources:
          limits:
            memory: 128Mi
            cpu: 0.1
```

## create service
```
apiVersion: v1
kind: Service
metadata:
  name: hello-svc
  labels:
    app: hello-world
spec:
  type: NodePort
  ports:
  - port: 8080
    nodePort: 30080
    protocol: TCP
  selector:
    app: hello-world
```

## test
```
curl localhost:8082/
```

## Update image version to 2.0
```
k apply -f k3d-nodeport-deploy.yaml

k rollout status deployment hello-deploy

k get deploy hello-deploy
```


## cleanup
```
k3d cluster list
k3d cluster delete tkb
```