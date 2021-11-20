## The types of data solutions that Accuknox provides includes


### Data Provenance for S3 in Container mounted environments 

This allows us to track and taint sensitive data in containerized environemnts as it flows through the network.

The data provenance system is able to answer questions like: 

- Which process [e.g., app] was used to create this data object [e.g., file]?
- When the process ran what were the other data object it wrote?
- What data objects did the process read?
- Could any data have flowed from this data object to that data object?
- What is the sensitivity of a given data flow or connection between processes?


### Data Protection and sensitive tracking for S3

A simpler version of the data protection and sensitive tracking for S3 enables us to track sensitive data and build audit logs at scale for S3 based sensitive data sources. 

This system is simply referred to as S3 Data Protection throughout Accuknox documentation.


### Data Protection and Governance for OLTP - MySQL / Postgres

This is a unified visibility based system which provides policy as code for enabling audit policies against MySQL and Postgres databases in K8s and Virtual machine environments.