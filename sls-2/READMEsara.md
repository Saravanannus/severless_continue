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

## My Serverless Framework (SLS) configuration describing each line in detail:

### Line-by-Line Breakdown:

#### 1. functions:

- This keyword defines the functions in your Serverless service. Each function is a piece of code that can be triggered by events like HTTP requests, SQS messages, or other AWS services.

#### 2. hello:

This is the name of the function within your service. The function name (hello) can be anything you choose and will be referenced in deployment and logs.

#### 3. handler: handler.hello

- handler: specifies the path to the function code.
- handler.hello means the function is located in the handler.js file, and the function's name is hello.
For example, in your handler.js file, there would be a function like this:
javascript

module.exports.hello = async (event) => {
  // function code here
};

#### 4. events:

- This defines the triggers or events that invoke the function. You can attach multiple events to a single function. In this example, the function hello is triggered by two events: HTTP API and SQS (Simple Queue Service).

## Event 1: HTTP API

#### 5.  -httpApi:

- This defines an HTTP API event that will trigger the function when an HTTP request is made.

#### 6. path: /

- This defines the URL path for the API endpoint that will trigger the function. The / path means that the function will be invoked when someone accesses the root URL (e.g., https://your-api-url.com/).

#### 7. method: get

- This specifies the HTTP method (GET, POST, etc.) that will trigger the function. In this case, the function will be invoked when a GET request is made to the / path.

# Event 2: SQS

#### 8. -sqs:

- This defines an SQS event that will trigger the function when a message is placed into an Amazon Simple Queue Service (SQS) queue. The SQS event allows the function to consume messages from the queue.

#### 9. arn: arn:aws:sqs:ap-southeast-1:255945442255:sara

- arn: specifies the Amazon Resource Name (ARN) of the SQS queue. The ARN uniquely identifies the queue (sara) located in the AWS region ap-southeast-1 with the account ID 255945442255.

#### 10. batchSize: 10

This defines the number of messages that AWS Lambda will pull from the SQS queue in one batch. In this case, it will retrieve up to 10 messages at a time to process in a single function invocation. This helps optimize performance by processing multiple messages in a batch.

#### 11. maximumBatchingWindow: 60

- This defines the maximum amount of time (in seconds) Lambda will wait before invoking the function with a batch of messages. If fewer than 10 messages are available in the queue, Lambda will wait for up to 60 seconds before triggering the function. This allows batching when messages arrive slowly.

#### 12. functionResponseType: ReportBatchItemFailures

- This specifies how the function should handle message processing failures. When set to ReportBatchItemFailures, the function will report which messages failed to be processed in the batch, and SQS will only retry those failed messages, rather than the entire batch. This helps improve efficiency when handling large message queues.

### Summary:

- The hello function is defined in the handler.js file and can be triggered by both HTTP GET requests at the root path (/) and messages in the SQS queue.

- The SQS configuration allows the function to process up to 10 messages at a time with a maximum wait time of 60 seconds before it invokes the function. If any messages in the batch fail to process, only those will be retried.