---
title : "Document Extraction and Enrichment"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
>⚠️ PRE-REQUISITE: In order to execute this notebook, make sure you have completed the first notebook 01-idp-document-classification.ipynb
### Overview
So far, in the previous two modules, we have categorized documents and identified the bank statements, invoices, and receipt documents. In this module we will look at Amazon Comprehend's default entities and also train an Amazon Comprehend custom entity recognizer and deploy an endpoint with it. The purpose of the custom entity recognizer is to identify the specific entities and generate custom metadata about our document in CSV format to be later analyzed by the business use case. In adition to this we also want to identify any checking and savings account numbers in the bank statements and perform redactions on them.
   ![arch2](/images/4/arch2.png)

### What is Named Entity Recognition (NER)?
Named entity recognition (NER) is a natural language processing (NLP) sub-task that involves sifting through text data to locate noun phrases called named entities and categorizing each with a label, such as person, organization, or brand. For example, in the statement “I recently subscribed to Amazon Prime,” Amazon Prime is the named entity and can be categorized as a brand.

### Getting Started
Open the `03-idp-document-enrichment.ipynb` notebook and follow the steps below
   ![s1](/images/5/s1.png)
### Step 1: Setup notebook
In this step, we will import some necessary libraries that will be used throughout this notebook. 
   ![s2](/images/5/s2.png)
### Step 2: Perform Name Entity Recognition using Amazon Comprehend
We have categorized our documents according to their respective document types and stored them in S3. Next, we will perform name entity recognition for 1 bank statement and 1 receipt using Amazon Comprehend NER, in this case Comprehend will extract the prebuilt generic entity types from the documents.

We will start the process by loading the extracted document text from S3 into a dataframe and subsequently using Amazon Comprehend DetectEntities API.
   ![s3](/images/5/s3.png)
Execute entity extraction on Bank Statement
You can see various entities in the text from the our sample bank statement. Note that these are the default entities that Amazon Comprehend has detected using the default pre-trained entity recognizer.
   ![s4](/images/5/s4.png)

Although entity extraction worked fairly well in identifying the generic entity types for everything in the documents, we want specific entities to be recognized for our use case. More specifically, we need to identify the customer's Savings and Checking bank account numbers, for example we want the entity types to be "CHECKING_AC" and "SAVINGS_AC".

Amazon Comprehend's default prebuilt entity recognizer isn't aware of these entity types, so we will need to train and use a custom entity recognizer in this notebook. We will also perform some document enrichments for example, in the bank statement we want to redact the customer's account numbers. We will discuss more and do all of this in the next notebook.
### Step 3: Train a custom Amazon Comprehend entity recognizer 
We will be training a custom Amazon Comprehend entity recognizer. There are two ways a custom recognizer can be trained -

- [Using Annotations](https://docs.aws.amazon.com/comprehend/latest/dg/cer-annotation.html)
- [Using Entity Lists](https://docs.aws.amazon.com/comprehend/latest/dg/cer-entity-list.html)
Annotations uses a large set of PDF files that have been annotated. These annotations can be created with service such as Amazon Ground Truth where real human workers can review your files and annotate them. This method is quite involved and if you are interested to learn more refer to this blog and this blog.

In our case, we will use Entity Lists, which is a CSV file that should contain the texts and it's corresponding entity type. The entities in this file is going to be specific to our business needs. For the purposes of this exercise, we have provided an entity list in CSV format in the `/entity-training/` directory called entitylist.csv. This file contains a custom entity Type for customer account numbers. We have used CHECKING_AC and SAVINGS_AC as the custom entity types. With this, we ultimately need the custom entity recognizer to recognize the savings and checking bank account numbers.

Let's take a look at our entity list.
   ![s5](/images/5/s5.png)
Let's train a custom entity recognizer with Amazon Comprehend. In order to train a custom entity recognizer we will need the entity list and the set of documents to train the model. We will use the same set of documents that we used earlier to train the custom classifer for this purpose.

Each custom entity needs atleast 100 samples in the data corpus (documents) for training purposes, meaning you should have atleast a 100 documents containing examples of each of the custom entities in your training dataset. Also, a minimum of 250 entity matches are needed per entity in the entity list to train a model for custom entity recognition. We have provided a training corpus named entity_training_corpus.csv which can be used to train the entity recognizer along with the entity list. Note that this corpus was generated the same way we generated training data for training a custom classifier in the first notebook. With these two data sets we will use Amazon Comprehend's CreateEntityRecognizer API.

   ![s6](/images/5/s6.png)

Let's now train a custom entity recognizer with this data and the entity list of savings and checking account numbers
   ![s7](/images/5/s7.png)
Check status of the Comprehend custom entity recognizer job
   ![s8](/images/5/s8.png)

### Step 4: Create custom entity recognizer real-time endpoint
We will create a real time entity recognizer endpoint with the trained entity recognizer.
   ![s9](/images/5/s9.png)
Once created, the endpoint can be located in the Amazon Comprehend console.
   ![s10](/images/5/s10.png)
   ![s11](/images/5/s11.png)
### Document Enrichment 1
We now have a custom entity recognizer real-time endpoint using which we can extract the custom entities from one of our bank statement documents.
   ![s11](/images/5/idp-custom-entity.png)
Now instead of returning us generic entities, Amazon Comprehend is returning us the entities from our scanned document that we are interested, i.e. the checking and savings account number.
   ![s12](/images/5/s12.png)

### Enrichment 2: Perform redaction document enrichment
We still need to perform some enrichments on the document. Since the document contains the customers savings and checking account numbers, we would like to redact those. Since we already know, by means of our custom entity, the savings and checking account number of the customer, we can easily use Amazon Textract's geometry data to redact that information wherever they appear in the document.
   ![s11](/images/5/idp-redaction.png)

We will pick a bank statement from our list of documents, we will get the S3 location of the document and then perform the actions below-

- Use Amazon Textract to get the geometry information i.e. the bounding boxes, of all the lines in the document
- Use the extracted text above to identify the entities `CHECKING_AC` and `SAVINGS_AC`, using Comprehend custom entity recognizer
- Find the bounding box for the `CHECKING_AC` and `SAVINGS_AC` words from the Textract response
- Use the bounding box geometry to annotate the document and redact the customer name and address.
   ![s13](/images/5/s13.png)

The function above finds the custom entities in the document, finds the corresponding geometry information of the custom entity text and perform redaction on the document. Let's call it for a sample bank statement.
   ![s14](/images/5/s14.png)
Once our redacted file has been generated, lets take a look at it...
   ![s15](/images/5/s15.png)
   ![s14](/images/5/redacted-doc.png)
As you can see, the checking and savings account numbers are hidden in the document now.

### Conclusion
In this notebook we trained an Amazon Comprehend custom entity recognizer using our own entity list so that we can extract those entities from our documents. We used 2 entities CHECKING_AC, and SAVINGS_AC. We then created an endpoint with the custom entity recognizer and performed a detect_entities with the endpoint with one of the bank statements. Finally, we saved the extracted entities into a CSV file and uploaded it to S3 for further analysis.

We still needed to perform some enrichments on the document. Since the document contains the customers checking and savings account numbers, we would like to redact those. Since we already know, by means of our custom entity, the customer's checking and savings bank account numbers, we used Amazon Textract's geometry data to redact that information in the document.




   






