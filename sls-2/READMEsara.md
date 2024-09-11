# ce6-sara-serverless02

# Basic Commands:
### 1. sls deploy
Deploy your entire serverless application to the cloud.

    sls deploy

### 2. sls deploy function --function <functionName>
Deploy a single function instead of the entire stack.


    sls deploy function --function myFunction
### 3. sls invoke --function <functionName>
Invoke a deployed function manually.


   sls invoke --function myFunction
### 4. sls invoke local --function <functionName>
Invoke a function locally.

    sls invoke local --function myFunction
### 5. sls remove
Remove the entire serverless service from the cloud.

    sls remove
### 6. sls logs --function <functionName>
View logs for a specific function.

    sls logs --function myFunction
# Configuration-Related Commands:
### 1. sls info
Show information about the deployed service.

    sls info
### 2. sls config credentials --provider aws --key <key> --secret <secret>
Configure AWS credentials for Serverless Framework.

    sls config credentials --provider aws --key <yourKey> --secret <yourSecret>

These commands help manage serverless deployments efficiently.



### Serverless with lambda function

1. Create repository as public in GitHub
2. Clone the repository
3. GO to your code in VSCode
4. Run serverless and select your application as API
5. Run npm init
6. Update serverless.yml and include

```
 plugins: -serverless-offline
```

7. Run 

```
npm install serverless-offline
```

8. Test using 
```
serverless offline
```
9. Push updates to repo
10. Deploy lambda
```
sls deploy
```

11. Create new SQS on the console
12. Add that SQS as part of your event source for your lambda function
```
       - sqs:
          arn: arn:aws:sqs:region:XXXXXX:myQueue
          batchSize: 10
          maximumBatchingWindow: 60
          functionResponseType: ReportBatchItemFailures
```
Taken from URL, https://www.serverless.com/framework/docs/providers/aws/events/sqs

13. Deploy again
14. Commit all the code
