Using the `kubectl run` command can help in generating a YAML template.

### Create an NGINX Pod

`kubectl run nginx --image=nginx`

### Generate POD Manifest YAML file (-o yaml). Don’t create it(–dry-run)

`kubectl run nginx --image=nginx --dry-run=client -o yaml`

### Create a deployment

`kubectl create deployment --image=nginx nginx`

### Generate Deployment YAML file (-o yaml). Don’t create it(–dry-run)

`kubectl create deployment --image=nginx nginx --dry-run=client -o yaml`

### Generate Deployment YAML file (-o yaml). Don’t create it(–dry-run) and save it to a file.

Name: httpd-frontend,
Image: httpd:2.4-alpine

`k create deployment httpd-frontend --image=httpd:2.4-alpine --dry-run=client -o yaml > my-deplo.yaml`

Make necessary changes to the file (for example, adding more replicas) and then create the deployment. `kubectl create -f nginx-deployment.yaml`
