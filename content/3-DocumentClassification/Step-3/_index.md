---
title : "Prepare a CSV training dataset for Amazon Comprehend custom classifier training"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3.4 </b> "
---

In this step, the extracted data is written into a CSV file and uploaded to S3. This file will be used as training data for next step. We will be training an Amazon Comprehend custom classifier in Multi-class mode using a CSV file. Take a look at the documentation for preparing data for a [Multi-class](https://docs.aws.amazon.com/comprehend/latest/dg/prep-classifier-data-multi-class.html) mode  model training. The CSV files are UTF-8 encoded plaintext files and should be of format.

```
CLASS,Text of document 1
CLASS,Text of document 2
CLASS,Text of document 3
```
Complete executing the code cells in this section to prepare the CSV file and upload it to S3. At the end of this step we will have our training data in CSV format in a file named `comprehend_train_data.csv` with classes `bank-statements`, `invoices` and `receipts`.

Now that we have text extracted from our documents and have also labeled them, we will create the training data in order to train an Amazon Comprehend custom classification model. Let's take a look at the labeled data. We have 100 sample of each document, so we should have about 300 rows of labeled data.
    ![s13](/images/3.clas/s13.png)

We will create a training dataset from extracted text and upload it to Amazon S3. The training data file will be written in CSV format and will be named comprehend_train_data.csv. Note that you can have more than one CSV file in an S3 bucket for training a Comprehend custom classifier. If you have more than one file, you can specify only the bucket/prefix in call to train the custom classifier. Amazon Comprehend will automatically use all the files under the bucket/prefix for training purposes.

The following code cells will upload the training data to the S3 bucket, and create a Custom Comprehend Classifier. You can also create a custom classifier manually, please see the subsequent sections for instructions on how to do that.
    ![s14](/images/3.clas/s14.png)

Complete executing the code cells in this section to prepare the CSV file and upload it to S3. At the end of this step we will have our training data in CSV format in a file named comprehend_train_data.csv with classes bank-statements, invoices and receipts.
    ![s15](/images/3.clas/s15.png)