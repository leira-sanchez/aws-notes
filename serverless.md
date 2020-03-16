# Serverless

## Lambda
* A compute service where you can upload your code and create a Lambda function. 

* Takes care of provisioning and managing the servers that you use to run the code. 

* You don't have to worry about operating systems, patching, scaling, etc.

* Environment variables are encrypted using the AWS KMS. When the Lambda function is invoked, they are decrypted and made available to the Lambda code. 

* Encryption helpers - 

[Cheat Sheet](https://tutorialsdojo.com/aws-cheat-sheet-aws-lambda/)

## Lambda@Edge
Lets you run Lambda functions to customize the content that CloudFront delivers, executing the functions in AWS locations closer to the viewer. The functions run in response to CloudFront events, without provisioning or managing servers. You can use lambda functions to change CloudFront requests and responses at the following points:
* Viewer request

* Origin Request

* Origin response

* Viewer response