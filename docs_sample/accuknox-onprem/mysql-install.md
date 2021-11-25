### Note:
1. Don't change the namespace name because if you change the namespace - You need to change the service name , If the service name is changed ,then you  
need to change the microservice configmap files . eg: app.yaml.

2. Please create a node pool on EKS / GKE / AKS (or) on-premises worker nodes with below Taints and labels

<b>Taints - mysql:true 

Labels - mysql:true</b>

### Installing Helm
This guide shows how to install the Helm CLI. Helm can be installed either from source, or from pre-built binary releases.

### From the Binary Releases

Every [release](https://github.com/helm/helm/releases) of Helm provides binary releases for a variety of OSes. These binary versions can be manually downloaded and installed.

Download your [desired version](https://github.com/helm/helm/releases)

Unpack it <b>(tar -zxvf helm-v3.0.0-linux-amd64.tar.gz)</b>

Find the helm binary in the unpacked directory, and move it to its desired destination <b>(mv linux-amd64/helm /usr/local/bin/helm)</b>

<b>Note:</b> Helm automated tests are performed for Linux AMD64 only during CircleCi builds and releases. Testing of other OSes are the responsibility of the community requesting Helm for the OS in question.

<b>For more reference:</b> [Click here..](https://helm.sh/docs/intro/install/)

---


Add accuknox repository to install  Mysql Percona helm package:
```sh
helm repo add accuknox-onprem-prerequisites https://USERNAME:PASSWORD@onprem.accuknox.com/repository/accuknox-onprem-prerequisites
helm repo update
helm search repo accuknox-onprem-prerequisites
helm pull accuknox-onprem-prerequisites/mysql-chart --untar
```
```sh
kubectl create namespace accuknox-mysql
cd mysql-chart 
kubectl apply -f bundle.yaml -n accuknox-mysql
kubectl apply -f cr.yaml -n accuknox-mysql
kubectl apply -f secrets.yaml -n accuknox-mysql
kubectl apply -f ssl-secrets.yaml -n accuknox-mysql
```
![Alt](../images/mysql-ssl-check.png)

```sh
kubectl apply -f backup-s3.yaml -n accuknox-mysql
```

## Note

1. To configure backup with gcs, add the HMAC keys in backup-s3.yaml, change the bucket name in cr.yaml and change the cron job entries as per the requirement in the cr.yaml.

2. HMAC Keys will vary for cloud providers . (GCP, AZURE,  AWS


After following steps the above steps, you will see a similar image as above 
Run a sanitary test with below commands at the mysql namespace

```sh
kubectl run -i --rm --tty percona-client --image=percona:8.0 --restart=Never -n accuknox-mysql -- bash -il 
mysql -h accuknox-mysql-haproxy -uroot -proot_password
```

Update the passwords in secret.yaml file and run below command

```sh
kubectl apply -f secrets.yaml
```
Optional To configure backup with gcs add the HMAC keys in backup-s3.yaml, change the bucket name in cr.yaml and cron can be changed as required cr.yaml files.

FQDN: For K8’s Service name

#### accuknox-mysql-haproxy.accuknox-mysql.svc.cluster.local