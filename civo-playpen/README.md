
## Create Cluster
Create Civo cluster and download Kubeconfig: ```export KUBECONFIG=/Users/jimcrews/repos/tiny_k8s_projects/civo-playpen/kubeconfig```

---
exec into running container: ```kubectl exec -it <pod-name> -- bash```

list processes: ```ps -A```

---

When you **cordon** a node, you prevent future Pods from being scheduled onto that machine. When you **drain** a node, you remove any Pods that are currently running on that machine.

use kubectl **uncordon** to re-enable Pods scheduling onto the node

---

Random commands

```k top nodes``` - list nodes resource consumption