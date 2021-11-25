### Note:
Pinot Operator Deployment
1. Don't change the namespace name because if you change the namespace - You need to change the service name , If the service name is changed ,then you need to change the microservice configmap files . eg: app.yaml.

2. Please create a node pool on EKS / GKE / AKS (or) on-premises worker nodes with below Taints and labels

<b>Taints - pinot:true

Labels - pinot:true</b>


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

Add accuknox repository to install Pinot helm package

```sh
helm repo add accuknox-onprem-prerequisites https://USERNAME:PASSWORD@onprem.accuknox.com/repository/accuknox-onprem-prerequisites
helm repo update
helm search repo accuknox-onprem-prerequisites
helm pull accuknox-onprem-prerequisites/pinot-chart --untar
```
```sh
kubectl create namespace accuknox-pinot
```

```sh
helm install accuknox-pinot pinot -n accuknox-pinot
```