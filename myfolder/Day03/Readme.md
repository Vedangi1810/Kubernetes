**Jobs and Cron Jobs:**



job.yml

kubectl appy -f job.yml

kubectl get Job -n nginx

kubectl get pods -n nginx

kubectl logs pod/nging-job-xxxx -n nginx



cron-job.yml

kubectl appy -f cron-job.yml

kubectl get CronJob -n nginx

kubectl get pods -n nginx

kubectl logs pod/nginx-job-xxxx -n nginx



Storage:



pv.yaml



pvc.yaml



deployment.yaml



kubectl get pods -n nginx -o wide (get on which node it's running)



way 01: Check Inside Pod (Mounted Path)

kubectl exec -it <pod\_name> -n nginx -- /bin/sh

df -h

ls -l /usr/share/nginx/html



way 02: See Detailed Mount Info

kubectl describe <pod\_name> -n nginx



way 03: Where Is Actual Data Stored? (Since You Use hostPath)

If your pv uses hostPath,

Since you are using KIND:

That path exists inside the KIND node container.

So:

docker ps (get id of that container)

docker exec -it <cont\_id> -- /bin/sh

ls -l /mnt/data



Pod path → /usr/share/nginx/html

PV hostPath → /mnt/data

