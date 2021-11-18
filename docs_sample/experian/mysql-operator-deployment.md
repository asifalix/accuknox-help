# MySQL Operator Deployment
**Note**
1. Do not change the namespace name.
If changes to the namespace are made, the you will need to change the service name & If the service name is changed, you will to need to change the microservice configmap files. (eg) app.yaml.
2. Please create a node pool on EKS / GKE / AKS (or) on-premises worker nodes with below Taints and Labels :
```
Taints - mysql:true 
Labels - mysql:true 
```
### Steps
1. Untar MySql deployment files
```
untar accuknox-dev-mysql.tar.xz
```
2. Create Namespace
```
kubectl create namespace accuknox-dev-mysql
```
3. Set Context
```
kubectl config set-context $(kubectl config current-context) --namespace=accuknox-dev-mysql
```
4. Change Directory
```
cd accuknox-dev-mysql
```
5. Apply the yaml files - in the order below
```
kubectl apply -f bundle.yaml 
kubectl apply -f cr.yaml 
kubectl apply -f secrets.yaml 
kubectl apply -f ssl-secrets.yaml 
kubectl apply -f backup-s3.yaml
```
6. Run a sanitary test with below commands at the mysql namespace
```
kubectl run -i --rm --tty percona-client --image=percona:8.0 --restart=Never -- bash -il
```
7. Login to MySql
```
mysql -h accuknox-dev-mysql-haproxy -uroot -proot_password
```
After successfully logging in, run any sanitary mysql query and validate it.

8. Update the passwords in secret.yaml file and run below command
```
kubectl apply -f secrets.yaml
```
9. Set FQDN (Kubernetes’s Service name) Value for Internal Cluster application
connectivity
```
FQDN: accuknox-dev-mysql-haproxy.accuknox-dev-mysql.svc.cluster.local
```
### Optional

To configure backup with GCS, add the HMAC keys in `backup-s3.yaml`, change the bucket name in `cr.yaml` and cron can be changed as required `cr.yaml` files.
