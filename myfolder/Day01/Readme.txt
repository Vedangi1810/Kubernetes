create kind-cluster.yaml
kind create cluster --config kind-cluster.yaml --name vd-kind-cluster
kubectl get nodes