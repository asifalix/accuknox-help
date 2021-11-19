
## What is Accuknox Data Agent
Accuknox Data Agent scans for the database, tables in the database and columns in those tables.
The Accuknox Data Agent uploads the data to Accuknox Control Plane. Accuknox Control Plane pushes the message to a Kafka topic

## How Accuknox Data Agent work with MySQL
Accuknox Data Agent get MySQL connection(user, host, port, password) related details from conf/agent-db-config.yaml. Then ADA get Mysql instance and get All DB, Tables and Columns details.

## Permissions required by ADA on MySQL DBs.
Which user created and configured in conf/agent-db-config. Give grant all permission to that user. Then only Accuknox Data Agent get DB instance and DB details. 

CREATE USER 'ada_user'@'localhost' IDENTIFIED BY 'ada@123';
GRANT ALL ON *.* TO 'ada_user'@'localhost';

## Software Requirements
AccuKnox Data Agent supports Linux and can be run on most major Linux based OSes such as Ubuntu 18.04+, Debian 8+, CentOS 7+, Fedora and RHEL.

## Network Requirements
AccuKnox Data Agent requires port number 443 to be open for egress. This port will be used to fetch Mysql meta data and to push metrics to AccuKnox Control Plane.