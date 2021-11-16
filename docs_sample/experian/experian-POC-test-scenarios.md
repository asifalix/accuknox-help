# S3 Data Protection Test Scenarios:
  **Note:** unzipped **experian-poc** directory contains test scripts that will access sensitive objects in s3 data buckets.
`
cd experian-poc
`
### Accessing AWS S3 Bucket - Access sensitive data with valid credentials
| S. No  | Test scripts | Expected Output |
| ------------- | ------------- | ------------- |
| 1. | `cd tests/valid_creds` `./access_ak-exp-poc-1-data_secret1.sh <access_key> <secret_key> <region> <bucket_name>` | User should see s3 access information for get-object operation of the sensitive data <secret1.txt> in s3 access logs page. HTTP status should be 200 |
|2. | `cd tests/valid_creds` `./access_ak-exp-poc-2-data_secret3.sh <access_key> <secret_key> <region> <bucket_name>` | User should see s3 access information for get-object operation of the sensitive data <secret3.txt> in s3 access logs page. HTTP status should be 200 | 
| 3. | `cd tests/valid_creds` `./access_ak-exp-poc-3-data_secret5.sh <access_key> <secret_key> <region> <bucket_name>` | User should see s3 access information for get-object operation of the sensitive data <secret5.txt> in s3 access logs page. HTTP status should be 200 |
| 4. | `cd tests/valid_creds` `./access_ak-exp-poc-4-data_secret4.sh <access_key> <secret_key> <region> <bucket_name>` | User should see s3 User should see s3 access information for get-object operation of the sensitive data <secret4.txt> in s3 access logs page. HTTP status should be 200 |
| 5. | `cd tests/valid_creds` `./access_ak-exp-poc-5-data_secret6.sh <access_key> <secret_key> <region> <bucket_name>` | User should see s3 access information for get-object operation of the sensitive data <secret6.txt> in s3 access logs page. HTTP status should be 200 |
### Accessing AWS S3 Bucket - Access sensitive data with invalid credentials
| S. No  | Test scripts | Expected Output |
| ------------- | ------------- | ------------- |
| 1. | `cd tests/invalid_creds` `access_ak-exp-poc-1-data_secret1_invalid_accessKey.sh <secret_key> <region> <bucket_name>` | User should see s3 access information for get-object operation of the sensitive data <secret1.txt> in s3 access logs page. HTTP status should be 403 |
| 2. | `cd tests/invalid_creds` `access_ak-exp-poc-2-data_secret3_invalid_accessKey.sh <secret_key> <region> <bucket_name>` | User should see s3 access information for get-object operation of the sensitive data <secret3.txt> in s3 access logs page. HTTP status should be 403 | 
| 3. | `cd tests/invalid_creds` `access_ak-exp-poc-3-data_secret5._invalid_secret.sh <access_key> <region> <bucket_name>` | User should see s3 access information for get-object operation of the sensitive data <secret5.txt> in s3 access logs page. HTTP status should be 403 |
| 4. | `cd tests/invalid_creds` `access_ak-exp-poc-4-data_secret4._invalid_secret.sh <access_key> <region> <bucket_name>` | User should see s3 User should see s3 access information for get-object operation of the sensitive data <secret4.txt> in s3 access logs page. HTTP status should be 403 | 
| 5. | `cd tests/invalid_creds` `access_ak-exp-poc-5-data_secret6._invalid_secret.sh <access_key> <region> <bucket_name>` | User should see s3 access information for get-object operation of the sensitive data <secret6.txt> in s3 access logs page. HTTP status should be 403 |
