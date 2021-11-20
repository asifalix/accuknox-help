# Pinot Deployment
**Note**
1. Do not change the namespace name.
If changes to the namespace are made, then you will need to change the service name & if the service name is changed, you will to need to change the microservice configmap files. (eg) app.yaml.
2. Please create a node pool on EKS / GKE / AKS (or) on-premise worker nodes with below Taints and Labels:
```
Taints - pinot:true
Labels -pinot:true
```
### Steps
1. untar pinot deployment files
```
untar accuknox-pinot-dev.tar.xz
```
2. Create Namespace
```
kubectl create namespace accuknox-dev-pinot
```
3. Set context
```
kubectl config set-context --current --namespace=accuknox-dev-pinot
```
4. Install Helm pkg
```
helm install accuknox-dev-pinot accuknox-pinot-dev/
```
5. Check the pods deployment
```
kubectl get pods -n accuknox-dev-pinot
```
![pinot deployment](https://user-images.githubusercontent.com/88204255/141975518-7eb29eb2-a89a-4ce4-b005-3c6a92834c82.png)
