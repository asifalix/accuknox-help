# Experian POC: Installation & Deployment Steps for Various Modules

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
 - Setup a VM with Nginx as webserver and point to the HTML [UI build](*)

### 3. S3 Data Audit POC
 1. [Setup 5 S3 buckets (5 for Data Bucket, atleast 1 bucket for logs).](*)
 2. [Populate some files using the provided script.](*)
 3. [Setup the S3 Audit Log Reporter Agent in a VM.](*)
 4. Configure the data buckets and logs buckets in YAML file.

**Note:** Please install the pre-requisites below before proceeding with deploying the modules:
 - [MySql Operator](*)
 - [Kafka Operator](*)
 - [Pinot Deployment Steps](*)
 - [Istio & it's gateway installation](*)
##  Architecture Diagram
![DP architecture](https://user-images.githubusercontent.com/88204255/141889558-f6b52e7e-4d2a-4797-973f-c594cb8ebdac.png)
## Data Protection
### 1. Data-protection-management
1. Download tgz file of      data-protection-management
```
  data-protection-mgmt.tar.gz
```
2. Create namespace for data-protection-management
```
kubectl create namespace accuknox-dev-data-protection-mgmt
```
3. Install using Helm
```
helm upgrade --install data-protection- mgmt data-protection-mgmt.tar.gz –n accuknox-dev-data-protection-mgmt
```
4. Verify the installation of data-protection-management
```
kubectl get pods -n accuknox-dev-data-protection-mgmt
```
### 2. s3-audit-reporter-consumer
1. Download tgz file of s3-audit-reporter-consumer
```
s3-audit-reporter-consumer-charts.tar.gz
```
2. Create namespace for s3-audit-reporter-consumer
```
kubectl create namespace accuknox-dev- s3-audit-reporter-consumer
```
3. Install using helm
```
helm upgrade --install s3-audit-reporter-consumer s3-audit-reporter- consumer-charts.tar.gz –n accuknox-dev- s3-audit-reporter-consumer
```
4. Verify the installation of s3-audit-reporter-consumer
```
kubectl get pods -n accuknox-dev- s3-audit-reporter-consumer
```
### 3. agent-data-collector
1. Download tgz file of agent-data-collector
```
agent-data-collector-charts.tar.gz
```
2. Create namespace for agent-data-collector
```
kubectl create namespace accuknox-dev- agent-data-collector
```
3. Install using helm
```
helm upgrade --install agent-data-collector agent-data-collector-
charts.tar.gz –n accuknox-dev- agent-data-collector
```
4. Verify the installation of agent-data-collector
```
kubectl get pods -n accuknox-dev- agent-data-collector
```
### 4. s3-audit-reporter
1. Download tgz file of s3-audit-reporter
```
s3-audit-reporter-charts.tar.gz
```
2. Untar the file
```
tar -xvf s3-audit-reporter.tar.gz
```
3. Move to the directory of s3-audit-reporter
```
cd s3-audit-reporter
```
4. Create namespace for s3-audit-reporter
```
kubectl create namespace [namespace]
```
5. Install Configmap using kubectl, please update with your bucket details
```
kubectl apply –f dev-config.yaml –n [namespace]
```
6. Install Secrets using kubectl
```
kubectl apply –f dev-image-secrets.yaml–n [namespace]
kubectl apply –f dev-deployment.yaml–n [namespace]
```
7. Verify the installation of s3-audit-reporter
```
kubectl get pods -n [namespace]
```
## Data Pipeline
### 1. data-pipeline-api
1. Download tgz file
```
data-pipeline-api-charts.tar.gz
```
2. Create namespace for data-pippeline-api
```
kubectl create namespace accuknox-dev- datapippeline-api
```
3. Install using helm
```
helm upgrade --install data-pipeline-api data-pipeline-api-charts.tar.gz –n accuknox-dev- datapippeline-api
```
4. Verify the installation of data-pippeline-api. [Pods status should be running] 
```
kubectl get pods -n 
accuknox-dev- datapippeline-api
```
### 2. datapipeline-temporal:
1. Download tgz file
```
datapipeline-temporal-charts.tar.gz
```
2. Create namespace for datapipeline-temporal
```
kubectl create namespace accuknox-dev- temporal
```
3. Install using helm
```
helm upgrade --install datapipeline-temporal datapipeline-temporal-charts.tar.gz –n accuknox-dev- temporal
```
4. Verify the installation of datapipeline-temporal [Pods status should be running] 
```
kubectl get pods -n accuknox-dev- temporal
```
# User Management
### 1. Keycloak:
1. Download tgz file of keycloak-charts.tar.gz
```
keycloak.tar.gz
```
2. Create namespace for user-management-service & keycloak
```
kubectl create namespace accuknox-dev-user-mgmt
```
3. Install using helm
```
helm upgrade --install keycloak keycloak-charts.tar.gz -n accuknox-dev- user-mgmt
```
4. Verify the installation of keycloak [Pods status should be running]
```
kubectl get pods -n accuknox-dev-user-mgmt
```
### 2. user-management-service:
1. Download tgz file of user-management-service
```
user-management-service.tar.gz
```
2. Install using helm
```
helm upgrade --install user-mgmt user-management-service.tar.gz -n accuknox-dev-user-mgmt
```
Verify the installation of user-management-service [Pods status should be running]
```
kubectl get pods -n accuknox-dev-user-mgmt
```
### 3. UI
1. Install nginx application on VM

2. Configure the certmanager(https) (eg: letsencrypt)

3. Untar the build
```
tar -xvf build.tar.gz
```
```
sudo cp -rvf build/* /usr/share/nginx/html/accuknox-app
```
5. Start the service
