---
title : "Document Review and Verification"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 6. </b> "
---
### Overview
**Amazon Augmented AI (Amazon A2I)** makes it easy to build the workflows required for human review of ML predictions. Amazon A2I brings human review to all developers, removing the undifferentiated heavy lifting associated with building human review systems or managing large numbers of human reviewers.

Amazon A2I provides built-in human review workflows for common machine learning use cases, such as content moderation and text extraction from documents, which allows predictions from Amazon Rekognition and Amazon Textract to be reviewed easily. You can also create your own workflows for ML models built on Amazon SageMaker or any other tools. Using Amazon A2I, you can allow human reviewers to step in when a model is unable to make a high confidence prediction or to audit its predictions on an on-going basis.

### Resource required for A2I
To incorporate Amazon A2I into your human review workflows, you need three resources. Expand the following sections to learn more about each of the resources.
#### Worker task template
A **worker task template** to create a worker UI. The worker UI displays your input data, such as documents or images, and instructions to workers. It also provides interactive tools that the worker uses to complete your tasks.
#### Human review workflow
A **human review workflow**, also referred to as a flow definition. You use the flow definition to configure your human workforce and provide information about how to accomplish the human review task. For built-in task types, you also use the flow definition to identify the conditions under which a review human loop is triggered. For example, with Amazon Textract can analyze text in a document using machine learning. You can use the flow definition to specify that a document will be sent to a human for content moderation review if Amazon Textracts's confidence score output is low for any or all pieces of text returned by Textract. You can create a flow definition in the Amazon Augmented AI console or with the Amazon A2I APIs.
#### Human loop
A **human loop** to start your human review workflow. When you use one of the built-in task types, the corresponding AWS service creates and starts a human loop on your behalf when the conditions specified in your flow definition are met or for each object if no conditions were specified. When a human loop is triggered, human review tasks are sent to the workers as specified in the flow definition.

When using a custom task type, you start a human loop using the Amazon Augmented AI Runtime API. When you call StartHumanLoop in your custom application, a task is sent to human reviewers.

