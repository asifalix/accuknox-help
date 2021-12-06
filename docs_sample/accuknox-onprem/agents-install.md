### Note

Step 1: Onboarding the cluster to the accuknox UI (Eg. CWPP cluster).

Step 2: Fetch the cluster id and workload id for the below agents installation.

![Alt](../images/onboard.png)

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

Cilium is open source software for transparently securing the network connectivity between application services deployed using Linux container management platforms like Docker and Kubernetes.

At the foundation of Cilium is a new Linux kernel technology called BPF, which enables the dynamic insertion of powerful security visibility and control logic within Linux itself. Because BPF runs inside the Linux kernel, Cilium security policies can be applied and updated without any changes to the application code or container configuration.

## Installation

Note 1.10.5 having crashingloopback issues, so we are using 1.9.8

```sh
curl -L --remote-name-all https://github.com/cilium/cilium-cli/releases/latest/download/cilium-linux-amd64.tar.gz{,.sha256sum} sha256sum --check cilium-linux-amd64.tar.gz.sha256sum

sudo tar xzvfC cilium-linux-amd64.tar.gz /usr/local/bin

rm cilium-linux-amd64.tar.gz{,.sha256

cilium install --version 1.9.8

cilium hubble enable
```
## Validate the cilium Installation

To validate that Cilium has been properly installed, you can run

```sh
cilium status --wait
```

![Alt](../images/cilium-status.png)

![Alt](../images/cilium-pods.png)

Refer official site: [https://docs.cilium.io/en/stable/gettingstarted/k8s-install-default/](https://docs.cilium.io/en/stable/gettingstarted/k8s-install-default/) 

## kArmor cli tool
kArmor is a CLI client to help manage KubeArmor.
kArmor tool can be used to install/uninstall kubearmor. Additionally it can be used to view kubearmor logs and other resources used by kubearmor.

## Installation

```sh
curl -sfL https://raw.githubusercontent.com/kubearmor/kubearmor-client/main/install.sh | sh
```
```sh
karmor install	#Installs Kubearmor
```

```sh
kubectl get pods -n kubesystem | grep kubearmor
```
![Alt](../images/kubearmor.png)

FYR: [https://github.com/kubearmor/kubearmor-client](https://github.com/kubearmor/kubearmor-client)

Refer official site: [https://www.accuknox.com/kubearmor/](https://www.accuknox.com/kubearmor/)

### Shared-informer-agent

```sh
kubectl create ns accuknox-agents
```

```sh
helm upgrade --install accuknox-shared-informer-agent shared-informer-agent-chart-1.0.1.tgz -n accuknox-agents
```

## Policy Enforcement Agent 

```sh
kubectl create ns policy-agent
```

```sh
helm upgrade --install accuknox-policy-enforcement-agent policy-enforcement-agent-1.0.1.tgz -n policy-agent
```

```sh
kubectl set env deploy/policy-enforcement-agent -n policy-agent workspace_id=<wid>
```

Note: wid - workspace id number fetch from Accuknox UI.

## Feeder-Service

```sh
kubectl create ns accuknox-feeder-service
```
```sh
helm upgrade --install accuknox-feeder-service feeder-service-1.0.1.tgz -n accuknox-feeder-service
```
## Knox-Containersec

```sh
helm upgrade --install accuknox-knox-containersec knox-containersec-chart-1.0.1.tgz -n accuknox-agents
```

## S3-audit-reporter

```sh
kubectl create ns accuknox-s3-audit-reporter-agent
```
```sh
helm upgrade --install accuknox-s3-audit-reporter-agent s3-audit-reporter-charts-1.0.1.tgz -n accuknox-s3-audit-reporter-agent
```
