Chat Application on k8s - 3 Tier

React     - Docker - Pod - Deployment - Service \
Node JS   - Docker - Pod - Deployment - Service  | Ingress
MonoDB    - Docker - Pod - Deployment - Service /

FYI : docker image tage <old> <new>

minikube start --driver=docker
git clone https://github.com/Vedangi1810/full-stack_chatApp.git
docker hub login
docker login : cmd

cd backend
docker build -t vedangi1018/chatapp-backend:latest . [To push image to my docker hub]
docker images
docker push vedangi1018/chatapp-backend:latest

cd frontend
docker build -t vedangi1018/chatapp-frontend:latest . [To push image to my docker hub]
docker images
docker push vedangi1018/chatapp-frontend:latest

https://hub.docker.com/_/mongo

cd k8s
kubectl apply -f namespace.yml


ingress.yml
kubectl get ns (there will be no ingress-nginx in minikube)
minikube addons enable ingress (so add that)
kubectl get svc -n ingress-nginx
kubectl port-forward svc/ingress-nginx-controller -n ingress-nginx 80:80







