**Service:**



Types of Services:



kubectl port-forward service/notes-app-service -n nginx 8000:8000 --address=0.0.0.0



https://localhost:80



Django-notes-app : dev branch

docker build -t notes-app-k8s . (from dockerfile)



docker image tag notes-app-k8s:latest vedangi1018/notes-app-k8s:latest



docker push vedangi1018/notes-app-k8s:latest



docke-image --> docker hub --> pod



mkdir k8s:

namespace.yaml

deployment.yaml (use your pushed image from docker hub)

service.yaml



kubectl port-forward service/notes-app-service -n nginx 8000:8000 --address=0.0.0.0 (only required when running notes-app individually, when using ingress-controller no need)



https://localhost:8000/



======================================================

Ingress:

run everything in nginx namespace

kubectl delete deployment/notes-app-deployment -n notes-app (similarly delete ns and service)

Ingress-controller : works at cluster level (nginx)

(outside notes-app folder) 


kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

[
    D:\DevOps\Kubernetes\Day04>kubectl get all -n ingress-nginx
    NAME                                          READY   STATUS    RESTARTS   AGE
    pod/ingress-nginx-controller-589b66c8-g589t   0/1     Running   0          51s

    NAME                                         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
    service/ingress-nginx-controller             LoadBalancer   10.96.100.232   <pending>     80:31179/TCP,443:31245/TCP   51s
    service/ingress-nginx-controller-admission   ClusterIP      10.96.165.231   <none>        443/TCP                      51s

    NAME                                       READY   UP-TO-DATE   AVAILABLE   AGE
    deployment.apps/ingress-nginx-controller   0/1     1            0           51s

    NAME                                                DESIRED   CURRENT   READY   AGE
    replicaset.apps/ingress-nginx-controller-589b66c8   1         1         0       51s
]



ingress.yaml (nginx folder) (80: service port)

kubectl get ing -n nginx

kubectl get -all -n nginx

kubctl get service -n ingress-nginx (expose ingress controller)

kubectl port-forward service/ingress-nginx-controller -n ingress-nginx 8080:80 --address=0.0.0.0 (ingress controller running on port 8080) (80: cluster port)

[
    Your Local Machine:8080
            ↓
    Ingress Controller Service:80 (inside cluster)

    8080      : 80
    LocalPort : ClusterPort

    Where	                    Port 80 Meaning
    ingress.yml	            Service port inside cluster
    port-forward	        Port of ingress controller service
    Local machine	        8080
]

kubectl delete pod --all -n nginx --force --grace-period=0

