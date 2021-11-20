# Istio Deployment
## What is Istio?
Istio is an open source service mesh that layers transparently onto existing distributed applications. Istio’s powerful features provide a uniform and more efficient way to secure, connect, and monitor services. Istio is the path to load balancing, service-to-service authentication, and monitoring – with few or no service code changes. Its powerful control plane brings vital features, including:
* Secure service-to-service communication in a cluster with TLS encryption, strong identity based authentication and authorization

* Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic  Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection

* A pluggable policy layer and configuration API supporting access controls, rate limits and quotas

* Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress
![istio deployment](https://user-images.githubusercontent.com/88204255/141981336-6687225d-1aba-401e-a543-c79c87d0066d.png)


## Installation Steps
1. Go to the Istio release page to download the installation file for your OS, or download and extract the latest release automatically (Linux or macOS):
```
curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.10.0 TARGET_ARCH=x86_64 sh -
```
2. Move to the Istio package directory.

For example, if the package is istio-1.11.3: `cd istio-1.10.0`

3. Create a namespace istio-system for Istio components:
```
kubectl create namespace istio-system
```
4. Install the Istio base chart which contains cluster-wide resources used by the Istio control plane:
```
helm install istio-base manifests/charts/base -n istio-system
```
5. Install the Istio discovery chart which deploys the istiod control plane service:
```
helm install istiod manifests/charts/istio-control/istio-discovery \ -n istio-system
```
6. Install the Istio ingress gateway chart which contains the ingress gateway components:
```
helm install istio-ingress manifests/charts/gateways/istio-ingress \ -n istio-system
```
## Verifying the installation
Ensure all Kubernetes pods in istio-system namespace are deployed and have
a STATUS of Running:
`kubectl get pods -n istio-system`
## Installing the Gateway
Along with creating a service mesh, Istio allows you to manage gateways, which are Envoy proxies running at the edge of the mesh, providing fine-grained control over traffic entering and leaving the mesh.
#Unzip and Change Directory
```
unzip platform-istio-gateway-dev
cd platform-istio-gateway-dev
```
**#Cert Manager**
**Install cert-manager. Cert-manager will manage the certificates of gateway domains.**

**#Setup permissions**

**When running on GKE (Google Kubernetes Engine), you might encounter a ‘permission denied’ error when creating some of the required resources:**
```
kubectl create clusterrolebinding cluster-admin-binding \  --clusterrole=cluster-admin \ --user=$(gcloud config get-value core/account)  
```
**#Install Cert-manager**

`kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.3.1/cert-manager.yaml`

*#platform-istio-gateway*

* Istio Gateway configurations for DNS
* This gateway config file defines the base API endpoints of the micro services under DNS
* This repository also contains necessary files to setup SSL for DNS (Refer issuer.yaml and cert.yaml) using cert-manager
#### Create Gateway
*#Find the Gateway IP*
```
INGRESS_HOST=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.status.loadBalancer.ingress[0].ip)
```
**This will give you a LoadBalancer IP:**
`echo ${INGRESS_HOST}`

**#Create DNS**

Create a record (for eg) ([sample.example.com](*) and [keycloak.example.com](*)) using LoadBalancer IP

#### #Create a certificate

Issuers, and ClusterIssuers, are Kubernetes resources that represent certificate authorities (CAs) that are able to generate signed certificates by honoring certificate signing requests.
```
kubectl apply -f issuer.yaml 
kubectl get ClusterIssuer -n cert-manager# Should have Status as Ready 
```
A Certificate is a namespaced resource that references an Issuer or ClusterIssuer that determine what will be honoring the certificate request.
```
kubectl apply -f cert.yaml 
kubectl get Certificate -n istio-system # Should have Status as Ready 
```
#### #Create gateway with SSL
```
kubectl apply -f gateway-with-ssl.yaml` [No need to specify namespace]
```
#### #Apply Virtual Service

A VirtualService defines a set of traffic routing rules to apply when a host is addressed.
Each routing rule defines matching criteria for traffic of a specific protocol.
If the traffic is matched, then it is sent to a named destination service (or subset/version of it) defined in the registry.
```
kubectl apply -f backend-api/virtual-service.yaml # [No need to specify namespace] 
kubectl apply -f keycloak/virtual-service.yaml # [No need to specify namespace]
```

