Object scanner scans for the database, tables in the database and columns in those tables.
The scanner then uploads the JSON to Accuknox Control Plane. Accuknox Control Plane pushes the message to a Kafka topic

## Installation Steps
Clone the following Accuknox Data Agent Repository 

Clone the repo using the following command,
git clone https://github.com/accuknox/accuknox-data-agent.git


### Open the terminal and navigate to,
cd accuknox-data-agent

### Configure Database details in agent-db-config.yaml(Path: conf/agent-db-config.yaml)
apiVersion: v1
type: agent-db-config
data: 
  workspace: 148
  apiToken: 
  databases:
    - version: V1
      type: mysql
      key: asdlkm2lk3n-q23-asd-12-3
      host: localhost
      port: 3306
      user: ada_test_user
      password: password
    - version: V1
      type: postgres
      key: asdlkm2lk3n-q23-asd-12-3
      host: localhost
      port: 5432
      user: test
      password: test

### To install packages and dependencies,
go mod download

### To run the Go program,
go run accuknox-data-agent