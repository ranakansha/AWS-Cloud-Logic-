# Import AWS S3 Excel file data into Dynamo db in AWS Cloud

Step 1 : CREATE IAM ROLE FOR various policy
--------------------------------------------------
```
a> S3FullAcess
b> dynamodbFUullAcess
C> LambdaBasicExecutionrole

```
Step 2 : Create S3 Bucket and Upload csv file into s3
  The Panes Name of my csv ile is :
  ```
----------------------------------------
  empid |name  |salary  | parttime
----------------------------------------
```
Step3 : Create dynamodb table where Empid is primary key
My table name is Testseries

Step4 : Create lambda function

[a> go lambd function services and create lambda function from scratch and the language is python ]
[b> choose existing role that we are created in step1]
[c> write the lambda logic that are mention below]
```
import boto3
s3_client = boto3.client('s3')
#dynamo_client = boto3.client('dynamodb')
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('testseries')

def lambda_handler(event, context):
    bucket_name = event['Records'][0]['s3']['bucket']['name']
    filename = event['Records'][0]['s3']['object']['key']
    resp=s3_client.get_object(Bucket=bucket_name,Key=filename)
    data = resp['Body'].read().decode("utf-8")
    employees = data.split("\n")
    for emp in employees :
        print(emp)
        employee_data = emp.split(",")
        try:
            table.put_item(
            Item={
                "empid":employee_data[0],
                "name" :employee_data[1],
                "salary":employee_data[2],
                "parttime":employee_data[3]
            }
            )
    
        except Exception as e:
            print("end of the file")
```
Step5 : save lambda function and test it.
step6 : reload your table coontent load in your db table.
