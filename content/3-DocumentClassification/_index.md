---
title : "Document Classification"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---



### Overview

Document classification is a two-step process. First, you train a custom classifier to recognize the classes that are of interest to you. Then you send unlabeled documents to be classified.

To train the classifier, specify the options you want, and send Amazon Comprehend documents to be used as training material. Based on the options you indicated, Amazon Comprehend creates a custom ML model that it trains based on the documents you provided. This custom model (the classifier) examines each document you submit. It then returns either the specific class that best represents the content (if you're using multi-class mode) or the set of classes that apply to it (if you're using multi-label mode).

In this lab we will walk you through a hands-on lab on document classification using Amazon Comprehend Custom Classification . We will use Amazon Textract to first extract text from our documents, label them, and then use the data for training our Amazon comprehend custom classifier. Our goal is - given a group of unknown documents, we want to be able to categorize which documents are bank statements, which are invoices, and which are receipts. To prepare the training data, we will use pre-existing bank statements, receipts, and invoices.

![arch](/images/3.clas/arch.png) 

### Sample Document Corpus
#### Bank Statements
The image below is the first page of a standard multi-page bank statement with details such as Customer Name, Address, Account Summary, Current balance, etc.
![bank](/images/3.clas/bank-doc.png)

#### Invoices
The image below is a standard payment invoice with details such as Business Details, Bill to, products, invoice ID etc.
![invoice](/images/3.clas/invoice-doc.png)

#### Receipts
The image below is a standard store reciept with details such as Items purchased, Store Details, Retail price for each Item, Sales Tax Rate, etc.
![receipt](/images/3.clas/receipt-doc.png)
