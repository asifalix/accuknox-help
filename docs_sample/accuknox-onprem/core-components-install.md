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

## User-management-service:

Step 1 : Create namespace has accuknox-dev-user-mgmt

Eg.

```sh
kubectl create ns accuknox-dev-user-mgmt
```
Step 2 : Install using helm 

Eg.

```sh 
helm upgrade --install user-management-service-1.0.1.tgz -n accuknox-dev-user-mgmt
```

## Agents-Auth-Service

Step 1 : Create namespace has accuknox-dev-agents-auth-service

Eg.

```sh
kubectl create ns accuknox-dev-agents-auth-service
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install  agents-auth-service-charts-1.0.1.tgz  -n accuknox-dev-agents-auth-service
```

## Anomaly-detection-management

Step 1 : Create namespace has  accuknox-dev-ad-mgmt

Eg. 

```sh
kubectl create ns accuknox-dev-ad-mgmt
```

Step 2 :  Install using helm 

Eg.

```sh
helm upgrade --install  anomaly-detection-mgmt-chart-1.0.1.tgz -n accuknox-dev-ad-mgmt
```

## Anomaly-detection-publisher-core

Step 1 : Create namespace has accuknox-dev-ad-core

Eg.
```sh
kubectl create ns accuknox-dev-ad-core
```
Step 2 : Install using helm 

Eg. 

```sh
helm upgrade --install anomaly-detection-publisher-core-chart-1.0.1.tgz -n accuknox-dev-ad-core
```

## Data-protection-mgmt

Step 1 : Create namespace has accuknox-dev-dp-mgmt

Eg.

```sh
kubectl create ns accuknox-dev-dp-mgmt
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install data-protection-mgmt-1.0.1.tgz  -n accuknox-dev-dp-mgmt
```

## Data-protection-core

Step 1 : Create namespace has accuknox-dev-dp-core

Eg.

```sh
kubectl create ns accuknox-dev-dp-core
```

Step 2 : Install using helm 
         
Eg. 

```sh
helm upgrade --install data-protection-core-1.0.1.tgz  -n accuknox-dev-dp-core
```

## Data-protection-consumer

Step 1 : Create namespace has accuknox-dev-dp-core   (Optional Step - Since namespace Created )

Eg.

```sh
kubectl create ns accuknox-dev-dp-core
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install data-protection-consumer-1.0.1.tgz  -n accuknox-dev-dp-core
```

## S3-audit-report-consumer

Step 1 : Create namespace has accuknox-dev-s3-audit-reporter-consumer

Eg. 

```sh
kubectl create ns accuknox-dev-s3-audit-reporter-consumer
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install s3-audit-reporter-consumer-charts-1.0.1.tgz  -n accuknox-dev-s3-audit-reporter-consumer
```

## Dp-db-audit-log-processor

Step 1 : Create namespace has accuknox-dev-dp-core

```sh
kubectl create ns accuknox-dev-dp-core
```

Step 2 : Install using helm 

Eg. 

```sh
helm upgrade --install dp-db-audit-log-processor-chart-1.0.1.tgz  -n accuknox-dev-dp-core
```

## Data-classification-pipeline-consumer

Step 1 : Create namespace has accuknox-dev-data-classification-pipeline-consumer

Eg.

```sh
kubectl create ns accuknox-dev-data-classification-pipeline-consumer
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install data-classification-pipeline-consumer-chart-1.0.1.tgz  -n accuknox-dev-data-classification-pipeline-consumer
```

## Cluster-management-service

Step 1 : Create namespace has accuknox-dev-cluster-mgmt

Eg.

```sh
kubectl create ns accuknox-dev-cluster-mgmt
```

Step 2 : Install using helm 

Eg. 

```sh
helm upgrade --install cluster-management-service-chart-1.0.1.tgz  -n accuknox-dev-cluster-mgmt
```

## Agent-data-collector

Step 1 : Create namespace has accuknox-dev-adc
Eg. 

```sh
kubectl create ns accuknox-dev-adc
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install agent-data-collector-charts-1.0.1.tgz   -n accuknox-dev-adc
```

## Cluster-onboarding-service

Step 1 : Create namespace has accuknox-dev-cluster-onboard
         
Eg. 

```sh
kubectl create ns accuknox-dev-cluster-onboard
```

Step 2 : Install using helm 

Eg. 

```sh
helm upgrade --install cluster-onboarding-service-1.0.1.tgz  -n accuknox-dev-cluster-onboard
```

## Cluster-entity-daemon

Step 1 : Create namespace has accuknox-dev-cluster-entity-daemon

Eg: 

```sh
kubectl create ns accuknox-dev-cluster-entity-daemon
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install cluster-entity-daemon-chart-1.0.1.tgz    -n accuknox-dev-cluster-entity-daemon
```

## Shared-informer-service

Step 1 : Create namespace has accuknox-dev-shared-informer-service

Eg.

```sh
kubectl create ns accuknox-dev-shared-informer-service
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install shared-informer-service-chart-1.0.1.tgz  -n accuknox-dev-shared-informer-service
```

## Data-pipeline-api

Step 1 : Create namespace has accuknox-dev-datapipeline-api

Eg. 

```sh
kubectl create ns accuknox-dev-datapipeline-api
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install data-pipeline-api-charts-1.0.1.tgz -n accuknox-dev-datapipeline-api
```

## Datapipeline-temporal

Step 1 : Create namespace has accuknox-dev-temporal

Eg.

```sh
kubectl create ns accuknox-dev-temporal
```

Step 2 : Install using helm 

Eg. 

```sh
helm upgrade --install datapipeline-temporal-charts-1.0.1.tgz  -n accuknox-dev-temporal
```

## Data-pipeline-samza-jobs

Step 1 : Create namespace has accuknox-dev-samzajobs

Eg. 

```sh
kubectl create ns accuknox-dev-samzajobs
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install datapipeline-samza-1.0.1.tgz  -n accuknox-dev-samzajobs
```

## Feeder-grpc-server

Step 1 : Create namespace has accuknox-dev-feeder-grpc-server

Eg. 

```sh
kubectl create ns accuknox-dev-feeder-grpc-server
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install feeder-grpc-server-chart-1.0.1.tgz -n accuknox-dev-feeder-grpc-server
```

Policy-service

Step 1 : Create namespace has accuknox-dev-policy-service

Eg. 

```sh
kubectl create ns accuknox-dev-policy-service
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install policy-service-charts-1.0.1.tgz  -n accuknox-dev-policy-service
```

## Policy-daemon

Step 1 : Create namespace has accuknox-dev-policy-daemon

Eg. 

```sh
kubectl create ns accuknox-dev-policy-daemon
```

Step 2 : Install using helm 

Eg. 

```sh
helm upgrade --install policy-daemon-charts-1.0.1.tgz  -n accuknox-dev-policy-daemon
```

## Policy-provider-service

Step 1 : Create namespace has accuknox-dev-policy-provider-service

Eg.

```sh
kubectl create ns accuknox-dev-policy-provider-service
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install policy-provider-service-1.0.1.tgz -n accuknox-dev-policy-provider-service
```

## Workload-identity-daemon

Step 1 : Create namespace has accuknox-dev-workload-identity-daemon

Eg.

```sh
kubectl create ns accuknox-dev-workload-identity-daemon
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install workload-identity-daemon-chart-1.0.1.tgz  -n accuknox-dev-workload-identity-daemon
```

## Recommended-policy-daemon

Step 1 : Create namespace has accuknox-dev-recommended-policy-daemon

Eg.

```sh
kubectl create ns accuknox-dev-recommended-policy-daemon
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install recommended-policy-daemon-1.0.1.tgz -n accuknox-dev-recommended-policy-daemon
```

Discoveredpolicy-daemon

Step 1 : Create namespace has accuknox-dev-discovered-policy-daemon

Eg. 

```sh
kubectl create ns accuknox-dev-discovered-policy-daemon
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install discoveredpolicy-daemon-charts-1.0.1.tgz -n accuknox-dev-discovered-policy-daemon
```

## Label-service

Step 1 : Create namespace has accuknox-dev-label-service

Eg.

```sh
kubectl create ns accuknox-dev-label-service
```

Step 2 : Install using helm 

Eg.

```sh
helm upgrade --install label-service-chart-1.0.1.tgz  -n accuknox-dev-label-service
```


## Knox-auto-policy

Step 1 : Create namespace has accuknox-dev-knoxautopolicy

Eg.

```sh
kubectl create ns accuknox-dev-knoxautopolicy
```

Step 2 : Install using helm 

Eg. 

```sh
helm upgrade --install knox-auto-policy-chart-1.0.1.tgz  -n accuknox-dev-knoxautopolicy
```


## Kvm-service

Step 1 : Create namespace has accuknox-dev-kvmservice

Eg.

```sh
kubectl create ns accuknox-dev-kvmservice
```

Step 2 : Install using helm 

Eg. 

```sh
helm upgrade --install kvm-service-chart-1.0.1.tgz  -n accuknox-dev-kvmservice