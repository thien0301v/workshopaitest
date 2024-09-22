---
title : "Classify documents with Amazon Comprehend custom classifier"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 3.6 </b> "
---

In this step we will use Amazon Comprehend custom classification model to classify sample documents. We will use `start_document_classification_job` API to launch an asynchronous job to classify the documents. This API supports documents in their native format (PDF/PNG/JPG/TIF) and can use Amazon Textract behind the scenes to read the text from the documents and subsequently determine the document class.Let's start by uploading our sample documents to the S3 bucket
    ![s18](/images/3.clas/s18.png)
Amazon Comprehend Async classification works with PDF, PNG, JPEG, as well as UTF-8 encoded plaintext files. Since our sample documents under the samples directory are of PNG format, we will specify a DocumentReadAction and use Amazon Textract with the `TEXTRACT_DETECT_DOCUMENT_TEXT` option. This will tell Amazon Comprehend to use Amazon Textract DetectDocumentText API behind the scenes to extract the text and then perform classification. For InputFormat, we will use `ONE_DOC_PER_FILE` mode which signifies that each file is a single document (the other mode is `ONE_DOC_PER_LINE` which means every line in the plaintext file is a document, this is best suited for small documents such as product reviews or customer service chat transcripts etc.)
    ![s20](/images/3.clas/s20.png)

### Check status of the classification job
The code block below will check the status of the classification job. If the job completes then it will download the output predictions. The output is a zip file which will contain the inference result for each of the documents being classified. The zip will also contain the output of the Textract operation performed by Amazon Comprehend.
    ![s21](/images/3.clas/s21.png)
    ![s22](/images/3.clas/s22.png)

Continue run next code
    ![s23](/images/3.clas/s23.png)


Let's take a look at the **Amazon Comprehend** classification output. We have collected the output for all the files in a documents variable. The script above will download and un-zip the zip file locally, so you can navigate into the classification-output directory from the file browser panel on the left and inspect the files manually.
    ![s24](/images/3.clas/s24.png)
Our documents under the samples/mixedbag folder has now been classified. We will upload them into S3 with proper prefix label.
    ![s25](/images/3.clas/s25.png)

The Comprehend classification process has also generated the Textract output from the documents (present under the `classification-output/amazon-textract-output`). This directory contains a folder for each document with the **Amazon Textract** JSON response. Let's load the plain text of each of these documents into the data frame. We use the pretty printer tool to get the LINES out of the documents.
    ![s26](/images/3.clas/s26.png)

Continue to the Lab