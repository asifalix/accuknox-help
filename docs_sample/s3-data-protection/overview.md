# S3 Data Protection - Installation & Deployment Steps for Various Modules

## Installation Flow
### 1. Backend Platform
 - Kubernetes cluster
 - Installing the backend software components in the kubernetes cluster
    1.  Setup Databases - MySQL, Pinot
    2. Setup Kafka
    3. Install Istio in Kubernetes
    4. Microservices
    5. Setup Istio API Gateway (Internal)

### 2. UI - Frontend
 - Setup a VM with Nginx as webserver and point to the HTML [UI build](https://help.accuknox.com/s3-data-protection/s3-data-protection-poc/#3_ui)

### 3. S3 Data Audit POC
 1. [Setup 5 S3 buckets (5 for Data Bucket, atleast 1 bucket for logs).](https://help.accuknox.com/s3-data-protection/s3-access-audit/)
 2. [Populate some files using the provided script.](https://help.accuknox.com/s3-data-protection/s3-data-protection-poc-test-scenarios/)
 3. [Setup the S3 Audit Log Reporter Agent in a VM.](https://help.accuknox.com/s3-data-protection/pre-requisites-s3-audit-reportor/)
 4. Configure the data buckets and logs buckets in YAML file.

**Note:** Please install the pre-requisites below before proceeding with deploying the modules:

 - [MySql Operator](https://help.accuknox.com/s3-data-protection/mysql-operator-deployment/)
 - [Kafka Operator](https://help.accuknox.com/s3-data-protection/kafka-operator-deployment/)
 - [Pinot Deployment Steps](https://help.accuknox.com/s3-data-protection/pinot-deployment/)
 - [Istio & it's gateway installation](https://help.accuknox.com/s3-data-protection/istio-depolyment/)

##  Architecture Diagram
![DP architecture](https://user-images.githubusercontent.com/88204255/141889558-f6b52e7e-4d2a-4797-973f-c594cb8ebdac.png)

## Data Protection
### 1. Data-protection-management

 - Download tgz file of data-protection-management
```
data-protection-mgmt.tar.gz
```

 - Create namespace for data-protection-management
```sh
kubectl create namespace accuknox-dev-data-protection-mgmt
```

 - Install using Helm
```sh
helm upgrade --install data-protection- mgmt data-protection-mgmt.tar.gz –n accuknox-dev-data-protection-mgmt
```

 - Verify the installation of data-protection-management
```sh
kubectl get pods -n accuknox-dev-data-protection-mgmt
```

### 2. s3-audit-reporter-consumer
 - Download tgz file of s3-audit-reporter-consumer
```
s3-audit-reporter-consumer-charts.tar.gz
```
 - Create namespace for s3-audit-reporter-consumer
```sh
kubectl create namespace accuknox-dev- s3-audit-reporter-consumer
```
 - Install using helm
```sh
helm upgrade --install s3-audit-reporter-consumer s3-audit-reporter- consumer-charts.tar.gz –n accuknox-dev- s3-audit-reporter-consumer
```
 - Verify the installation of s3-audit-reporter-consumer
```sh
kubectl get pods -n accuknox-dev- s3-audit-reporter-consumer
```

### 3. agent-data-collector
 - Download tgz file of agent-data-collector
```
agent-data-collector-charts.tar.gz
```
 - Create namespace for agent-data-collector
```sh
kubectl create namespace accuknox-dev- agent-data-collector
```
 - Install using helm
```sh
helm upgrade --install agent-data-collector agent-data-collector-
charts.tar.gz –n accuknox-dev- agent-data-collector
```
 - Verify the installation of agent-data-collector
```sh
kubectl get pods -n accuknox-dev- agent-data-collector
```

### 4. s3-audit-reporter
 - Download tgz file of s3-audit-reporter
```
s3-audit-reporter-charts.tar.gz
```
 - Untar the file
```sh
tar -xvf s3-audit-reporter.tar.gz
```
 - Move to the directory of s3-audit-reporter
```
cd s3-audit-reporter
```
 - Create namespace for s3-audit-reporter
```sh
kubectl create namespace [namespace]
```
 - Install Configmap using kubectl, please update with your bucket details
```sh
kubectl apply –f dev-config.yaml –n [namespace]
```
 - Install Secrets using kubectl
```sh
kubectl apply –f dev-image-secrets.yaml–n [namespace]
kubectl apply –f dev-deployment.yaml–n [namespace]
```
 - Verify the installation of s3-audit-reporter
```sh
kubectl get pods -n [namespace]
```

## Data Pipeline
### 1. data-pipeline-api
 - Download tgz file
```
data-pipeline-api-charts.tar.gz
```
 - Create namespace for data-pippeline-api
```sh
kubectl create namespace accuknox-dev- datapippeline-api
```
 - Install using helm
```sh
helm upgrade --install data-pipeline-api data-pipeline-api-charts.tar.gz –n accuknox-dev- datapippeline-api
```
 - Verify the installation of data-pippeline-api. [Pods status should be running] 
```sh
kubectl get pods -n accuknox-dev- datapippeline-api
```

### 2. datapipeline-temporal:
 - Download tgz file
```
datapipeline-temporal-charts.tar.gz
```
 - Create namespace for datapipeline-temporal
```sh
kubectl create namespace accuknox-dev- temporal
```
 - Install using helm
```sh
helm upgrade --install datapipeline-temporal datapipeline-temporal-charts.tar.gz –n accuknox-dev- temporal
```
 - Verify the installation of datapipeline-temporal [Pods status should be running] 
```sh
kubectl get pods -n accuknox-dev- temporal
```

# User Management
### 1. Keycloak:
 - Download tgz file of keycloak-charts.tar.gz
```
keycloak.tar.gz
```
 - Create namespace for user-management-service & keycloak
```sh
kubectl create namespace accuknox-dev-user-mgmt
```
 - Install using helm
```sh
helm upgrade --install keycloak keycloak-charts.tar.gz -n accuknox-dev- user-mgmt
```
 - Verify the installation of keycloak [Pods status should be running]
```sh
kubectl get pods -n accuknox-dev-user-mgmt
```

### 2. user-management-service:
 - Download tgz file of user-management-service
```
user-management-service.tar.gz
```
 - Install using helm
```sh
helm upgrade --install user-mgmt user-management-service.tar.gz -n accuknox-dev-user-mgmt
```
 - Verify the installation of user-management-service [Pods status should be running]
```sh
kubectl get pods -n accuknox-dev-user-mgmt
```

### 3. UI
 - Install nginx application on VM
 - Configure the certmanager(https) (eg: letsencrypt)
 - Untar the build
```sh
tar -xvf build.tar.gz
```
```sh
sudo cp -rvf build/* /usr/share/nginx/html/accuknox-app
```
 - Start the service
