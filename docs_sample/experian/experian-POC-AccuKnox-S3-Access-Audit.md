# AccuKnox S3 Access Audit
AccuKnox S3 Access Audit allows you to audit the access of the objects stored in an AWS S3 bucket.
With AccuKnox S3 Access Audit, users can understand what operation was performed on S3 objects, the status of the operation, who performed the operation and when the operation was performed on an S3 object.
## Assumptions
1. We assume that we have the following 5 AWS S3 buckets created:

    | S. No.  |  Data Bucket Name | Logs Bucket Name  |
    | :------------ |:---------------:| -----:|
    | 1. | ak-exp-poc-1-data | ak-exp-poc-1-logs |
    | 2. | ak-exp-poc-2-data | ak-exp-poc-2-data |
    | 3. | ak-exp-poc-3-data | ak-exp-poc-3-logs |
    | 4. | ak-exp-poc-4-data | ak-exp-poc-4-logs |
    | 5. | ak-exp-poc-5-data | ak-exp-poc-5-logs |
Data Buckets are the buckets where we store the actual data. Logs buckets are where the S3 Access logs are written to by AWS S3 Server. Upload some files in all those buckets.
Create data buckets: https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html
Configure log buckets: https://docs.aws.amazon.com/AmazonS3/latest/userguide/enable-server-access-logging.html

2. We also assume that the S3 buckets are not public and are not accessible outside the Experian's environment.

3. Upload multiple test files to each of the data buckets:
```
unzip experian-poc.zip 
cd experian-poc/setup
update <access_key>, <secret_key> and <region> in upload_files.sh
Run upload_files.sh for each buckets:
./upload_files.sh <bucket-name>

```
 | S. No.  |  Bucket Name |  Command  |
 | :------------ |:---------------:|:---------------:|
 | 1. | ak-exp-poc-1-data | `./upload_files.sh ak-exp-poc-1-data` |
 | 2. | ak-exp-poc-2-data | `./upload_files.sh ak-exp-poc-2-data` |
 | 3. | ak-exp-poc-3-data | `./upload_files.sh ak-exp-poc-3-data` |
 | 4. | ak-exp-poc-4-data | `./upload_files.sh ak-exp-poc-4-data` |
 | 5. | ak-exp-poc-5-data | `./upload_files.sh ak-exp-poc-5-data` |
    
## How To
In order to setup AccuKnox S3 Access Audit perform the following steps:

1. Visit [AccuKnox Platform](*)
2. Login using the email and password.
3. Select or create a new workspace
4. On the left navigation pane, select **Data Protection**
5. Next, select **Data Sources**
6. Click on the **Configure Data Source** button at the top right corner
7. Choose **No** for **Is the s3 bucket mounted inside a container workload?**
8. Choose **No** for **Is your S3 access log buckets accessible from outside your private network?**
9. In our scenario, we do not have S3 bucket objects accessible from outside the private network, hence click on **Done**.
10. Follow the steps [here](*) to install the **AccuKnox S3 Audit Reporter Agent**.
11. Once the agent has been configured and is running, it'll start syncing the objects in the data bucket with AccuKnox Platform.
12. Now, on the left navigation pane, under **Data Protection**, click on **Sensitive Source Labels**
13. Enter a value for **Label**.
14. Under **S3 BUCKET** on the left, select the bucket you want to configure sensitive sources from and select the objects that are sensitive on the right.
15. Click on **Next**.
16. We can skip the Configure Flagged Destination step.
17. Review the selection and click on **Create**

## Testing Scenarios
Until now, we have configured sensitive sources - the objects we think are sensitive. Now, use the AWS CLI to access the files in the data buckets as mentioned here - [POC Scenarios](*).
Then, at the AccuKnox Platform, on the left navigation pane, select S3 Access Logs. Now, you should be able to see the S3 access information.
| Heading |  Description |
| :------------ |:---------------:|
| BUCKET NAME | The name of the bucket that the request was processed against. |
| TIMESTAMP | The time at which the request was received |
| REQUESTER | The canonical user ID of the requester, or a - for unauthenticated requests. |
| KEY | The "key" part of the request, URL encoded, or "-" if the operation does not take a key parameter. In simple words, the object path. | 
| OPERATION | The operation that was performed in the current request. | 
| HTTP STATUS | The numeric HTTP status code of the response. |
