---
title : "Verification"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 6.2 </b> "
---
Now let's go back to the notebook `04-idp-document-a2i.ipynb`. **Start running the code cells from the beginning. You will need to provide few details as you move along.**
- Enter the S3 bucket name idp-a2i-xxxxxx to initialize the BUCKET variable. We will use this BUCKET variable throughout the notebook.
    ![s16](/images/6/s16.png)
- You would need to provide the private work team ARN that you had created before. To find the work team ARN, click the **Human review workflow** you created earlier and copy the ARN from the Summary section under Workforce. It should look like `<arn:aws:sagemaker:<region>:<account_id>:workteam/private-crowd/<team-name>`. Enter this value to initialize the `WORKTEAM_ARN` in the notebook.
    ![s17](/images/6/s17.png)
- Now that we have setup the A2I WorkFlow definition, all that's left is calling Amazon Textract's Analyze Document API including the A2I paramters in the HumanLoopConfig. Provide the A2I workflow ARN to be used by Amazon Textract. You can find the workflow ARN in the Human review workforce **Summary** screen.
    ![s18](/images/6/s18.png)
- Execute the code cell to perform AnalyzeDocument. Once data is extracted using Amazon Textract, the key-value pairs show up in the labeling portal for human review.
    ![s19](/images/6/s19.png)
- Then go to **Amazon SageMaKer** -> Labeling workforces
    ![s20](/images/6/s20.png)
- Click to Labeling portal sign-in URL
    ![s21](/images/6/s21.png)
- Login to the labelling/human review portal. You should have received an email with a link to the Labeling/human review portal with details about how to login and a portal URL. Follow the instructions in the email, you will need to reset your password to login.
- You can see that a human review task has been added. Select the job and click on **Start Working**.
    ![s22](/images/6/s22.png)
- You can now get to see the extracted information on the right, in order to verify and make changes if needed. Submit the job once completed. You also have the option to decline and release the task if needed.
    ![s23](/images/6/s23.png)

### Conclusion
In this notebook we created an A2I human review workflow for **Amazon Textract** including a private work team using Amazon Augmented AI. We then used **Amazon Textract** to extract data from a sample document and added a Human Config Loop for Human Review. Finally, we performed a manual review task using a customized portal.