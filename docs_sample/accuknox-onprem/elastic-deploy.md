### Elastic Operator Deployment

#### 1.Please create a namespace of your choice. Example : elastic-logging
```sh
kubectl create ns elastic-logging
```

Note: Please use feeder-service namespace , if required.

#### 2. Clone the git repository
```sh
git clone -b dev https://github.com/accuknox/Accuknox-Logging
```
- Navigate into the directory that holds eck-operator folder.


#### 3.Helm Install
```sh
helm install eck-operator eck-operator/ -n <namespace>
```
- Navigate into the directory that holds elasticsearch folder.


#### 4.Helm Install
```sh
helm install elastisearch elasticsearch/ -n <namespace>
```
- Navigate into the directory that holds kibana folder.


#### 5.Helm Install
```sh
helm install kibana kibana/ -n <namespace>
```

#### 6. Beats Setup:
- The agent will be spinned along with Filebeat running along as a sidecar.
- The filebeat configuration file in the package can be updated to specific Elastic instances, and logs can be viewed in <b>Kibana</b>.

#### a. Elastic Configuration Parameters:
- The below Configuration parameters can be updated for elastic configuration.
> <i>(If Default params needs to be modified)</i>
```yaml
 - name: ELASTICSEARCH_HOST
        value: https://<svc-name>
 - name: ELASTICSEARCH_PORT
        value: "<svc-port>"
 - name: ELASTICSEARCH_USERNAME
        value: "elastic"
 - name: ELASTICSEARCH_PASSWORD
        value: "<elastic-password>"
```
To get elastic password
```sh
kubectl get secret elasticsearch-es-elastic-user -o go-template='{{.data.elastic | base64decode}}' -n namespace
```

#### b. Command to be Used:
```sh
kubectl set env deploy/feeder -n feeder-service ELASTICSEARCH_HOST=”https://elasticsearch-es-http”
```

#### c. Update Log Path:
- To Update the Log path configured, please modify the below log input path under file beat inputs.
```yaml
filebeat.inputs:
        - type: container
        paths:
        - /log_output/cilium.log
```

### 7. Kibana Dashboard
- Once the filebeat starts listening, an index will be created or updated on the elastic configured and the pushed logs can be seen.
- In order to create a dashboard, you will need to build visualizations. Kibana has two panels for this
  1. One called <b>Visualize</b> and
  2. Another called <b>Dashboard</b>
- In order to create your dashboard, you will first create every individual visualization with the Visualize panel and save them.


#### 8.Successful Installation
```sh
kubectl get all -n <namespace>
kubectl port-forward svc/kibana-kb-http 5601:5601
```
- All the pods should be up and running
- Kibana Ui with filebeat index should be seen (after beat installation)
