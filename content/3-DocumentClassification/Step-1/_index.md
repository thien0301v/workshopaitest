---
title : "Setup notebook and upload sample documents to Amazon S3"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.2 </b> "
---


In this step we will install the required librarues, import the required modules, and initialize variables. We will also download the sample documents from our workshop repository and upload them to the SageMaker S3 bucket so we can process them. The ``curl`` command below downloads the ``classification-training.zip`` file which contains the data that will be required to train our custom Amazon Comprehend Classifier.

1. Run from Step 1 to 6
   ![run](/images/3.clas/run.png)

    ![down](/images/3.clas/download.png)
2. In the subsequenct code cells, we unzip and extract all the files from the zip file and subsequently upload them to an **Amazon S3** bucket. Complete executing all the code cells in this step.
   ![step7](/images/3.clas/step7.png)
   ![step8](/images/3.clas/step8.png)
   The data has been put into S3 and can be found in **AWS S3**.
   ![s3](/images/3.clas/s3.png)
or we can use the code in the file to extract the data
   ![s3](/images/3.clas/c2.png)