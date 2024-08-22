## Generate POD Manifest YAML file (-o yaml)

`k run nginx --image=nginx --dry-run=client -o yaml`

## Generate Deployment YAML file (-o yaml)

`k create deploy httpd-frontend --image=httpd:2.4-alpine --replicas=3 --dry-run=client -o yaml`

## Create Service - ClusterIP

`k expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml`

## Create Service - NodePort

`k expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml`

## Taint Node

`k taint node kind-worker spray=mortein:NoSchedule` (NoSchedule, PreferNoSchedule or NoExecute)

## Add Label to Node

`k label node node01 color=blue`

## Edit pod, deployment

`k edit pod frontend`
`k edit deployment frontend`

## Replace 

`kubectl replace --force -f ./pod.json`