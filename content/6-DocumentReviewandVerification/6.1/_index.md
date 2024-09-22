---
title : "Amazon S3 bucket setup and requirements"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 6.1 </b> "
---

- We will need an Amazon S3 bucket, which will be used to store data for A2I workers. This is already created as part of the CloudFormation stack. The name of the S3 bucket should be of the pattern `idp-a2i-xxxxxxxx`. Navigate to the Amazon S3 console to find the bucket name.
Go to S3
    ![s1](/images/6/s1.png)
    ![s2](/images/6/s2.png)

### Setup an A2I Human review workflow
- Go to the Amazon SageMaker console and click the Human review workflow option under Augmented AI in the left panel. Then click the Create human review workflow button.
    ![shu](/images/6/A2IHumanRWCreate.png)
- Provide a Name for the human review workflow. The S3 bucket value must be of the pattern s3://idp-a2i-xxxxxx/. 
    ![s3](/images/6/s3.png)
- In IAM Role, select Create a new role and then enter the name of the S3 bucket (without s3://, such as idp-a2i-xxxxxx).
    ![s4](/images/6/s4.png)
    ![s5](/images/6/s5.png)
    ![s6](/images/6/s6.png)
- Under Task type, select Textract - Key-value pair extraction option.
    ![s7](/images/6/s7.png)
- Next, under Amazon Textract form extraction - Conditions for invoking human review, select the Trigger human review for all form keys identified by Amazon Textract with confidence scores in a specified range checkbox and enter the values shown below. You can also customize worker task templates but for the purpose of this demo select Create from a default template and enter a Template name (example: idp-a2i-template).
    ![s8](/images/6/s8.png)
    ![s9](/images/6/s9.png)
- Under **Worker task template design** enter the **Task description**. You can also customize the **Instructions** as shown below.
    ![s10](/images/6/s10.png)
- Under **Workers** section, select the Private worker type. Click on the create a **new team** link to create a new Private Team.
    ![s11](/images/6/s11.png)
    ![s12](/images/6/s12.png)
- Under **Add workers**, select **Invite new workers by email**. In the **Email addresses** section enter your email. Under organization name enter **your company name**. For **Contact Email** use your email to receive instructions. Leave the other fields as default and click **Create Private Team**.
    ![s13](/images/6/s13.png)
    ![s14](/images/6/s14.png)
- Back to **Create Human flow** and refresh:
    ![s15](/images/6/s15.png)
- Click **Create** to complete creation of the Human review workflow. Once created, the workflow should be active and ready to use.
  

  
  
    
  
  


