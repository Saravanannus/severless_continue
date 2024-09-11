# ce6-sara-serverless02

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