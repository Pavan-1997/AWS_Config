# AWS Config

It is a service provided by Amazon Web Services (AWS) that helps you assess, audit, and evaluate the configurations of your AWS resources. It provides a way to manage and track the configuration changes and compliance of your AWS environment over time. AWS Config continuously monitors the state of your resources and records configuration changes, allowing you to maintain a history of these changes and ensuring that your resources adhere to your desired configurations.

---
We use AWS Config to detect compliant and non-compliant ec2 instances for the below rule.

- Compliant (EC2 Instance has Monitoring enabled)
- Non-Compliant (EC2 Instance does not have Monitoring enabled)
  
1.  Go to AWS Config from AWS Management Console and Click on Get started


2. Go with default values and click on Create


3. Go to AWS Lambda from AWS Console -> Click on Create a function -> Give Runtime - Python 3.11 -> Click on Create function -> Give the python file in the repo - Click on Deploy 


5. Now go back to Step 1 Rules on the left pane -> Click on Add rule -> Click on Create custom Lambda rule -> Click on Next -> Give Name -> Give the ARN of Lambda from the above step

    In Evaluation mode -> Select trigger type as When configuration changes -> Select Resources -> Select Resource type - AWS EC2 Instance -> Click on Next -> Click on Save


6. Now go to the Lambda function created -> Under Configuration, Click on Permissions on the left -> Open the Role > Now IAM gets opened, click on Add permissions -> Attach policies and add below
     
    `CloudWatchFullAccess`
    `AmazonEC2FullAccess`
    `AWS_ConfigRole`
    `AWSCloudTrail_FullAccess`
 

7. Now create an EC2 instance and under Monitoring tab -> Click on Manage detailed monitoring ->  Enable the detailed monitoring -> Click on Confirm

    ![image](https://github.com/Pavan-1997/AWS_Config/assets/32020205/fc676276-50f6-4ef9-a598-c073eda95f7c)
    
    ![CONFIG_EN](https://github.com/Pavan-1997/AWS_Config/assets/32020205/440de8fb-51e6-4b01-b055-26e1b6e78fd2)


8. Now go to the AWS Config -> In the dashboard after few minutes you should see the Complaint resource(s) as 1 If not,

    Go to Rules on the left pane -> Click on the rule created -> Actions -> Click on Re-evaluate

      ![CONFIG_REVAL](https://github.com/Pavan-1997/AWS_Config/assets/32020205/c0375159-c822-496e-b942-76cdd0acf061)

    
    Now in the Resources in scope -> Select filter to All -> Click on refresh you should see the EC2 under compliance

      ![CONFIG_COMP](https://github.com/Pavan-1997/AWS_Config/assets/32020205/09455d24-c5a9-41ac-8c79-2be3457d736c)

    
10. Now follow Step 7. to Disable the detailed monitoring

    ![CONFIG_DIS](https://github.com/Pavan-1997/AWS_Config/assets/32020205/541dd717-5ab8-42c6-b3fd-8216f7aa8e2c)


11. Followed by Step 8.

    ![CONFIG_NON_COMP](https://github.com/Pavan-1997/AWS_Config/assets/32020205/0ea880e5-58ac-4f89-86d4-66e0e6d05f56)
