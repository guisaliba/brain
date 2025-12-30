## What is Lambda?
AWS Lambda is a piece of code that runs **serverless**.
this can also be interpreted as "code that runs on a server that you don't have to buy or manage". you can run whatever you define as your code e.g.: a Python script, a JS function running on Node, etc.

Lambda works with events. that means, the piece of code you defined as your Lambda function will be executed or ran in response to an event. this could be a file being uploaded to an S3 bucket, a change in a DynamoDB table, etc.

it allows developers to manage pieces of functionalities that otherwise would have to live in a dedicated server, or inside a container with several additional costs. Lambda solves that problem while allowing scaling with ease.

if your function is executed at its peak e.g. 100 times a day, you don't pay for 100 executions all the time, for every day in the month. you pay per execution, meaning that if the average executions of your Lambda is e.g. 5 times a day you'll likely pay for those and in a busy day, for the 100 invokes.

## Really serverless?
 even though calling it serverless, doesn't mean it's not running  in a server. so how does AWS manages to execute your own Lambdas at the exact time they should be executed? are they listening to all the Lambdas all the time?

the answer is no. Lambdas are shipped with something called **cold start**. it means that when an event asks to execute your function (in other words, triggers), AWS will take 100ms - 1s (which is extremely fast) to run your code.

after that cold execution, any other subsequent executions in a window of time will be run almost instantly, around 100ms. it's kind of of waking up your code, warming it up, and then running it. this way AWS doesn't need to keep your code up to run all the time.

talking about code, a Lambda function is basically a function declared as a **handler** (or Lambda handler). this function has two parameters: **event** and **context**. whenever it gets invoked, the Lambda runtime will pass these two down to the handler.

an event is a JSON with data for the function to process while context is a bunch of information about the runtime environment, invocation, etc.

## Deploying it
when the code of your handler is done, you have to deploy it to AWS along with its trigger. the trigger can be configured through the Lambda console panel, the same place where you would define your code in the console's own code editor.

as aforementioned, the event could be an S3 bucket file upload, so in the trigger configuration you can choose it to be from S3, choose the bucket and what events on that bucket should the trigger be listening to.
e.g.: file upload, file deletion, copy, restore from Glacier initiated, etc.

from the console, the S3 bucket (or any other event source) would automatically has its permission configured to allow it invoking a Lambda function (`lambda:InvokeFunction`). otherwise, you have to give the event source this permission or it won't work.

**note**: the Lambda function and the event source MUST be in the same region.
e.g.: if the trigger is a change to a Dynamo table, both the table and Lambda must be in the same region.

## Best scenarios for using Lambdas
Lambda thrives in **event-driven architecture**, where the flow of an application is dictated by events rather than a central controller. Typical triggers include:
- **API Gateway** for web APIs.
- **S3 Events** like file uploads.
- **DynamoDB Streams** for database changes.
- **SQS (Simple Queue Service)** or **SNS (Simple Notification Service)** for messaging and queueing systems.

Example:
- A user uploads a file to an S3 bucket (event).
- This triggers a Lambda function that processes the file (e.g., image resizing, video encoding, or data parsing).
- The function completes, and the processed file is saved, or the result is forwarded to another service.

### When to Use AWS Lambda:
- **Short, event-driven tasks**: Ideal for processing events like file uploads, database changes, and API requests.
- **Scalable microservices**: Lambda is perfect for building small, modular microservices that handle specific tasks within larger applications.
- **Automation**: Use Lambda to automate tasks like cleaning up unused resources, responding to system health changes, or periodically fetching data from an API.
- **Pay-as-you-go**: If you only need to run code occasionally, Lambda is cost-effective because you only pay when the function is actually running.

### Containers, VMs, and Lambda
Lambda abstracts away the infrastructure, but understanding how [[containers]] and VMs (read more on [[containers-vs-virtual-machines]]) relate helps clarify how Lambda operates behind the scenes.
- **VMs**: Lambda doesn’t involve you in VM management. AWS handles the allocation of VMs behind the scenes, ensuring that your Lambda function runs in a secure and isolated environment, but you don't need to think about VMs at all.
- **Containers**: Lambda functions run inside lightweight **containers** to ensure portability and isolation. However, **AWS manages these containers for you**. While you don't explicitly manage the containers in Lambda, you can build your Lambda functions as **container images** if needed, giving you more control over your runtime environment.