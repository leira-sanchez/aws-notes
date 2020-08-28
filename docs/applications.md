# Applications

## SQS 
A web service that gives you access to a message queue that can be used to store messages while waiting for a computer to process them. 

* It's a distributed queue system that enables web service applciations to quickly and reliably queue messages that one component in the application generates to be consumed by another component.

* A queue is a temporary repository for messages that are awaiting processing.

* **Decouple** the components of an application so they run independently, easing message manageent between components.

* Pull-based. An EC2 instance pulling the messages out of the queue.

* Messages are <= 256 KB.

* Messages can be kept in the queue from 1 minute to 14 days; the default retention period is 4 days.

* **Visibility time out** - the amount of time that the message is invisible in the SQS queue after a reader picks up that message. If the job is processed before the visibility timeout expires, teh message is deleted from the queue. If not, the message will become visible again and another reader will process it which could result in the same message being delivered twice.
    * Max: 12 hours

* **Long polling** - retrieve messages from your queues.Short polling returns imeediately if if the queue is empty. Long polling doesn't return a response until a message arrives in the message queue or the long poll times out. Cheaper.

* You need to impolement your own application-level tracking, especially if your application uses multiple queues.

* Messages in SQS queue are not encrypted by default.

* Messages in the queue will continue to exist even after the EC2 instance has processed it, until you delete that message.

1. **Standard Queues** - nearly unlimited number of transactions per second. Guarantees that a message is delivered at least once. **Might send the message more than once and possibly out of order.**

1. **FIFO Queue** - first-in-first-out delivery and exactly-once processing: the order in which messages are sent and received is strictly preserved and a message is delivered once and remains available until a consumer processes and deletes it. Duplicates are not introduced into the queue.
    * Support message groups that allow multiple ordered message groups withihn a single queue.

    * Limited to 300 transactions per second (TPS) but have all the capabilities of standard queues.

[Cheat Sheet](https://tutorialsdojo.com/aws-cheat-sheet-amazon-sqs/)

## SWF
Simple Work Flow Service - enables applications for a range of use cases, including media processing, web application back-ends, business process workflows, and analytics pipelines, to be designed as a coordination of tasks. Makes it easy to coordinate work across distributed application components.

* Tasks - invocations of various processing steps in an application which can be performed by execturable code, web service calls, human actions, and scripts.

* Workflow executions retention period can be up to 1 year.

* Tasks are never duplicated.

* Keeps track of all the tasks and events in an application.

* Workflow Actors - an application that can initiate a workflow. 

* Deciders - control the flow of activity tasks in a workflow exection. A decider decides what to do next.

* Activity workers - carry out the activity tasks.

## SNS
Simple Notification Service - web service to send notifications from the cloud.

* Profies a highly scalable, flexible, and cost-effective capability to publish messages from an application and immediately deliver them to subscribers or other applications.

* Push notifications

* SMS text messages or email to SQS or any HTTP endpoint

* Allows you to group multiple recipients using topics.
    * Topic - an access point for allowing recipients to dynamically subscribe for identical copies of the same notification

* Messages published to SNS are stored redundantly across multiple availability zones

* Benefits
    * Instantaneous, push-based delivery (no polling)

    * Simple APIs and easy integration with applications

    * Flexible message delivery over multiple transport protocols

    * Inexpensive, pay-as-you-go

    * Console offers point-and-click interface

## Elastic Transcoder
* Media transcoder in the cloud

* Converts media files from their original source format into formats that will play on the screen

* Provides transcoding presets for popular output formats

* Pay based on the minutes that you transcode and the resolution at which you transcode

## API Gateway
Fully managed service that makes it easy for developers to publish, maintain, monitor, and secure APIs at any scale.

### What Can API Gateway Do?
* Expose HTTPS endpoints to define a RESTful API

* Serverless-ly connect to services like Lambda & DynamoDB

* Send each API endpoint to a different target

* Run efficiently with lo cost

* Scale effortlessly (automatically)

* Track and control usage by API key

* Throttle requests to prevent attacks

* Connect to CloudWatch to log all requests for monitoring

* You can enable API caching to cache your endpoint's response. This way, you can reduce the number of calls made to your endpoint and also improve the latency of the requests to your api.

* Enabling caching for a stage, API Gateway caches responses from your endpoint for a specified time-to-live (TTL) period, in seconds. Then, responds to the request by looking up the endpoint response from the cache instead of making a request to your endpoint.

* Enable CORS on API Gateway 

### Configure API Gateway
1. Define an API (container)

1. Define Resources and nested Resources (URL paths)

1. For each Resource:
    * Select supported HTTP methods

    * Set security

    * Choose target (EC2, Lambda, DynamoDB, etc.)

    * Set request and response transformations

### Deploy API Gateway
1. Deploy API to a stage
    * Uses API Gateway domain by default

    * Can use custom domain

    * Now supports AWS Certificate Manager: free SSL/TLS certs

## Kinesis
A platform to send your streaming data to. 

* **Streaming Data** - data that is generated continuously by thousands of data sources, which typically send in the data records simultaneously, and in small sizes (KBs).

### Types

1. **Kinesis Streams** - a place to store data.
    * By default, stores data 24h but it is possible to store it for up to 7 days

    * Data is stored in shards

1. **Kinesis Firehose**
    * Doesn't have data persistance. You must do something with that data as soon as it gets to Firehose

1. **Kinesis Analytics** - works with Kinesis Streams and Kinesis Firehose to analyze the data on the fly on either service. Stores the data on S3, Redshift, or Elasticsearch Cluster

[Cheat Sheet](https://tutorialsdojo.com/aws-cheat-sheet-amazon-kinesis/)

## Web Identity Federation && Cognito
* **Web Identity Federation** - lets you give your users access to AWS resources after they have successfully authenticated with a web-based identity provider like Amazon, Facebook, or Google. The user receives an authentication code from the Web ID provider, which they can trade for temporary AWS security credentials.

* **Cognito** - Amazon's Web Identity Federation Service (Identity Broker).
    * Sign-up and sign-in to your apps

    * Access for guest users

    * Acts as an Identity Broker between your application and Web ID proviers, so you don't need to write any additional code

    * Synchronizes user data for multiple devices

    * Recommended for all mobile applications AWS services

    * Tracks the association between user identity and the various different devices they sign-in from 

    * Uses Push Synchronization to push updates and synchronize user data across multiple devices

    * Uses SNS to send a notification to all the devices associated with a given user identity whenever data stored in the cloud changes

    * **User Pools** - directories used to manage sign-up and sign-in functionality for mobile and web applications. Users can sign-in directly to the User Pool or through social media. Successful authentication generates a JSON Web Token

    * **Identity pool** - authorise access to your AWS resource

    ## Elasticsearch Service
    [Cheat Sheet](https://tutorialsdojo.com/aws-cheat-sheet-amazon-elasticsearch-amazon-es/)