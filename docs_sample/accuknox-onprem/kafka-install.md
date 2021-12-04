## Note:
Kafka Operator Deployment
1. Don't change the namespace name because if you change the namespace - You need to change the service name , If the service name is changed ,then you need to change the microservice configmap files . eg: app.yaml.

2. Please create a node pool on EKS / GKE / AKS (or) on-premises worker nodes with below Taints and labels

<b>Taints - kafka:true 

Labels - kafka:true</b>

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


Add accuknox repository to install strimzi-kafka-operator helm package:

```sh
helm repo add accuknox-onprem-prerequisites https://USERNAME:PASSWORD@onprem.accuknox.com/repository/accuknox-onprem-prerequisites
helm repo update
helm search repo accuknox-onprem-prerequisites
helm pull accuknox-onprem-prerequisites/strimzi-kafka-operator --untar
```
```sh
kubectl create namespace accuknox-kafka
```
```sh
helm install accuknox-kafka  strimzi-kafka-operator -n accuknox-kafka
```

Check the Pods deployment
```sh
kubectl get pods -n accuknox-kafka
```

Extract the connectivity information.

## Get bootstrap server endpoint
```sh
kubectl get kafka accuknox-kafka -o jsonpath='{.status.listeners[?(@.type=="external")].bootstrapServers}' -n accuknox-kafka
```
## Get CA
```sh
kubectl get secret accuknox-kafka-cluster-ca-cert -o jsonpath='{.data.ca\.p12}' -n accuknox-kafka | base64 -d > ca.p12
```

Note:

For any application connecting to Kafka outside the GKE, It needs to communicate via SSL/TLS authentication.

We need to provide the connectivity details to the component owners who are configuring the application deployed outside GKE Cluster..

## Get CA Password
```sh
kubectl get secret accuknox-kafka-cluster-ca-cert -o jsonpath='{.data.ca\.password}' -n accuknox-kafka | base64 -d > ca.password
```

## Get User Cert
```sh
kubectl get secret/node-event-feeder-common -n accuknox-kafka -o jsonpath='{.data.user\.p12}' | base64 -d > user.p12
```
## Get user password
```sh
kubectl get secret/node-event-feeder-common -n accuknox-kafka -o jsonpath='{.data.user\.password}' | base64 -d > user.password
```
## Convert user.p12 into base64
```sh
cat user.p12 | base64 > user.p12.base64
```
## Convert ca.p12 into base64
```sh
cat ca.p12 | base64 > ca.p12.base64
```

## Convert ca.password into base64
```sh
cat ca.password | base64 > ca.password.base64
```
## Convert user.password into base64
```sh
cat user.password | base64 > user.password.base64
```
## Convert p12 to pem
```sh
openssl pkcs12 -in ca.p12 -out ca.pem
```

![Alt](../images/ca-user-verify.png)

Note: copy the password from ca.password (file)

## Convert ca.pem to base64
```sh
cat ca.pem | base64 > ca.pem.base64
```
Note: ca.p12, ca.password, user.p12 and user.password are required to be used in Java based applications. For Go based applications, use ca.pem, user.p12 and user.password. For use in Kubernetes, use the base64 versions of respective files.

FQDN (K8’s Service name) Value for Internal Cluster application connectivity.

FQDN : accuknox-kafka-bootstrap.accuknox-kafka.svc.cluster.local:9092

## Get Certificates and store it
NOTE: 

1. If kafka cluster is upgraded or reinstalled, then cluster will generate new certificates and you need to change/update key-pair in the kafka clients or applications. 

2. To mitigate this issue store these below certificates in safe place at the time of installing kafka(first time installation).

3. Manually apply these certificates using "kubectl" command or place under templetes folder.
And also turn off the auto certificate generation by configuring(uncomment) "clusterca" and "clientsca" to "false" in "kafka-cluster.yaml" file(below image is for your reference). Once done the changes, install/upgarde the cluster.

![Alt](../images/kafka-cert-ref.png)

```sh
kubectl get secret/accuknox-clients-ca -o yaml -n accuknox-kafka > accuknox-clients-ca.yaml
kubectl get secret/accuknox-clients-ca-cert -o yaml -n accuknox-kafka > accuknox-clients-ca-cert.yaml
kubectl get secret/accuknox-cluster-ca-cert -o yaml -n accuknox-kafka > accuknox-cluster-ca-cert.yaml
kubectl get secret/accuknox-cluster-ca -o yaml -n accuknox-kafka > accuknox-cluster-ca.yaml
kubectl get secret/node-event-feeder -o yaml -n accuknox-kafka > node-event-feeder.yaml
kubectl get secret/node-event-feeder-common -o yaml -n accuknox-kafka > node-event-feeder-common.yaml
```

