HPA, VPA, KEDA - Autoscaling

HPA : (replicas) normal/stateless application
VPA : (size of pod) stateful application (mysql)

KEDA : K8s Event Driven Autoscaling
       Based on matrix it automatically perform HPA or VPA

kubectl top node
- matrix api not available

kubernetes kind cluster metrix server:
https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.6.1/components.yaml

mkdir nginx

kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.6.1/components.yaml

kubectl -n kube-system edit deployment metrics-server

follow : https://github.com/LondheShubham153/kubestarter/tree/main/HPA_VPA

kubectl get pods -n kube-system
kubectl top node/pod

mkdir apache

namespace.yaml
deployment.yaml
service.yaml

[curl http://apache-service.apache.svc.cluster.local]

kubectl port-forward svc/apache-service -n apache 82:80 --address=0.0.0.0

http://localhost:82

kubectl scale deployment apache-deployment -n apache --replicas=3 [Manual scaling]
kubectl scale deployment apache-deployment -n apache --replicas=1


hpa.yaml
kubectl get hpa -n apache
kubectl run load-generator --image=busybox -n apache [crashlopopbackoff]
kubectl get pod -n apache
kubectl run -i --tty load-generator --image=busybox -n apache /bin/sh
    while true; do wget -q -O- http://apache-service.apache.svc.cluster.local; done

new terminal:
    kubectl get hpa -n apache
    kubectl get pod -n apache



