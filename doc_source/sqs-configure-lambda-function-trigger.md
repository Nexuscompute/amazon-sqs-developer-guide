# Configuring a queue to trigger an AWS Lambda function \(console\)<a name="sqs-configure-lambda-function-trigger"></a>

You can use an AWS Lambda function to process messages in an Amazon SQS queue\. Lambda polls the queue and invokes your Lambda function synchronously with an event that contains queue messages\. You can specify another queue to act as a *dead\-letter queue* for messages that your Lambda function can't process\. 

A Lambda function can process items from multiple queues \(using one Lambda event source for each queue\)\. You can use the same queue with multiple Lambda functions\.

If you associate an encrypted queue with a Lambda function but Lambda doesn't poll for messages, add the `kms:Decrypt` permission to your Lambda execution role\.

Note the following restrictions:
+ Your queue and the Lambda function must be in the same AWS Region\.
+ An [encrypted queue](sqs-server-side-encryption.md) that uses the default key \(AWS managed KMS key for Amazon SQS\) cannot invoke a Lambda function in a different AWS account\.

For information about implementing the Lambda function, see [Using AWS Lambda with Amazon SQS](https://docs.aws.amazon.com/lambda/latest/dg/with-sqs.html) in the *AWS Lambda Developer Guide*\.

## Prerequisites<a name="configure-lambda-function-trigger-prerequisites"></a>

To configure Lambda function triggers, you must meet the following requirements:
+ If you use an IAM user, your Amazon SQS role must include the following permissions:
  + `lambda:CreateEventSourceMapping`
  + `lambda:ListEventSourceMappings`
  + `lambda:ListFunctions`
+ The Lambda execution role must include the following permissions:
  + `sqs:DeleteMessage`
  + `sqs:GetQueueAttributes`
  + `sqs:ReceiveMessage`
+ If you associate an encrypted queue with a Lambda function, add the `kms:Decrypt` permission to the Lambda execution role\.

For more information, see [Overview of managing access in Amazon SQS](sqs-overview-of-managing-access.md)\.

**To configure a queue to trigger a Lambda function \(console\)**

1. Open the Amazon SQS console at [https://console\.aws\.amazon\.com/sqs/](https://console.aws.amazon.com/sqs/)\.

1. In the navigation pane, choose **Queues**\.

1. On the **Queues** page, choose the queue to configure\. 

1. On the queue's page, choose the **Lambda triggers** tab\.

1. On the **Lambda triggers** page, choose a Lambda trigger\.

   If the list doesn't include the Lambda trigger that you need, choose **Configure Lambda function trigger**\. Enter the Amazon Resource Name \(ARN\) of the Lambda function or choose an existing resource\. Then choose **Save**\.

1. Choose **Save**\. The console saves the configuration and displays the **Details** page for the queue\.

   On the **Details** page, the **Lambda triggers** tab displays the Lambda function and its status\. It takes approximately 1 minute for the Lambda function to become associated with your queue\.

1. To verify the results of the configuration, [send a message to your queue](sqs-using-send-messages.md) and then view the triggered Lambda function in the Lambda console\.