Monitoring and Logging: [RBAC in cluster level]

mkdir dashboard

https://github.com/LondheShubham153/kubestarter/tree/main/kind-cluster
Setting Up the Kubernetes Dashboard
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml

==========================================================
dashboard-admin-user.yaml

[ClusterRole will be already created]
ServiceAccount
ClusterRoleBinding
==========================================================
kubectl get clusterrole -n kubernetes-dashboard
    ClusterRole
    cluster-admin

Get the Access Token Retrieve the token for the admin-user:
    kubectl -n kubernetes-dashboard create token admin-user
    Copy the token for use in the Dashboard login.

Access the Dashboard Start the Dashboard using kubectl proxy:
    kubectl proxy (works for localhost)
    kubectl proxy --port=8001 --address=0.0.0.0 --accept-hosts='.*' (if prev command don't work)
    Open the Dashboard in your browser:

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
    Use the token from the previous step to log in.

===========================================================================================
Custom Resource Definitions (CRDs) - Not asked in Interviews

mkdir crd
devops-crd.yaml
devops-cr.yaml

=============================================================================================

Operators, Helm, Service Mesh, Kubernetes API
[Helm and service mesh might be asked in interviews]
[Operators and k8s API not asked in interviews]

Helm:

mkdir helm

https://helm.sh/docs/intro/install/
winget install Helm.Helm

helm version
helm

helm create apache-helm

[Edit: templates/service.yaml, values.yaml]

helm package .\apache-helm
    can import/export this package

helm install dev-apache apache-helm
kubectl get pods/deployments/svc

helm install dev-apache apache-helm -n dev-apache --create-namespace
kubectl get pods/deployments/svc [deleted]

helm install prd-apache apache-helm -n prd-apache --create-namespace
vim apache-helm/values.yaml {change replicas from 2 to 3}
vim apache-helm/Chart.yaml {not sure why}
helm package apache-helm
helm upgrade prd-apache ./apache-helm -n prd-apache
helm rollback prd-apache 1 -n prd-apache (rollback to previous revision 1)

create-->edit-->package-->install/upgrade
================================================================

helm search repo <repo_name>
helm repo add stable https://charts.helm.sh/stable
helm search repo
helm repo list
helm list

Questions:

Helm: Package manager for k8s, makes deployments easy and maintain consisteny accross env

Helm Chart: Package of pre-configured k8s resources, templates, configuration files

Structure of Helm Chart:
    charts/ : optional folder to stpre dependent/sub chart
    values.yaml: default configuration values for k8s
    chart.yaml: chart info like name, type (application/library), version, appVersion
    templates/: k8s manifest files

What is the difference between a Helm Chart and a Helm Release?
A Helm chart is the package itself,
while a Helm release is an instance of a Helm chart that has been deployed to a Kubernetes cluster.

================================================================
Init Container Vs SidecarContainer

mkdir pods
init-container.yaml

kubectl get pods -w [pod status: init, PodInitializing, completed]
kubectl logs init-test -c init-container -c main-container

sidecar-container.yaml
kubectl get pods -w
kubectl logs sidecar-test -c sidecar-container -c main-container