# IAM
Access key ID,Secret access key
AKIAVLBFLXW4KRLJTCFB,2QDN26//Koqo9p0bY/685N6BOBbcgHIT11ZQ15zW
# 
source set_env.sh

1. aws eks update-kubeconfig --region us-east-1 --name Datpt57Cluster
2. kubectl get node
3. kubectl get svc

#  Apply kubectl
kubectl apply -f ./myconfig/aws-secret.yaml
kubectl apply -f ./myconfig/env-secret.yaml
kubectl apply -f ./myconfig/env-configmap.yaml

# Aplly deployment
kubectl apply -f ./myconfig/api-feed-deployment.yaml
kubectl apply -f ./myconfig/api-user-deployment.yaml
kubectl apply -f ./myconfig/frontend-deployment.yaml
kubectl apply -f ./myconfig/reverseproxy-deployment.yaml

# Aplly service
kubectl apply -f ./myconfig/api-feed-service.yaml
kubectl apply -f ./myconfig/api-user-service.yaml
kubectl apply -f ./myconfig/frontend-service.yaml
kubectl apply -f ./myconfig/reverseproxy-service.yaml

# check deployment
## Check the deployment names and their pod status
kubectl get deployments
## Create a Service object that exposes the frontend deployment
## The command below will ceates an external load balancer and assigns a fixed, external IP to the Service.
kubectl expose deployment frontend --type=LoadBalancer --name=publicfrontend
kubectl expose deployment reverseproxy --type=LoadBalancer--name=publicreverseproxy
## Repeat the process for the *reverseproxy* deployment. 
## Check name, ClusterIP, and External IP of all deployments
kubectl get services 
kubectl get pods 
# It should show the STATUS as Running
