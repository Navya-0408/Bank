# Bank   this is navya
===nagios==
 docker pull jasonrivers/nagios:latest
 docker images
 docker run --name nagios4 -d -p 8888:80 jasonrivers/nagios:latest
 docker start -ai nagios4
 *open browser type localhost:8888
     username: nagiosadmin
     pw: nagios

===kubernets===
minikube start
docker login
minikube version
minikube status
kubectl create deployment myngnix --image=ngnix
kubectl get deployment
kubectl get pods
kubectl describe pods 
kubectl expose deployment myngnix --type-Nodeport --port=80 --target-port=80 --name=myngnix
kubectl get service myngnix
kubectl port-forward sevice/myngnix 3080:80
openbrowser and in url 127.0.0.1-3080
....
then open another powershell and 
minikube dashboard

     
