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

#### Add accuknox repository to install Agents helm package:

```sh
helm repo add accuknox-onprem-agents https://USERNAME:PASSWORD@onprem.accuknox.com/repository/accuknox-onprem-agents
helm repo update
helm search repo accuknox-onprem-agents
```

<b>Follow the below order to install agents on k8s cluster.</b>


#### Cilium

Installation using Helm

Step 1: 
```sh
helm repo add cilium https://helm.cilium.io/
```
Step 2: 
```sh
helm install cilium cilium/cilium --version 1.10.5 --namespace kube-system
```
FYR: https://docs.cilium.io/en/v1.10/gettingstarted/k8s-install-helm/

## kArmor
kArmor is a CLI client to help manage KubeArmor.
KubeArmor is a container-aware runtime security enforcement system that restricts the behavior (such as process execution, file access, and networking operation) of containers at the system level.

## Installation

```sh
curl -sfL https://raw.githubusercontent.com/kubearmor/kubearmor-client/main/install.sh | sh
```

## To build and install, clone the repository and make install

FYR: https://github.com/kubearmor/kubearmor-client


### Shared-informer-agent

Step 1 : Create namespace has accuknox-shared-informer-agent

Eg: kubectl create ns accuknox-dev-shared-informer-agent

Step 2 :  Install using helm 

```sh
helm upgrade --install shared-informer-agent-chart-1.0.1.tgz  -n accuknox-shared-informer-agent
```

## S3-audit-reporter

Step 1 : Create namespace has accuknox-dev-s3-audit-reporter
Eg.
```sh
kubectl create ns accuknox-s3-audit-reporter
```
Step 2 :  Install using helm 

Eg.
```sh
helm upgrade --install s3-audit-reporter-charts-1.0.1.tgz   -n  accuknox-s3-audit-reporter
```

## Feeder-Service

Step 1 : Create namespace has feeder-service
Eg.
```sh
kubectl create ns feeder-service
```

Step 2 :  Install using helm 

Eg.

```sh
helm upgrade --install feeder-service-1.0.1.tgz  -n  feeder-service
```

## Knox-Containersec

Step 1 : Create namespace has accuknox-onprem-agents

```sh
kubectl create ns accuknox-agents
```

Step 2 :  Install using helm 

Eg.
```sh
helm upgrade --install knox-containersec-chart-1.0.1.tgz  -n  accuknox-agents
```

## Policy Enforcement Agent 

Install using helm 

```sh
helm upgrade --install policy-enforcement-agent-1.0.1.tgz  -n  accuknox-agents
```
