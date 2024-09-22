---
title : "Getting Started"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---

In the first notebook, we will upload these bank statements, invoices, and receipts into an Amazon S3 bucket, use Amazon Textract to extract the raw text from the documents, label the data appropriately, and then train an Amazon Comprehend custom classifier with the labeled data.

1. Open the first notebook titled ``01-idp-prep-document-classification.ipynb``. You'll be prompted to select an image and kernel. Select the options as shown in the image below and click **Select** .
   ![envir](/images/3.clas/envir.png)
The notebook should autmatically attach to an **ml.t3.medium** instance (with 2vCPU and 4GiB memory). If it is not, click on the **"Switch instance type"** and select ml.t3.medium from the list of instance.

>⚠️ ``ml.t3.medium`` is the preferred instance type. Please DO NOT select any other instance type as it may cause the account to incur unexpected charges.
