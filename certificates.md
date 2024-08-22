In an environment set up by kubeadm, look for the kube api server definition file - `cat /etc/kubernetes/manifests/kube-apiserver.yaml`

identify the certificate file used for each pupose, eg. the api server certificate file (--tls-cert-file=/etc/kubernetes/pki/apiserver.crt)

decode the certificate to see its details

`openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout`

