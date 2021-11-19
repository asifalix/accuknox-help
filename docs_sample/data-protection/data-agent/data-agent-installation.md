## Accuknox Data Agent DB configuration
AccuKnox Data Agent can scan more than 1 Database at a time. 

The database to be scanned is configured through a file located at conf/agent-db-config.yaml The following is an example of a agent-db-config.yaml:

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
      type: mysql
      key: asdlkm2lk3n-q23-asd-12-3
      host: localhost
      port: 5432
      user: test
      password: test

## Installation
Unzip AccuKnox Data Agent

Edit the conf/agent-db-config.yaml

Add the Workspace ID

Add the apiToken

The app.yaml and agent-db-config.yaml files must be present inside conf/ folder.

Run AccuKnox Data Agent
./ada