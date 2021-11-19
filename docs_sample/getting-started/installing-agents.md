# Installing Agents

We will need the following agents to get started.

## Shared Informer Agent


Installation Guide
******************

This agent authenticates with your cluster and collects information regarding entities like nodes,pods,namespaces

Command to create a namespace

```
kubectl create namespace <namespace-name>
```

Commands to create cluster role

```
kubectl create clusterrole <cluster-role-name> 
--verb=get,list,watch 
--resource=nodes,pods,namespace,services,endpoints
```

YAML to create service account

Note: Service Account Name and Namespace should be the same while creating role binding.

```

accuknox-sa.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: accuknox-agents
  namespace: accuknox-agents
secrets:
- name: accuknox-agent-secrets
```

Apply Yaml

```
kubectl apply -f <yaml-file-name> -n <namespace>
```

Create cluster role binding


```
kubectl create clusterrolebinding <cluster-rolebinding-name> 
--clusterrole=<cluster-role-name-used-above> 
--serviceaccount=<namespace>:<serviceaccountname>
```

Command for installing shared-informer-agent

```

kubectl apply -f https://github.com/accuknox/Onboarding-Agents-File/raw/master/sia-deploy.yaml -n <namespace-name>
```

Apply yaml file

```

kubectl apply -f <name-of-yaml-file>
```

## Cilium

Installation Guide 
***********

This agent is used to apply network policies

For managed environment (GKE):
*****

Command to Extract the Cluster CIDR to enable native-routing


```
NATIVE_CIDR=$(gcloud container clusters describe $CLUSTER_NAME --zone $CLUSTER_ZONE --format 'value(clusterIpv4Cidr)')
```
Setup Helm repository

```

helm repo add cilium https://helm.cilium.io/
```

Deploy Cilium release via Helm

```

helm install cilium cilium/cilium --version 1.9.8 \ 
--namespace kube-system \ 
--set nodeinit.enabled=true \ 
--set nodeinit.reconfigureKubelet=true \ 
--set nodeinit.removeCbrBridge=true \ 
--set cni.binPath=/home/kubernetes/bin \ 
--set gke.enabled=true \ 
--set ipam.mode=kubernetes \ 
--set nativeRoutingCIDR=$NATIVE_CIDR
```

## KubeArmor

Installation Guide
***********

Trains a model based on container workload type. It constantly monitors the syscalls happening inside the container. After training, if the vae sees syscalls happening in a way not seen in training phase, it will send high reconstruction error with detailed forensics information.

Deploy KubeArmor for GKE

```

kubectl apply -f https://raw.githubusercontent.com/kubearmor/KubeArmor/master/deployments/GKE/kubearmor.```

Deploy KubeArmor Host Policy

```

kubectl apply -f https://raw.githubusercontent.com/kubearmor/KubeArmor/master/pkg/KubeArmorHostPolicy/config/crd/bases/security.kubearmor.com_kubearmorhostpolicies.yaml
```

Deploy KubeArmor Policy

```

kubectl apply -f https://raw.githubusercontent.com/kubearmor/KubeArmor/master/pkg/KubeArmorPolicy/config/crd/bases/security.kubearmor.com_kubearmorpolicies.yaml ```

## Feeder Service

Installation Guide
******************

Feeder service deployment that collects feeds from Kubearmor and Cilium

Download the YAML file


```
wget https://raw.githubusercontent.com/accuknox/Onboarding-Agents-File/master/feeder-service.yaml
```

Copy paste the values into the above YAML File

Append the following code at the end of the YAML file

Note: Note: kindly maintain the indentation of the code.

 


          - name: KAFKA_BOOTSTRAP_SERVERS
            value: "34.133.201.60:9095"
          - name: KAFKA_PORT
            value: "9095"
          - name: HUBBLE_URL
            value: "hubble-relay.kube-system.svc.cluster.local"
          - name: HUBBLE_PORT
            value: "80"
          - name: KUBEARMOR_URL
            value: "kubearmor.kube-system.svc.cluster.local
          - name: KUBEARMOR_PORT
            value: "32767"
          - name: KAFKA_SSL_CA_LOCATION
            value: "/home/feeder-service/ca.pem"
          - name: KAFKA_SSL_KEYSTORE_LOCATION
            value: "/home/feeder-service/user.p12"
          - name: KAFKA_SSL_KEYSTORE_PASSWORD
            value: "REhtSHdOWXkyMkF0"

Apply the YAML file

 
```
kubectl apply -f <yaml file name> -n <namespace>
```

Set the env of Feeder Service

 
```
kubectl set env deploy/feeder -n feeder-service tenant_id=51 cluster_id=345

```
 
