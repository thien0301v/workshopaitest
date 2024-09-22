---
title : "Extract text from sample documents using Amazon Textract"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.3 </b> "
---

In this section we use **Amazon Textract's** ``detect_document_text`` API to extract the raw text information for all the documents in S3. We will also label the data according to the document type. This labeled data will be used to train a custom Amazon Comprehend classifier. We define a utility function that uses the ``textract_extract_text`` API to extract text from a document and find which category (or directory in **S3**) it belongs to and then label the data and return an array [``<label>``, ``<document_text>``].
    ![s2](/images/3.clas/s2.png)

Execute all the code cells in this step to prepare labeled data for **Comprehend** classifier training. At the end of this step, we should have a collection `labeled_collection` ready with labeled data required for **Amazon Comprehend** classification. Note that a large assumption here is that we already have a lebeled set of historic documents to be able to train a custom classification model.
    ![train](/images/3.clas/train.png)

