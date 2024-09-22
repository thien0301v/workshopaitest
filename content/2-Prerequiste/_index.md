---
title : "Preparation "
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

{{% notice info %}}
You need to create 1 AWS account to perform this lab.
{{% /notice %}}

If you don't already have an AWS account with Administrator access create one now  .
  - [Create AWS account](https://aws.amazon.com/vi/getting-started/)

### **Deloy CloudFormation Stack**
1. Download the AWS CloudFormation templates using the "Download Template" button below and use it in the AWS Cloudformation console
It cotains a sample of SageMaker [Download Template](https://idp-assets-wwso.s3.us-east-2.amazonaws.com/cfn/idp-workshop-templates.zip).
 ![stack](/images/2.prerequisite/yaml-stack.png)

2. Search the "Cloud Formation" 
   ![search](/images/2.prerequisite/search.png)
3. Create "stack" and select "With new resources(standard)
   ![create](/images/2.prerequisite/create.png)
4. In prepare template, we choose "Choose an existing template", Specify template we choose "Upload a template file"
   ![create](/images/2.prerequisite/create1.png)
And "Next"
5. Stack name is "IDPSageMakerCfnStack", Parameters is default
   ![name](/images/2.prerequisite/name.png)
And "Next"
6. Next to Step 4: Review and Create
  ![step4](/images/2.prerequisite/step4.png)
7. Wait to excute and we get this. 
 ![complete](/images/2.prerequisite/complete.png)

##### Once the CloudFormation stacks are deployed, follow the instructions below to access Amazon SageMaker Studio IDE

### Amazon SageMaker Studio access
1. Search the "SageMaker"
   ![sage](/images/2.prerequisite/sage.png)
2. You should already be in the Domains page, if not click on the Domains option in the left menu. Next, click on the Domain name.
     >Note: if you changed the name of your domain in the cloudformation template then that name will be shown in the list.
     ![domain](/images/2.prerequisite/sagedomain.png)
3. In the **Domain details** page click on the Launch drop-down and then click on **Studio**
   ![studio](/images/2.prerequisite/studio.png)
4. The SageMaker Studio IDE will open in a new browser tab. The page may take a few minutes to load when you access SageMaker Studio for the first time. Once the SageMaker Studio IDE loads, you will be presented with the UI with a screen that looks like this. Click on "Studio Classic" (on the left menu near the top).
   ![studioclassic](/images/2.prerequisite/studioclassic.png)
5. You will see an existing SageMaker Studio classic application running. Click on "Open".
   ![open](/images/2.prerequisite/openclassic.png)
6. You will be redirected to a new browser tab with the Amazon SageMaker Studio Classic IDE:
    ![jupy](/images/2.prerequisite/jupyterlab.png)
7. Once you are in the Amazon SageMaker Studio IDE, you should already see the workshop repo folder.
   ![repo](/images/2.prerequisite/repo.png)