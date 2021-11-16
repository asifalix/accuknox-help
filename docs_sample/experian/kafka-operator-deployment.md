# Kafka Operator Deployment
**Note**
1. Do not change the namespace name. If changes to the namespace are made, the you will need to change the service name & If the service name is changed, you will to need to change the microservice configmap files. (eg) app.yaml.
2. Please create a node pool on EKS / GKE / AKS (or) on-premises worker nodes with below Taints and Labels:
```
Taints - kafka:true 
Labels - kafka:true 
```
### Steps
1. Untar the Kafka deployment files
```
untar saas-kafka-Experian.tar.xz
```
2. Create Namespace
```
kubectl create namespace accuknox-dev-kafka
```
3. Set Context
```
kubectl config set-context --current --namespace=accuknox-dev-kafka
```
4. Install the Helm pkg
```
helm install dev-kafka saas-kafka
```
5. Check the Pods deployment
```
kubectl get pods -n accuknox-dev-kafka
```
6. Extract the connectivity information
```
## Get bootstrap server endpoint
kubectl get kafka dev-kafka -o jsonpath='{.status.listeners[?(@.type=="external")].bootstrapServers}' -n accuknox-dev-kafka

## Get CA 
kubectl get secret dev-kafka-cluster-ca-cert -o jsonpath='{.data.ca\.p12}' -n accuknox-dev-kafka | base64 -d > ca.p12 

## Get CA Password 
kubectl get secret dev-kafka-cluster-ca-cert -o jsonpath='{.data.ca\.password}' -n accuknox-dev-kafka | base64 -d > ca.password 

## Get User Cert 
kubectl get secret/node-event-feeder-common -n accuknox-dev-kafka -o jsonpath='{.data.user\.p12}' | base64 -d > user.p12 

## Get user password 
kubectl get secret/node-event-feeder-common -n accuknox-dev-kafka -o jsonpath='{.data.user\.password}' | base64 -d > user.password

## Convert user.p12 into base64
cat user.p12 | base64 > user.p12.base64

## Convert ca.p12 into base64
cat ca.p12 | base64 > ca.p12.base64 

## Convert ca.password into base64
cat ca.password | base64 > ca.password.base64 

## Convert user.password into base64 
cat user.password | base64 > user.password.base64 

## Convert p12 to pem 
openssl pkcs12 -in ca.p12 -out ca.pem 

## Convert ca.pem to base64 
cat ca.pem | base64 > ca.pem.base64 
```
### Note
1. ca.p12, ca.password, user.p12 and user.password are required to be used in Java based applications.
2. For Go based applications, use ca.pem, user.p12 and user.password.
3. In Kubernetes, use the base64 versions of respective files.
#### Set FQDN (Kubernetes’s Service name) Value for Internal Cluster application
connectivity
```
FQDN : dev-kafka-kafka-bootstrap.accuknox-dev-kafka.svc.cluster.local:9092
```
