Check Pods Running status:

```sh
kubectl get pods -n accuknox-dev-kafka
```
![Alt](../images/kafka-pod.png)

Check Kafka Cluster status:
```sh
kubectl get kafka -n accuknox-dev-kafka
```
![Alt](../images/kafka.png)

Check Kafka Topics status:
```sh
kubectl get kafkaTopics -n accuknox-dev-kafka
```
![Alt](../images/kafka-topics.png)
