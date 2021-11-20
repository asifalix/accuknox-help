

### Enterprise Data Challenges

With the adoption of the cloud (private and public) enterprise data is being spread out into multiple places and stored in multiple technologies. As a result, enterprises are quickly being inundated with uncertainties of who has access to what data. To compound the matters, the aggressive postures taken by regulatory bodies such as GDPR, CCPA, HIPAA, HITRUST etc. are making it impossible to be certain about the access compliance of the data. 

The below diagram shows different dimensions of complexity aspects of enterprise data.



<img src="/assets/images/data-protection.png" />

GIven the complexity of data explosion, enterprises are unable to answer some fundamental questions related to their data and its security. 

- I do not know an exhaustive list of all the ways my data is stored.
- I do not know which user, which process, which application has access to what data. 
- I do not have a way to apply the same access restrictions to the same data no matter which environment it is at any point in time.
- I do not know which data is sensitive and which data is not sensitive. (sensitive data would be more than CC or SSN, even name, email are considered PII)
- I do not know all the places where data exists for a specific user, transaction or object. 
- While the access to the data from the application layer is protected, it is unclear about the access from system level, non-application centric data (backup, data warehouse, ML data etc.) 

### How it works?
Discovery - In this part of the product, given a data source location (AWS, Azure, GCP, Network File System, Box, DropBox) or a Kubernates cluster,  the system will identify all the data sources available - regardless of “How it is stored” (RDBMS, File, non-RDBMS etc.) 

Classification and Labelling Label - In this part of the product, for all the discovered data, the system will try to identify the sensitive data. The system will also label the data based on different sensitivity aspects of the data under different labels. A user will be allowed to confirm, override or delete the labels. 

Audit and Enforcement: In this part of the product, the system will monitor the access to the discovered and labeled data sources, and report/alert any exception to the policy specified for the data. In cases where technically possible, the system will prevent the access to the data in question. In addition to the functional aspect of the product, the system will have administrative capabilities to - 

Collect the access to the data source location and establish the connection. 

Create policies that specify which data labels are allowed access to by which identities

Reporting to view and set up alerting mechanisms for policy exceptions
