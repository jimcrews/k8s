![node port diag](https://i.sstatic.net/A2G76.png)

### NodePort definition

``` yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service

spec:
  type: NodePort
  ports:
  - targetPort: 80
    port: 80
    nodePort: 30008
  selector:
    app: myapp
    type: front-end
```

If not provided:

 - targetPort is assumed to be the same as Port
 - NodePort will be automatically created

### Commands
``` shell
k create -f service-definition.yaml
k get services

k create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml 

k create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml

# create ClusterIP service to expose pod
k expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml

# create NodePort service to expose pod (edit the file to dpecify node port) 
k expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml
```

Create a pod called httpd using the image httpd:alpine in the default namespace. Next, create a service of type ClusterIP by the same name (httpd). The target port for the service should be 80.

Try to do this with as few steps as possible.

```
k run httpd --image=httpd:alpine --port=80 --expose=True
```