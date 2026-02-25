docker-cont --> pods --> deployments --> service --> user

kubectl get pods/nodes
kubectl get ns/namespace
kubectl get pods -n kube-system

To create namespace:
kubectl create ns nginx

To create pod nginx:
kubectl run nginx --image=nginx -n nginx

To delete pod:
kubectl delete pod nginx -n nginx

==================================
namespace.yaml
kubectl apply -f namespace.yaml

pod.yaml
kubectl apply -f pod.yaml

kubectl exec -it pod/nginx-pod -n nginx -- bash
OR
kubectl exec -it nginx-pod -n nginx -- /bin/sh
exit

kubectl describe pod/nginx-pod -n nginx

who will decide to run container in which pod and on which node? (ans: Filtering and scoring)
I can use kubectl describe (with all k8s components)

deployment.yaml

kubectl delete pod nginx-pod
kubectl apply -f deployment.yaml (If your deployment is creating pod, then no need to use pod.yaml)
kubectl get pods
kubectl scale deployment/nginx-deployment -n nginx --replicas=5
kubectl get pods
kubectl scale deployment/nginx-deployment -n nginx --replicas=1
kubectl get pod -n nginx -o wide

Rolling update in Deployments:
kubectl set image deployment/nginx-deployment -n nginx nginx=nginx:1.27.3
kubectl get pods -n nginx

kubectl delete -f deployment.yml

Replicaset : replicaset.yml (no rolling update or rollback functionality)
kubectl apply -f replicaset.yaml

Daemonset : daemonset.yml (ensures each replica/pod runs on each number of worker node, no need to mention replicas)
kubectl apply -f daemonset.yaml

kubectl get, kubectl describe, kubectl logs, and kubectl explain.

