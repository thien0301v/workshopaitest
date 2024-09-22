---
title : "Create Amazon Comprehend Classification training job"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 3.5 </b> "
---

Now that we have text extracted from our documents and have also labeled them, we will create the training data in order to train an Amazon Comprehend custom classification model . Our corpus has 100 samples of each document, so we should have about 300 rows of labeled data.

We will use Amazon Comprehend's Custom Classification to train our own model for classifying the documents. We use the `CreateDocumentClassifier` API to create a classifier which will train a custom model using the labeled data CSV file we created above. The training data contains extracted text, that was extracted using Amazon Textract, and then labeled. The following code cell uses `create_document_classifier` from **boto3 Python SDK** to initiate the model training process.

#### Create Amazon Comprehend custom classification Training Job
We will use Amazon Comprehend's Custom Classification to train our own model for classifying the documents. We will use Amazon Comprehend CreateDocumentClassifier API to create a classifier which will train a custom model using the labeled data CSV file we created above. The training data contains extracted text, that was extracted using Amazon Textract, and then labeled.
    ![s16](/images/3.clas/s16.png)




Note that you can also create a custom classifier using the **Amazon Comprehend** console manually. Refer to the documentation  to learn more how to create a custom classifier using the console. Continue with the remaining of the cells in this step. The custom classifier training could take upto ~30 mins.
    ![s17](/images/3.clas/s17.png)