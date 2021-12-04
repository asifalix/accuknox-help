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

### Add accuknox repository to install Core Components helm package:

```sh
helm repo add accuknox-onprem-services https://USERNAME:PASSWORD@onprem.accuknox.com/repository/accuknox-onprem-services
helm repo update
helm search repo accuknox-onprem-services
```


<b>Follow the below order to install onprem-services on k8s cluster</b>

## Keycloak


Step 1 : 

```sh
kubectl create ns accuknox-user-mgmt
```

Step 2: 

```sh
helm upgrade --install accuknox-keycloak accuknox-onprem-services/keycloak-1.0.1.tgz -n accuknox-user-mgmt
```

## Usermanagement

helm upgrade --install accuknox-user-mgmt-service user-management-service-1.0.1.tgz -n accuknox-user-mgmt

## Agents-Auth-Service

Step 1 :

```sh
kubectl create ns accuknox-agents-auth-service
```

Step 2 :

```sh
helm upgrade --install  agents-auth-service-charts-1.0.1.tgz  -n accuknox-agents-auth-service
```

## Anomaly-detection-publisher-core

Step 1 : 

```sh
kubectl create ns accuknox-ad-core
```
Step 2 :

```sh
helm upgrade --install anomaly-detection-publisher-core-chart-1.0.1.tgz -n accuknox-ad-core
```

## Cluster-management-service

Step 1 : 

```sh
kubectl create ns accuknox-cluster-mgmt
```

Step 2 :

```sh
helm upgrade --install cluster-management-service-chart-1.0.1.tgz  -n accuknox-cluster-mgmt
```

## Anomaly-detection-management

Step 1 :

```sh
kubectl create ns accuknox-ad-mgmt
```

Step 2 :  

```sh
helm upgrade --install  anomaly-detection-mgmt-chart-1.0.1.tgz -n accuknox-ad-mgmt
```

## Data-protection-mgmt

Step 1 : 

```sh
kubectl create ns accuknox-dp-mgmt
```

Step 2 : 

```sh
helm upgrade --install data-protection-mgmt-1.0.1.tgz  -n accuknox-dp-mgmt
```

## Data-protection-core

Step 1 : 

```sh
kubectl create ns accuknox-dp-core
```

Step 2 :

```sh
helm upgrade --install data-protection-core-1.0.1.tgz  -n accuknox-dp-core
```

## Data-protection-consumer

Step 1 :

```sh
helm upgrade --install data-protection-consumer-1.0.1.tgz  -n accuknox-dp-core
```

## S3-audit-report-consumer

Step 1 : 

```sh
kubectl create ns accuknox-s3-audit-reporter-consumer
```

Step 2 :

```sh
helm upgrade --install s3-audit-reporter-consumer-charts-1.0.1.tgz  -n accuknox-s3-audit-reporter-consumer
```

## Dp-db-audit-log-processor

Step 1 : 

```sh
helm upgrade --install dp-db-audit-log-processor-chart-1.0.1.tgz  -n accuknox-dp-core
```

## Data-classification-pipeline-consumer

Step 1 :

```sh
kubectl create ns accuknox-data-classification-pipeline-consumer
```

Step 2 : 

```sh
helm upgrade --install data-classification-pipeline-consumer-chart-1.0.1.tgz  -n accuknox-data-classification-pipeline-consumer
```

## Agent-data-collector

Step 1 :

```sh
kubectl create ns accuknox-adc
```

Step 2 : 

```sh
helm upgrade --install agent-data-collector-charts-1.0.1.tgz   -n accuknox-adc
```

## Cluster-onboarding-service

Step 1 :

```sh
kubectl create ns accuknox-cluster-onboard
```

Step 2 : 

```sh
helm upgrade --install cluster-onboarding-service-1.0.1.tgz -n accuknox-cluster-onboard
```

## Cluster-entity-daemon

Step 1 : 
```sh
kubectl create ns accuknox-cluster-entity-daemon
```

Step 2 :

```sh
helm upgrade --install cluster-entity-daemon-chart-1.0.1.tgz -n accuknox-cluster-entity-daemon
```

## Shared-informer-service

Step 1 :
```sh
kubectl create ns accuknox-shared-informer-service
```

Step 2 :

```sh
helm upgrade --install shared-informer-service-chart-1.0.1.tgz  -n accuknox-shared-informer-service
```

## Data-pipeline-api

Step 1 : 

```sh
kubectl create ns accuknox-datapipeline-api
```

Step 2 : 

```sh
helm upgrade --install data-pipeline-api-charts-1.0.1.tgz -n accuknox-datapipeline-api
```

## Datapipeline-temporal

Step 1 : 
```sh
kubectl create ns accuknox-temporal
```

Step 2 : 
```sh
helm upgrade --install datapipeline-temporal-charts-1.0.1.tgz  -n accuknox-temporal
```

## Zookeeper

Step 1 :

```sh
kubectl create ns accuknox-samzajobs 
```
Step 2 :
```sh
helm upgrade --install zookeeper zookeeper-chart -n accuknox-samzajobs 
```

## Data-pipeline-samza-jobs

Step 1 : 
```sh
helm upgrade --install datapipeline-samza-1.0.1.tgz  -n accuknox-samzajobs
```

## Feeder-grpc-server

Step 1 : 

```sh
kubectl create ns accuknox-feeder-grpc-server
```

Step 2 :

```sh
helm upgrade --install feeder-grpc-server-chart-1.0.1.tgz -n accuknox-feeder-grpc-server
```

## Policy-service

Step 1 : 

```sh
kubectl create ns accuknox-policy-service
```

Step 2 :

```sh
helm upgrade --install policy-service-charts-1.0.1.tgz  -n accuknox-policy-service
```

## Policy-daemon

Step 1 : 

```sh
kubectl create ns accuknox-policy-daemon
```

Step 2 :

```sh
helm upgrade --install policy-daemon-charts-1.0.1.tgz  -n accuknox-policy-daemon
```

## Policy-provider-service

Step 1 : 

```sh
kubectl create ns accuknox-policy-provider-service
```

Step 2 : 

```sh
helm upgrade --install policy-provider-service-1.0.1.tgz -n accuknox-policy-provider-service
```

## Workload-identity-daemon

Step 1 :

```sh
kubectl create ns accuknox-workload-identity-daemon
```

Step 2 :

```sh
helm upgrade --install workload-identity-daemon-chart-1.0.1.tgz  -n accuknox-workload-identity-daemon
```

## Recommended-policy-daemon

Step 1 : 

```sh
kubectl create ns accuknox-recommended-policy-daemon
```

Step 2 : 

```sh
helm upgrade --install recommended-policy-daemon-1.0.1.tgz -n accuknox-recommended-policy-daemon
```

## Discoveredpolicy-daemon

Step 1 :

```sh
kubectl create ns accuknox-discovered-policy-daemon
```

Step 2 : 

```sh
helm upgrade --install discoveredpolicy-daemon-charts-1.0.1.tgz -n accuknox-discovered-policy-daemon
```

## Label-service

Step 1 :

```sh
kubectl create ns accuknox-label-service
```

Step 2 :

```sh
helm upgrade --install label-service-chart-1.0.1.tgz  -n accuknox-label-service
```


## Knox-auto-policy

Step 1 : 

```sh
kubectl create ns accuknox-knoxautopolicy
```

Step 2 : 

```sh
helm upgrade --install knox-auto-policy-chart-1.0.1.tgz  -n accuknox-knoxautopolicy
```


## Kvm-service

Step 1 :

```sh
kubectl create ns accuknox-kvmservice
```

Step 2 : 

```sh
helm upgrade --install kvm-service-chart-1.0.1.tgz  -n accuknox-kvmservice