---
title : "Classify a document with the real-time endpoint (optional)"
date : "`r Sys.Date()`"
weight : 7
chapter : false
pre : " <b> 3.8 </b> "
---
The next step is to use the Amazon Comprehend real-time endpoint to classify these documents. We use the `comprehend.classify_document()`function with extracted document text and inference endpoint as input parameters. To classify a sample document, we will first convert the document to ByteArray and then use **Textract** `classify_document` API to classify it. Since `classify_document` is a real time (synchronous) API we will call it with the document bytes of the above sample document. Again, as before we will let Amazon Comprehend utilize Amazon Textract behind the scenes to read the document and then classify it. Since we are allowing Comprehend to use Amazon Textract behind the scenes to extract the text, we will be limited to use single page documents.

Once the endpoint has been created, we will use a mix of documents under the `/samples/mixedbag/` directory and try to classify them to bank statement, invoice, and receipt documents respectively.
    ![s29](/images/3.clas/s29.png)
Let's view one of the documents
    ![s30](/images/3.clas/s30.png)
To classify this sample document, we will first convert the documents to ByteArray and then use Textract classify_document API to classify it. Since `classify_document` is a real time (synchronous) API we will call it with the document bytes of the above sample document. Again, as before we will let Amazon Comprehend utilize Amazon Textract behind the scenes to read the document and then classify it. Since we are allowing Comprehend to use Amazon Textract behind the scenes to extract the text, we will be limited to use single page documents.
    ![s31](/images/3.clas/s31.png)
Lets now run the inference on our sample document
    ![s32](/images/3.clas/s32.png)
Note that Comprehend will return all the classes of documents with a confidence score linked to each class in an array of key-value pairs (Name-Score), we can pick only the document class with the highest confidence score from the endpoint's response.
### Conclusion
In this notebook we have trained an Amazon Comprehend custom classifier using our sample documents by extracting the text from the documents using Amazon Textract and labeling the data into a CSV file format training dataset. We then trained an Amazon Comprehend custom classifier with the extracted text and created an **Amazon Comprehend Classifier** real time endpoint to perform classification of a set of unknown documents.

In the next notebook we will look at a few methods to perfrom extraction of key insights from our documents using Amazon Textract.