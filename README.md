# AWS-User-activity-monitoring-using-CloudTrail

**Overview:** 
In this project, We have some users in aws account. We created some access keys for that. This activity will be captured by cloudtrail. From the cloud trai, this event event is paased to event bridge. Using event bridge we can trigger a lambada function which will make an entry in dynomodb table like accesskey id, creation date,..

AWS CloudTrail is a service provided by AWS that one can use for operational and risk auditing, governance, and compliance of the AWS account.

**Step 1: 
Create a trail in CloudTrail**

Go to aws cloudtrail->click create trail->give storage location as new s3 bucket->disable kms encrytption->select management events->click create.

**Step 2: 
create function in lambda**

Go to lambda->click create function->select python->copy the attached code in this repo and paste it on lambda dashboard->click deploy

To access dynamodb, give permission for lamda
Click permission inside the lambda->click role->click add permissions->attach policy->give dynamodbfullaccess

**Step 3:
Create a table in Dynamodb**

Go to dynamodb->click create table->type cloudtrailkey in partion key option

**Step 4: 
Create rule in EventBridge**

Go to eventbridge->create rule-> make event bus as default->select IAM as aws service->click eventtype as aws api call via cloudtrail->slect eventtype specifications as specific operations and enter create access key inside the box(because bydefault whenever any api call happens, cloudtrail will send all events to eventbridge. From that we can filter create access key event)->select target as lambda function->click create rule

**Step 5:
To check working process**

Go to IAM->Click security credentials->create access key.

Now go to dynamodb table, one record is created.

So whenever iam access key is created cloudtrail pass event to eventbridge and eventbridge trigger the lambda function and make an entry in dynamodb table.
