StatefulSet: (Database)

mkdir mysql

namespace.yaml
statefulset.yaml
service.yaml
configmap.yaml
secret.yaml

kubectl exec -it <ss_name> -n mysql -- bash
mysql -u root -p
show databases;

Kubectl delete pod <pod_name> -n mysql 
    Immediately new pod will be created with same name (to maintain the state)

All env var, service, volume claims are tightly coupled with statefulset

======================================================================================
Just for Knowledge:
kubectl config set-context --current --namespace=mysql

======================================================================================
Resource Quotas: [limits and Requests]

mkdir nginx

namespace.yaml
deployment.yaml
pv.yaml -- notsure
pvc.yaml -- not sure
======================================================================================

Probes: (check status of pods)
- liveness probe
- readiness probe
- startup probe

mkdir django-notes-app
cd k8s

service.yaml
deployment.yaml

kubectl describe pods/pod_name -n nginx
If want [do port-forward and check from url]
======================================================================================

Taints and Tolerants:
Control-plane is tainted by default

kubectl get nodes
To add taint:
kubectl taint node vd-kind-cluster-worker prod=true:NoSchedule
kubectl taint node vd-kind-cluster-worker2 prod=true:NoSchedule

mkdir nginx
kubectl apply -f pod.yaml
kubectl get pods -n nginx
    - pending
kubectl describe pods/pod_name -n nginx

To remove taint:
kubectl taint node vd-kind-cluster-worker prod=true:NoSchedule-
[Again try to schedule and get pods]

Tolerations: [even if node is tainted pod can run on that node because it's tolerated]
- Add tolerations in pod.yaml







