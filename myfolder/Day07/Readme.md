Node Affinity:

RBAC:
    - Service Account: Namespace level : Role and Role Binding
    - User: CLuster level : ClusterRole and ClusterRoleBinding

mkdir apache
kubectl delete -f . [delete all resources]

namespace.yaml

[
D:\DevOps\Kubernetes\Day07>kubectl auth whoami
ATTRIBUTE                                           VALUE
Username                                            kubernetes-admin
Groups                                              [kubeadm:cluster-admins system:authenticated]
Extra: authentication.kubernetes.io/credential-id   [X509SHA256=b60cc1464f76677534b70b572827a7e1fce0f8d00acd3b8394c6303fc4ca19f0]

D:\DevOps\Kubernetes\Day07>kubectl auth can-i get pod
yes

D:\DevOps\Kubernetes\Day07>kubectl auth can-i get pod -n apache
yes
]

deployment.yaml
role.yaml
serviceaccount.yaml
get serviceaccount.yaml

kubectl auth can-i get pod -n apache --as=apache-user
    - no [because user is yet not binded with role]

role-binding.yaml

kubectl auth can-i get pods --as=apache-user -n apache 
===================================================================
Subject Kind	apiGroup value
User	        rbac.authorization.k8s.io
Group	        rbac.authorization.k8s.io
ServiceAccount	"" (empty)
===================================================================
To Check Any Resource's API Group:

    kubectl api-resources 
    NAME        SHORTNAMES   APIGROUP   NAMESPACED
    pods        po                      true
    deployments deploy       apps       true
    jobs                    batch       true
===================================================================
Can we create a User in Kubernetes using YAML?
    No. Kubernetes does not manage Users. It relies on external authentication mechanisms. 
    Only ServiceAccounts are native objects.

When To Use What ?
Application inside cluster -->	ServiceAccount
Human login via kubeconfig -->	User (certificate/OIDC)
Team-based access -->	Group
===================================================================

===================================================================