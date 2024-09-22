---
title : "Document Extraction"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---


### Extracting data from documents using Amazon Textract
Amazon Textract is a machine learning (ML) service that automatically extracts text, handwriting, and data from scanned documents. It goes beyond simple optical character recognition (OCR) to identify, understand, and extract data from forms and tables. Expand the following sections to take a brief look at the document extraction capabilities of Amazon Textract.

### Parsing Amazon Textract API responses
You can extract text and structured data information using Amazon Textract's [`DetectDocumentText`](https://docs.aws.amazon.com/textract/latest/dg/API_DetectDocumentText.html)  and AnalyzeDocument  APIs respectively. These APIs respond with JSON data which contains WORDS, LINES, FORMS, TABLES, geometry or bounding box information, relationships and so on. This JSON response can be tricky to parse, especially for larger or multi-page documents. For this purpose, we will use a group of tools named **amazon-textract-textractor** that makes it easy to obtain information such as WORDS, LINES, TABLES, and FORMS from the document, and obtain bounding box information. Following are the features available

- A [caller](https://github.com/aws-samples/amazon-textract-textractor/tree/master/caller)  which provides a collection of ready to use functions and sample implementations to speed up the evaluation and development for any project using Amazon Textract. Making it easy to call Amazon Textract regardless of file type and location.
- A [response parser](https://github.com/aws-samples/amazon-textract-response-parser)  to easily parse JSON returned by Amazon Textract. The library parses JSON and provides programming language specific constructs to work with different parts of the document.
- A [prettyprinter](https://github.com/aws-samples/amazon-textract-textractor/tree/master/prettyprinter)  which provides functions to format the output received from Amazon Textract in more easily consumable formats such as CSV or markdown.
- An [overlayer](https://github.com/aws-samples/amazon-textract-textractor/tree/master/overlayer)  that gets you bounding box geometry information that can be used for annotation, or redaction purposes.


### Getting Started with Lab
In this part, we will look at ways to extract information from documents. Open the `02-idp-document-extraction.ipynb` notebook in Amazon SageMaker Studio and follow the steps below.
   ![s1](/images/4/s1.png)

### Step 1: Setup notebook
In this step we will select kernel like previous notebook that will be used in the notebook.
   ![s2](/images/4/s2.png)
Then run scripts in Step 1
Let's select a bank statement we classified in the previous exercise
   ![s3](/images/4/s3.png)
   ![s4](/images/4/s4.png)


### Step 2: Extract unstructured data with Amazon Textract
In this step we will mainly look at how to extract text information (LINES and WORDS) from one of the bank statements. Text data in the form of WORDS and LINES can be extracted from documents using Amazon Textract DetectDocumentText API. Following code calls the API to extract text from documents.

Amazon Textract is an ML powered OCR service that is capable of detecting and extracting text from documents. Text data in the form of WORDS and LINES can be extracted from documents using Amazon Textract DetectDocumentText API. Let's extract the words and lines from the bank statement.
   ![s5](/images/4/s5.png)
As you can notice, we were able to extract the LINES and WORDS from the document, but we also lost some of the structural formatting within the document. For example the document contains a few tables and we would like to extract the table information in a tabular structure. So let's do that next.

### Step 3: Extract table data using Amazon Textract
In this step we will take a brief look at how to extract table information from the bank statemente. Our bank statement has two tables.
   ![s6](/images/4/s6.png)
As you can see, the response from Amazon Textract is a large `JSON` object that contains a lot of information. Let's parse out the table data from this reponse. To do this, we will see how to extract the tables using the textract response parser tool that we installed earlier. 
   ![s7](/images/4/s7.png)
In the code cells above, we used the Textract `AnalyzeDocument` API to extract info from the document and subsequently used textract response parser Document to parse out the tables from the `JSON` response. We can further use additional tooling to call the Textract API and use textract pretty printer tool to view the tables in a slightly more human readable way. We will see how to extract the tables using the Textract pretty printer tool. We will also use `call_textract` method from the Textract Caller tool that we installed earlier. These set of tools make it easy for us to make Textract API calls and parse it's JSON output. In our subsequent sections, we will make use of these tools to make API calls and subsequently to parse the JSON response.
   ![s8](/images/4/s8.png)
In the code cell above, we extracted the tables as a Python List and then converted them to Pandas DataFrame. You can also extract tables in other formats such as CSV, TSV etc. Refer to the [PrettyPrinter](https://github.com/aws-samples/amazon-textract-textractor/tree/master/prettyprinter) documentation for more. Now let's look at the DataFrames.
   ![s9](/images/4/s9.png)

### Step 4: Extract forms (key/value) data using Amazon Textract
Let's look at how Amazon Textract can be used to extract form data from the document. In this example, we will use a sample Employment Verification form.
   ![s10](/images/4/s10.png)
In our previous example, our document was in S3 and we called Amazon Textract by specifying the S3 location of the document. In this case our document is present locally, we can either upload this document into S3, or we can use the document's Byte Array from our local environment to call the API. Let's use the document Byte Array for this example. Note that this method only applies to Textract Sync (real-time) APIs, since the async APIs only support documents placed in S#. In the code cell below, we first convert our document to a Byte array, and then call the `AnalyzeDocument` API with FORMS feature. Subsequently we use textract response parser tool to parse out the form key/value pairs and print them out.
   ![s11](/images/4/s11.png)
And the result
   ![s12](/images/4/s12.png)

### Step 5: Query based extraction using Amazon Textract 
When processing a document with Amazon Textract, you may add queries to your analysis to specify what information you need. This involves passing a question, such as "What is the customer's social security number?" to Amazon Textract. Amazon Textract will then find the information in the document for that question and return it in a response structure separate from the rest of the document's information. Queries can be processed alone, or in combination with any other FeatureType, such as TABLES or FORMS. Queries can be a powerful tool in situations where only a few pieces of critical information is desired from a document. 

Let's pass a couple of Queries to extract from our Employment Verification form.
   ![s13](/images/4/s13.png)
   ![s14](/images/4/s14.png)

### Step 6: Signature detection with Amazon Textract
Amazon Textract can detect the presence of signatures in documents. The AnalyzeDocument API has the following four feature types – Forms, Tables, Queries, and Signatures. The Signatures feature can be used by itself or in combination with other feature types. When used by itself, Signatures feature type provides a json response that includes a) location and confidence scores of the detected signatures and b) raw text (words and lines) from the documents. If the Signatures feature is used along with Forms feature that extracts key value pairs in a form, the detected signature will be associated as a value to the relevant key. Similarly, when used along with Tables feature type, the detected signature will be associated to a cell within the table.

Let's try to detect the signatures in our Employment Verification form.
   ![s15](/images/4/s15.png)

Textract has detected three signatures in the document along with their bounding box information along with the confidence scores.

### Step 7: Extracting invoices/receipts with Amazon Textract
Let's now look at the `AnalyzeExpense` API to extract information from an invoice document.
   ![s16](/images/4/s16.png)

It is important to note that textract provides the ability to seperately extract the "line items" in the invoice and the "Summary" of the invoice.
   ![s17](/images/4/s17.png)
   ![s18](/images/4/s18.png)

### Step 8: Extracting identity documents with Amazon Textract 
To see how extraction of identity documents works with Amazon Textract we will use a sample Passport document. Passport is a special document, i.e. an Identity document. To extract infromation from US passports and driver's license, Amazon Textract's AnalyzeID API can be used.
   ![s19](/images/4/s19.png)
We will use the call_textract_analyzeid tool from the amazon-textract-textractor library.
   ![s20](/images/4/s20.png)

Note that in the call to call_textract_analyzeid you can also pass an S3 path to the parameter document_pages as
`call_textract_analyzeid(document_pages=["s3://bucket/prefix/doc.png"])`

Let's look at the extracted information from the Passport document. Notice that the Keys are normalized, this means it makes it easy to parse out the required information from the response JSON from Textract.
   ![s21](/images/4/s21.png)








