## AccuKnox Data Agent for MySQL
Accuknox Data Agent scans for the database, tables in the database and columns in those tables and exports them to AccuKnox SaaS for data classification and labelling.

## Hardware Requirements
- RAM - 1 GB (Minumum)
- Storage 512 MB (Minimum)

## System Requirements
AccuKnox Data Agent runs on a Linux host and can be run on Linux based OSes such as Ubuntu 18.04+, Debian 8+, CentOS 7+, Fedora and RHEL.

## Software Requirements
In order to use Accuknox Data Agent, a working MySQL server 5.6+ that it can connect to is all that is required. 

## Network Requirements
AccuKnox Data Agent requires port number 443 to be open for egress. This port will be used to communicate with the AccuKnox Control Plane.

## Permissions required by Accuknox Data Agent on MySQL.
AccuKnox Data Agent requires a MySQL user and password with read-only permission to the information_schema table.

### MySQL 5.7+
```
CREATE USER 'ada_user'@'<host>' IDENTIFIED BY '<password>';
GRANT SELECT ON information_schema.* TO '<host>'@'<password>';
FLUSH PRIVILEGES;
```

