---
title : "Create Amazon Comprehend real-time endpoint (optional)"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 3.7 </b> "
---

To use the Amazon Comprehend custom classifier model we need to create a real-time endpoint. Real time endpoints can either be created programmatically using Comprehend's Boto3 client  or manually via the console. To learn how to create a real-time endpoint using console refer to the documentation. We use the CreateEndpoint API via Boto3 `comprehend.create_endpoint()` method to create the real-time endpoint.

Once our Comprehend custom classifier is fully trained (i.e. status = TRAINED). We can create a real-time endpoint. We will use this endpoint to classify documents in real time. The following code cells use the comprehend Boto3 client to create an endpoint, but you can also create one manually via the console. Instructions on how to do that can be found in the subsequent section.
    ![s27](/images/3.clas/s27.png)


It may take ~15 minutes for the endpoint to get created. Once the end-point is created successfully, you can begin classifying documents (these are our unknown set of documents) under the `/samples/mixedbag` directory. Recall that our goal is to classify these unknown documents into bank statements, invoices and receipts respectively.
    ![s28](/images/3.clas/s28.png)

