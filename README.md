# AWS-Cloud-Logic
Import AWS S3 Excel file data into Dynamo db in AWS Cloud

Step 1 : CREATE IAM ROLE FOR various policy
a> S3FullAcess
b> dynamodbFUullAcess
C> LambdaBasicExecutionrole

Step 2 : Create S3 Bucket and Upload csv file into s3
  The Panes Name of my csv ile is :
  __________________________________
 | empid | name | Salary | parttime|
 |       |      |        |         |
 ___________________________________
