# s3-glue-lambda-project

# Description
An AWS Lambda function is triggered when a file is uploaded to the input Amazon S3 bucket. This Lambda function then initiates an AWS Glue job, which processes the uploaded CSV file, converts it into JSON format, and stores the transformed file in a designated destination S3 bucket.

## Steps

1. login AWS
2. create s3 bucket: s3-input-file-ami & s3-destination-file-ami
3. create new Iam role for glue "aws-s3-glue-role" role :
     AmazonS3FullAccess
     AWSGlueConsoleFullAccess
     AWSGlueServiceRole
4. create new iam role for lambda function:
     AWSGlueServiceRole
     AWSLambdaBasicExecutionRole-bd61b20b-4b
5. create glue job
6. add source(csv) and target(json) in glue and attach iam role.
create lambda function and attach iam role and paste below code.
7. add trigger as s3 if "PUT" files(as soon as file is uploaded in s3, lambda should trigger)
8. upload a csv file in input s3 file for testing.
9. check glue console under "Runs". A new entry will be there .
9. a new  file will get created in another s3 destination bucket

```bash
import json
import boto3

glueClient = boto3.client('glue')

def lambda_handler(event, context):
    glueClient.start_job_run(JobName='csv-json-job')
    return "Job started"
```

## License

[MIT](https://choosealicense.com/licenses/mit/)
