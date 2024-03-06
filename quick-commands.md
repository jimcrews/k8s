## Generate POD Manifest YAML file (-o yaml)

`k run nginx --image=nginx --dry-run=client -o yaml`

## Generate Deployment YAML file (-o yaml)

`k create deploy httpd-frontend --image=httpd:2.4-alpine --replicas=3 --dry-run=client -o yaml`

