## Istio Resource Requirements

| Component Name      | Istio |
| ----------- | ----------- |
| No of Nodes      | 3       |
|  Machine Type  |   E2 / ec2 / vm (vmware / Cloud based VM)      |
| Image Type | Any Linux based OS with Container support ( EG: GCP COS-Containerd)  |
| CPU Per Node | 2 |
| Memory Per Node | 4 |
| Disk Size Per Node  | 50 |
| Total CPU | 6 |
| Total Memory | 12 |
| Total Disk Size | 150 |

## MySQL Resource Requirement

| Component Name      | MySQL |
| ----------- | ----------- |
| No of Nodes      | 3       |
|  Machine Type  |   E2 / ec2 / vm (vmware / Cloud based VM)      |
| Image Type | Any Linux based OS with Container support ( EG: GCP COS-Containerd)  |
| CPU Per Node | 16 |
| Memory Per Node | 20 |
| Disk Size Per Node  | 50 |
| Total CPU | 48 |
| Total Memory | 60 |
| Total Disk Size | 150 |
| Taints & Lables | mysql:true |
| Node Pool Name | db-mysql |

## Kafka Resource Requirement

| Component Name      | Kafka |
| ----------- | ----------- |
| No of Nodes      | 3       |
|  Machine Type  |   E2 / ec2 / vm (vmware / Cloud based VM)      |
| Image Type | Any Linux based OS with Container support ( EG: GCP COS-Containerd)  |
| CPU Per Node | 6 |
| Memory Per Node | 16 |
| Disk Size Per Node  | 50 |
| Total CPU | 18 |
| Total Memory | 48 |
| Total Disk Size | 150 |
| Taints & Lables | kafka:true |
| Node Pool Name | db-kafka |

## Pinot Resource Requirement

| Component Name      | Pinot |
| ----------- | ----------- |
| No of Nodes      | 6       |
|  Machine Type  |   E2 / ec2 / vm (vmware / Cloud based VM)      |
| Image Type | Any Linux based OS with Container support ( EG: GCP COS-Containerd)  |
| CPU Per Node | 6 |
| Memory Per Node | 20 |
| Disk Size Per Node  | 50 |
| Total CPU | 36 |
| Total Memory | 120 |
| Total Disk Size | 300 |
| Taints & Lables | pinot:true |
| Node Pool Name | db-pinot |