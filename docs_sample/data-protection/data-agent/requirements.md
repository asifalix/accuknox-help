
## What is Accuknox Data Agent
Accuknox Data Agent scans for the database, tables in the database and columns in those tables.
The Accuknox Data Agent uploads the data to Accuknox Control Plane. Accuknox Control Plane pushes the message to a Kafka topic

## How Accuknox Data Agent work with MySQL
Accuknox Data Agent get MySQL connection(user, host, port, password) related details from conf/agent-db-config.yaml. Then ADA get Mysql instance and get All DB, Tables and Columns details.

## Permissions required by ADA on MySQL DBs.
Which user created and configured in conf/agent-db-config. Give grant all permission to that user. Then only Accuknox Data Agent get DB instance and DB details. 

CREATE USER 'ada_test_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL ON *.* TO 'ada_test_user'@'localhost';

## Accuknox Data Agent DB configuration
AccuKnox Data Agent can scan more than 1 DataBase at a time. 

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

Configure the agent db config to be monitored

Add the workspace

Add the apiToken

The app.yaml and agent-db-config.yaml files must be present inside conf/ folder.

Run AccuKnox Data Agent